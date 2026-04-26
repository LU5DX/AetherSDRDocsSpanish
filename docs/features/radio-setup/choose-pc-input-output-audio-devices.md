# Elegir dispositivos de audio de entrada/salida del PC

Seleccione qué dispositivos de audio de entrada y salida del PC utiliza AetherSDR para enrutar el audio recibido a sus altavoces o auriculares, y para capturar el audio del micrófono durante la transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado a un FLEX-8600. La pestaña Audio no está disponible sin una conexión al radio.
- Los dispositivos de audio que desea utilizar deben ser reconocidos por su sistema operativo antes de abrir este diálogo.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **PC Audio Devices:**, haga clic en el menú desplegable **Input:** y seleccione el micrófono o dispositivo de entrada de línea que desea usar para el audio de transmisión.
4. Haga clic en el menú desplegable **Output:** y seleccione el altavoz, auricular o dispositivo de salida de línea que desea usar para el audio recibido.
5. Haga clic en **Close**.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango / Opciones | Clave de configuración |
|---|---|---|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del PC host (micrófono o entrada de línea) usado para el audio de TX. | Sistema predeterminado | Todos los dispositivos reportados por el SO | — |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del PC host (altavoces o auriculares) usado para el audio de RX. | Sistema predeterminado | Todos los dispositivos reportados por el SO | — |
| **Audio Boost:** | Aplica ganancia adicional en la ruta de audio del cliente. | Off | On / Off | `AudioBoost` |
| **Audio Buffer:** | Aumenta el búfer de audio para reducir cortes durante conexiones VPN o SmartLink. | — | 50–1000 ms | `AudioBuffer` |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | Auto | Auto / Uncompressed / Opus | `AudioCompression` |
| **Recording: Radio Side / Client Side** | Selecciona si las grabaciones se capturan en el radio o en este PC. | — | Radio Side / Client Side | `RecordMode` |
| **Save to:** | Carpeta donde se guardan las grabaciones. | — | Cualquier ruta con permisos de escritura | `RecordDir` |
| **...** | Abre un explorador de carpetas para elegir el directorio de grabación. | — | — | — |
| **Auto-record on TX** | Inicia la grabación automáticamente cada vez que transmite. | Off | On / Off | `AutoRecordTx` |
| **Idle timeout:** | Segundos de silencio tras los cuales se detiene una grabación automática. | — | — | `RecordIdleTimeout` |
| **Line Out:** | Ajusta la ganancia de la salida de línea del radio. | — | — | — |
| **Mute (Line Out)** | Silencia la salida de línea del radio. | — | — | — |
| **Headphone:** | Ajusta la ganancia de los auriculares del radio. | — | — | — |
| **Mute (Headphone)** | Silencia la salida de auriculares del radio. | — | — | — |

## Consejos

- Si su dispositivo no aparece en el menú desplegable **Input:** u **Output:**, cierre el diálogo, verifique que el SO reconoce el dispositivo y vuelva a abrir `Settings > Radio Setup...` para regresar a la pestaña **Audio**. La enumeración de dispositivos ocurre cuando la pestaña se abre por primera vez.
- Para operación remota o por VPN, aumente **Audio Buffer:** para reducir los cortes, y considere configurar **Audio Compression (SmartLink):** en Opus. Consulte [Activar el realce de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md) y [Elegir entre Opus y audio sin compresión para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md).

## Solución de problemas

- **Un dispositivo aparece en el SO pero no en el menú desplegable** — Cierre el diálogo Radio Setup y vuelva a abrirlo. La lista de dispositivos se carga cuando se construye la pestaña Audio; los dispositivos conectados después de abrir la pestaña no aparecerán hasta que se cierre y vuelva a abrir el diálogo.
- **El audio se reproduce pero suena distorsionado o recortado** — Active **Audio Boost:** solo si la señal recibida es demasiado débil. Si ya está activado, desactívelo para reducir la distorsión.
- **Cortes durante la operación remota** — Aumente **Audio Buffer:** hacia 1000 ms y cambie **Audio Compression (SmartLink):** a Opus.

## Relacionados

- [Activar el realce de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre Opus y audio sin compresión para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar la grabación automática en TX y elegir una carpeta de guardado](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
