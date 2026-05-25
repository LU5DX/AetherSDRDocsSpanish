# Applet del servidor TCI

El applet del servidor TCI ejecuta un servidor WebSocket TCI de estilo Expert, de modo que el software externo de registro, modos digitales y SDR (Log4OM, herramientas SunSDR, etc.) pueda leer y controlar la radio a través del protocolo TCI.

El audio de TX de TCI se recibe a través del WebSocket y se introduce en una ranura de flujo dax_tx dedicada, independiente de la ruta del dispositivo de audio DAX2 de Windows SmartSDR. Así, la TX de TCI funciona en todas las plataformas, incluyendo Windows y Linux, sin necesidad de PipeWire.

## Ver cuántos clientes TCI están conectados

El applet del servidor TCI muestra un recuento de clientes en vivo en su indicador de estado. Utilícelo para confirmar que Log4OM, las herramientas SunSDR o cualquier otro cliente TCI se ha conectado correctamente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El applet TCI requiere una conexión de radio activa.
- El servidor TCI debe estar en ejecución (Activar conmutado a On). Si está detenido, el estado muestra `(stopped)` y no se muestra ningún recuento de clientes.

## Pasos

1. Haga clic en el botón de la bandeja **TCI** en la barra lateral derecha para abrir el applet del servidor TCI.
2. Lea el indicador de estado junto al campo Port.

Cuando el servidor está en ejecución y al menos un cliente está conectado, el estado muestra:

```
:<puerto> (N clients)
```

Por ejemplo, con dos clientes conectados en el puerto predeterminado:

```
:50001 (2 clients)
```

Cuando el servidor está en ejecución pero no hay clientes conectados, el estado muestra el puerto y `(0 clients)`. Cuando el servidor está detenido, el estado muestra `(stopped)`.

## Función de cada control

| Control                        | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Port                           | Puerto en el que escucha el servidor WebSocket TCI. Los valores fuera de rango se redondean a `50001`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Enable                         | Inicia o detiene el servidor TCI.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Server status                  | Muestra `(stopped)`, `:<puerto> (N clients)` o `(port in use)`. Se vuelve rojo en caso de error de enlace.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| RX1–RX4 gain+meter             | Medidor/deslizador combinado; arrastre para ajustar la ganancia de RX TCI para el canal y emite `tciRxGainChanged`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| TX gain+meter                  | Arrastre para ajustar la ganancia de TX TCI y emite `tciTxGainChanged`. El audio de TX TCI siempre está permitido, independientemente de la plataforma o la disponibilidad de DAX alojado.                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| TX overflow mode (right-click) | Haga clic derecho en el medidor/deslizador de ganancia de TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento de TX. Emite `tciTxOverflowModeChanged`. El valor predeterminado es Clip, por lo que los usuarios existentes no verán cambios en el comportamiento.                                                                                                                                                                                                                                                                                                                                                                                     |
| RX/TX slice-assignment labels  | Muestra qué slice impulsa actualmente cada fila RX/TX. Muestra `—` cuando no se asigna ningún slice o `Slice <letra>` cuando hay un slice mapeado.                                                                                                                                                                                                                                                                                                                                                                                                                                                |

## Detalles del modo de desbordamiento de TX

Haga clic derecho en el medidor/deslizador de ganancia de TX para abrir el menú del modo de manejo de desbordamiento de TX. Esta configuración determina cómo se manejan las muestras de los clientes TCI que están fuera de rango (>1.0) antes de que la radio las vea.

| Modo        | Valor | Descripción                                                                                                                                                                                                 |
|-------------|-------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Clip        | 0     | Recorta los excesos a ±1.0. Valor defensivo predeterminado; introduce armónicos en los excesos pero protege la conversión posterior a int16.                                                                              |
| NaN guard   | 1     | Pasa las muestras sin alterar bit a bit; solo pone a cero los valores NaN/Inf patológicos. Preserva la fidelidad del tono en modos digitales; los flotantes fuera de rango llegan a la radio.                                                           |
| Measure     | 2     | Nunca modifica las muestras. Cuenta los excesos para telemetría; la conversión posterior a int16 sigue recortando en la ruta DAX nativa de la radio.                                                                          |

Clip es el valor predeterminado y preserva el limitador defensivo heredado. NaNGuard y Measure son progresivamente menos destructivos para la fidelidad del tono en modos digitales. El modo se conserva como `TciTxOverflowMode` (0, 1 o 2).

## Consejos

- El recuento de clientes se actualiza automáticamente cuando un cliente se conecta o desconecta; no es necesario actualizar.
- Cuando hay un cliente conectado, el estado muestra `(1 client)` (singular); dos o más muestran `(N clients)` (plural).
- El texto de estado se vuelve azul cuando hay uno o más clientes conectados, lo que facilita su identificación de un vistazo.

## Solución de problemas

- **El estado muestra `(port in use)`** — Otro proceso ya está vinculado al puerto configurado. Cambie el valor en el campo Port a un puerto no utilizado en el rango 1024–65535 y presione Enter. El servidor se reinicia automáticamente si Enable está activado.
- **El estado permanece en `(stopped)` después de hacer clic en Enable** — El enlace falló y Enable volvió a Off. Verifique el valor del puerto y confirme que ninguna otra aplicación esté usando ese puerto.
- **El recuento de clientes permanece en 0** — Confirme que la aplicación de terceros esté configurada para conectarse al host y puerto correctos. El puerto en uso se muestra en el indicador de estado.

## Relacionado

- [Enable the TCI server for Log4OM / SunSDR clients](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Change the TCI port](../../features/tci/change-the-tci-port.md)
- [Autostart TCI on launch](../../features/tci/autostart-tci-on-launch.md)
- [TCI Server overview](../../features/tci/overview.md)
