# Applet de servidor TCI

El applet de servidor TCI ejecuta un servidor WebSocket TCI estilo Expert para que software de terceros de registro, modos digitales y SDR (Log4OM, herramientas SunSDR, etc.) pueda leer y controlar la radio mediante el protocolo TCI.

El audio de TX de TCI se recibe a través del WebSocket y se introduce en una ranura dedicada de flujo dax_tx que es independiente de la ruta del dispositivo de audio DAX2 de SmartSDR en Windows, por lo que la TX de TCI funciona en todas las plataformas, incluidos Windows y Linux, sin PipeWire.

## Vea cuántos clientes TCI están conectados

El applet de servidor TCI muestra un recuento de clientes en vivo en su indicador de estado. Úselo para confirmar que Log4OM, las herramientas SunSDR o cualquier otro cliente TCI se ha conectado correctamente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El applet TCI requiere una conexión de radio activa.
- El servidor TCI debe estar en ejecución (Enable activado). Si está detenido, el estado muestra `(stopped)` y no hay recuento de clientes disponible.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha para abrir el applet de servidor TCI.
2. Lea el indicador de estado junto al campo Port.

Cuando el servidor está en ejecución y al menos un cliente está conectado, el estado muestra:

```
:<port> (N clients)
```

Por ejemplo, con dos clientes conectados en el puerto predeterminado:

```
:50001 (2 clients)
```

Cuando el servidor está en ejecución pero no hay clientes conectados, el estado muestra el puerto y `(0 clients)`. Cuando el servidor está detenido, el estado muestra `(stopped)`.

## Qué hace cada control

| Control                        | Descripción                                                                                                                                                                                     | Notas                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Port                           | Puerto en el que escucha el servidor WebSocket TCI. Los valores fuera de rango se ajustan a `50001`. Tiene nombre accesible "TCI port" y descripción accesible "TCP port the TCI server listens on". |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Enable / Disabled              | Inicia o detiene el servidor TCI. El texto del botón se actualiza dinámicamente a "Enabled" cuando el servidor está en ejecución y "Disabled" cuando está detenido. Tiene nombre accesible "TCI server enable". | El botón es marcable. Si Autostart TCI está habilitado en la configuración, el botón se inicializa como "Enabled" y marcado. Al alternar, el texto se actualiza inmediatamente. Si el enlace falla, el botón vuelve a desmarcarse y el texto revierte a "Disabled".                                                                                                                                                                                                                                                                                                             |
| Server status                  | Muestra `(stopped)`, `:<port> (N clients)` o `(port in use)`. Se pone en rojo al fallar el enlace.                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| RX1–RX8 gain+meter             | Medidor/deslizador combinado; al arrastrar se establece la ganancia de RX de TCI para el canal y se emite `tciRxGainChanged`.                                                                      | Cada deslizador tiene nombre accesible "TCI RX gain" seguido del número de canal (1–8) para compatibilidad con lectores de pantalla. Los canales por encima de la capacidad de slices de la radio se ocultan.                                                                                                                                                                                                                                                                                                                                                                         |
| TX gain+meter                  | Al arrastrar se establece la ganancia de TX de TCI y se emite tciTxGainChanged. El clic derecho abre el selector de modo de desbordamiento de TX (Clip / NaNGuard / Measure).                      | TciServer::setTxGain persiste TciTxGain internamente; la interfaz refleja el valor almacenado. El audio de TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú de clic derecho permite elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes de modos digitales: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo anula NaN/Inf), o Measure (bypass real con conteo de recorte). El predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| TX overflow mode (right-click) | Haga clic derecho en el medidor/deslizador de ganancia de TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento de TX. Emite `tciTxOverflowModeChanged`. El predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento. |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| RX/TX slice-assignment labels  | Muestran qué slice impulsa actualmente cada fila de RX/TX. Muestran `—` cuando no hay slice asignado o `Slice <letra>` cuando hay un slice mapeado.                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

## Detalles del modo de desbordamiento de TX

Haga clic derecho en el medidor/deslizador de ganancia de TX para abrir el menú de modo de manejo de desbordamiento de TX. Esta configuración determina cómo se manejan las muestras fuera de rango (>1.0) de los clientes TCI antes de que lleguen a la radio.

| Modo        | Valor | Descripción                                                                                                                                                                                                   |
|-------------|-------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Clip        | 0     | Limita los excesos a ±1.0. Predeterminado defensivo; introduce armónicos en el exceso pero protege la conversión int16 posterior.                                                                            |
| NaN guard   | 1     | Pasa las muestras bit a bit exactas; solo anula valores patológicos NaN/Inf. Preserva la fidelidad del tono de los modos digitales; los flotantes fuera de rango llegan a la radio.                          |
| Measure     | 2     | Nunca muta las muestras. Cuenta los excesos para telemetría; la conversión int16 posterior aún limita en la ruta DAX nativa de la radio.                                                                      |

Clip es el predeterminado y preserva el limitador defensivo heredado. NaNGuard y Measure son progresivamente menos destructivos para la fidelidad del tono de los modos digitales. El modo se persiste como `TciTxOverflowMode` (0, 1 o 2).

## Capacidad de canales RX

Las filas RX1–RX8 gain+meter se mapean a los canales DAX 1–8. En radios con menos de 8 slices, las filas por encima de la capacidad de slices de la radio se ocultan automáticamente. Por ejemplo, una radio con 4 slices muestra solo RX1–RX4; una radio con 8 slices muestra todas las RX1–RX8. Las etiquetas de asignación de slices a la derecha de cada fila muestran qué slice impulsa actualmente ese canal.

## Consejos

- El recuento de clientes se actualiza automáticamente cuando un cliente se conecta o desconecta; no es necesario actualizar.
- Cuando hay un cliente conectado, el estado muestra `(1 client)` (singular); dos o más muestran `(N clients)` (plural).
- El texto de estado se pone azul cuando hay uno o más clientes conectados, lo que facilita identificarlo de un vistazo.
- El texto del botón Enable cambia entre "Enabled" y "Disabled" para indicar claramente el estado actual del servidor.

## Solución de problemas

- **El estado muestra `(port in use)`** — Otro proceso ya está vinculado al puerto configurado. Cambie el valor en el campo Port a un puerto no utilizado en el rango 1024–65535 y presione Enter. El servidor se reinicia automáticamente si Enable está activado.
- **El estado permanece en `(stopped)` después de hacer clic en Enable** — El enlace falló y Enable volvió a apagarse. El texto del botón revierte a "Disabled". Verifique el valor de Port y confirme que ninguna otra aplicación use ese puerto.
- **El recuento de clientes permanece en 0** — Confirme que la aplicación de terceros está configurada para conectarse al host y puerto correctos. El puerto en uso se muestra en el indicador de estado.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Autostart TCI al iniciar](../../features/tci/autostart-tci-on-launch.md)
- [Resumen del servidor TCI](../../features/tci/overview.md)
