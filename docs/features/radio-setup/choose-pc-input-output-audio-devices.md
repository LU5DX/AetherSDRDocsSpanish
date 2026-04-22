# Seleccionar dispositivos de audio de entrada/salida del PC

Seleccione qué tarjeta de sonido o interfaz de audio del PC utilizará AetherSDR para enrutar el audio recibido a sus altavoces o auriculares, y para capturar su micrófono durante la transmisión. Debe realizar este proceso una vez después de la instalación, y nuevamente cada vez que cambie su hardware de audio.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio solo está disponible cuando hay una conexión de radio activa.
- Conozca el nombre de los dispositivos de entrada y salida de audio que desea utilizar (tal como los reporta su sistema operativo).

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Audio**.
3. En **PC Audio Devices:**, ubique el menú desplegable **Input:**. Seleccione el dispositivo que desea que AetherSDR utilice para la entrada de micrófono o línea.
4. Ubique el menú desplegable **Output:** inmediatamente debajo. Seleccione el dispositivo que desea que AetherSDR utilice para la reproducción del audio recibido.
5. Haga clic en **Close** para guardar y cerrar el diálogo.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango / valores válidos | Clave de configuración |
|---|---|---|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del host (micrófono o entrada de línea) utilizado para el audio de transmisión. | Sistema predeterminado | Todos los dispositivos enumerados por el SO | — |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del host (altavoces o auriculares) utilizado para el audio recibido. | Sistema predeterminado | Todos los dispositivos enumerados por el SO | — |
| **Audio Boost:** | Activa ganancia adicional en la ruta de audio del cliente. | Off | On / Off | `AudioBoost` |
| **Audio Buffer:** | Aumenta el búfer de reproducción para absorber la fluctuación en conexiones VPN o SmartLink. | — | 50–1000 ms | `AudioBuffer` |
| **Audio Compression (SmartLink):** | Selecciona el códec de audio utilizado a través de SmartLink o LAN. Tres posiciones: Auto, Uncompressed, Opus. | Auto | Auto / Uncompressed / Opus | `AudioCompression` |

## Consejos

- Si no escucha audio después de seleccionar un dispositivo, verifique que el dispositivo de salida seleccionado no esté silenciado en el mezclador de su sistema operativo.
- Para operación remota o por VPN, aumentar el valor de **Audio Buffer:** reduce las interrupciones a costa de mayor latencia.
- **Audio Boost:** es útil cuando el nivel de audio recibido es bajo después de ajustar el volumen del SO y los controles deslizantes **Line Out:** o **Headphone:** de la radio.

## Solución de problemas

- **Los nombres de dispositivo no aparecen en los menús desplegables** — Las listas se llenan cuando se carga la pestaña Audio. Cierre y vuelva a abrir Radio Setup después de conectar o habilitar un nuevo dispositivo de audio en el sistema operativo.
- **El audio se interrumpe bajo SmartLink** — Aumente **Audio Buffer:** (`AudioBuffer`) hacia 1000 ms y cambie **Audio Compression (SmartLink):** a Opus, que es más resistente a la pérdida de paquetes.
- **No se recibe audio transmitido en el otro extremo** — Verifique que el dispositivo correcto esté seleccionado en **Input:** y que el sistema operativo haya concedido a AetherSDR acceso al micrófono.

## Relacionados

- [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y seleccionar una carpeta de guardado](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
