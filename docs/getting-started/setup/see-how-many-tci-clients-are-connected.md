# Applet del servidor TCI

El applet del servidor TCI ejecuta un servidor WebSocket TCI de estilo Expert para que software de terceros para registro, modos digitales y SDR (Log4OM, herramientas SunSDR, etc.) puedan leer y controlar el radio mediante el protocolo TCI.

El audio TX de TCI se recibe a través del WebSocket y se alimenta en una ranura de flujo dax_tx dedicada que es independiente de la ruta del dispositivo de audio DAX2 de SmartSDR en Windows, por lo que la transmisión TCI funciona en todas las plataformas, incluyendo Windows y Linux, sin PipeWire.

## Ver cuántos clientes TCI están conectados

El applet del servidor TCI muestra un conteo de clientes en vivo en su indicador de estado. Use esto para confirmar que Log4OM, las herramientas SunSDR o cualquier otro cliente TCI se haya conectado exitosamente.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El applet TCI requiere una conexión activa al radio.
- El servidor TCI debe estar en ejecución (Habilitar activado). Si está detenido, el estado muestra `(stopped)` y no hay conteo de clientes disponible.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha para abrir el applet del servidor TCI.
2. Lea el indicador de estado junto al campo Puerto.

Cuando el servidor está en ejecución y al menos un cliente está conectado, el estado muestra:

```
:<puerto> (N clientes)
```

Por ejemplo, con dos clientes conectados en el puerto predeterminado:

```
:50001 (2 clientes)
```

Cuando el servidor está en ejecución pero no hay clientes conectados, el estado muestra el puerto y `(0 clientes)`. Cuando el servidor está detenido, el estado muestra `(stopped)`.

## Qué hace cada control

| Control                        | Descripción                                                                                                                                                                                                                              | Notas                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Puerto (Port)                  | Puerto en el que escucha el servidor WebSocket TCI. Los valores fuera de rango se ajustan a `50001`.                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Habilitar (Enable)             | Inicia o detiene el servidor TCI.                                                                                                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Estado del servidor            | Muestra `(stopped)`, `:<puerto> (N clientes)` o `(port in use)`. Se vuelve rojo en caso de error de enlace.                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Medidor+deslizador de ganancia RX1–RX4 | Medidor/deslizador combinado; arrastrar establece la ganancia RX de TCI para el canal y emite `tciRxGainChanged`.                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Medidor+deslizador de ganancia TX       | Arrastrar establece la ganancia TX de TCI y emite `tciTxGainChanged`. El clic derecho abre un selector de modo de desbordamiento TX (Clip / NaNGuard / Measure).                                                                         | TciServer::setTxGain persiste TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú de clic derecho permite a los usuarios elegir cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modo digital: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo pone a cero NaN/Inf), o Measure (bypass verdadero con conteo de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Modo de desbordamiento TX (clic derecho) | Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite `tciTxOverflowModeChanged`. El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento. |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Etiquetas de asignación de segmento RX/TX | Muestran qué segmento impulsa actualmente cada fila RX/TX. Muestra `—` cuando no hay ningún segmento asignado o `Segmento <letra>` cuando hay un segmento mapeado.                                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

## Detalles del modo de desbordamiento TX

Haga clic derecho en el medidor/deslizador de ganancia TX para abrir el menú de modo de manejo de desbordamiento TX. Esta configuración determina cómo se manejan las muestras fuera de rango (>1.0) de los clientes TCI antes de que el radio las vea.

| Modo        | Valor | Descripción                                                                                                                                                                                                                     |
|-------------|-------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Clip        | 0     | Sujeta firmemente los picos a ±1.0. Predeterminado defensivo; introduce armónicos en los picos pero protege la conversión a int16 descendente.                                                                                  |
| NaN guard   | 1     | Pasa las muestras bit a bit sin cambios; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad del tono del modo digital; los flotantes fuera de rango llegan al radio.                                       |
| Measure     | 2     | Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión a int16 descendente aún sujeta en la ruta DAX nativa del radio.                                                                                    |

Clip es el valor predeterminado y preserva el limitador defensivo heredado. NaNGuard y Measure son progresivamente menos destructivos para la fidelidad del tono del modo digital. El modo se persiste como `TciTxOverflowMode` (0, 1 o 2).

## Consejos

- El conteo de clientes se actualiza automáticamente cuando un cliente se conecta o desconecta; no es necesario refrescar.
- Cuando hay un cliente conectado, el estado muestra `(1 cliente)` (singular); dos o más muestran `(N clientes)` (plural).
- El texto de estado se vuelve azul cuando hay uno o más clientes conectados, lo que facilita verlo de un vistazo.

## Solución de problemas

- **El estado muestra `(port in use)`** — Otro proceso ya está vinculado al puerto configurado. Cambie el valor en el campo Puerto a un puerto no utilizado en el rango 1024–65535 y presione Enter. El servidor se reinicia automáticamente si Habilitar está activado.
- **El estado permanece `(stopped)` después de hacer clic en Habilitar** — El enlace falló y Habilitar se desactivó. Verifique el valor del Puerto y confirme que ninguna otra aplicación esté usando ese puerto.
- **El conteo de clientes permanece en 0** — Confirme que la aplicación de terceros esté configurada para conectarse al host y puerto correctos. El puerto en uso se muestra en el indicador de estado.

## Relacionados

- [Enable the TCI server for Log4OM / SunSDR clients](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Change the TCI port](../../features/tci/change-the-tci-port.md)
- [Autostart TCI on launch](../../features/tci/autostart-tci-on-launch.md)
- [TCI Server overview](../../features/tci/overview.md)
