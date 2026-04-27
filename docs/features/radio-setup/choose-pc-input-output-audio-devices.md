# Seleccionar dispositivos de audio de entrada/salida del PC

Esta página explica cómo seleccionar qué dispositivos de audio del PC utiliza AetherSDR para la salida de audio de recepción del radio y la entrada de micrófono. Es necesario hacer esto la primera vez que configure AetherSDR o cuando cambie auriculares, altavoces o interfaces de audio.

## Antes de comenzar

- El radio debe estar conectado. Los controles de Radio Setup no están disponibles sin una conexión de radio activa.
- Conozca qué dispositivos de entrada y salida de audio expone su PC (revise la configuración de audio del sistema operativo si no está seguro).

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Audio**.
3. En **PC Audio Devices:**, haga clic en el menú desplegable **Input:** y seleccione el dispositivo que desea usar para el micrófono o la entrada de audio.
4. Haga clic en el menú desplegable **Output:** y seleccione el dispositivo que desea usar para la reproducción de audio de recepción.
5. Cierre el diálogo. Las selecciones surten efecto de inmediato.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del sistema (micrófono, interfaz de audio, etc.). | Predeterminado del sistema | Dispositivos de entrada disponibles | — |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del sistema (altavoces, auriculares, interfaz de audio, etc.). | Predeterminado del sistema | Dispositivos de salida disponibles | — |
| **Audio Boost:** | Aplica ganancia adicional en la ruta de audio del cliente. | Off | On / Off | `AudioBoost` |
| **Audio Buffer:** | Aumenta el búfer de audio del cliente para absorber el jitter en conexiones VPN o SmartLink. | — | 50–1000 ms | `AudioBuffer` |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | Auto | Auto / Uncompressed / Opus | `AudioCompression` |
| **Recording: Radio Side / Client Side** | Selecciona si las grabaciones se capturan en el radio o en el cliente. | — | Radio Side / Client Side | `RecordMode` |
| **Save to:** | Carpeta donde se guardan las grabaciones. | — | Cualquier ruta válida | `RecordDir` |
| **...** | Abre un explorador de carpetas para seleccionar el directorio de grabación. | — | — | — |
| **Auto-record on TX** | Inicia automáticamente la grabación al transmitir. | Off | Checked / Unchecked | `AutoRecordTx` |
| **Idle timeout:** | Segundos de silencio tras los cuales se detiene automáticamente una grabación activa. | — | — | `RecordIdleTimeout` |

## Consejos

- Los menús desplegables Input y Output muestran únicamente los dispositivos que el sistema operativo expone en ese momento. Si falta un dispositivo, conéctelo y vuelva a abrir la pestaña Audio — la enumeración de dispositivos ocurre cuando la pestaña se muestra por primera vez.
- Si el audio de recepción suena demasiado bajo con el dispositivo de salida elegido, active **Audio Boost:** antes de aumentar el volumen del sistema operativo.
- En conexiones VPN o SmartLink, aumente **Audio Buffer:** para reducir cortes. Valores superiores a 200 ms añaden un retardo perceptible.

## Solución de problemas

- **No aparecen dispositivos de audio en los menús desplegables** — La pestaña Audio enumera los dispositivos al cargarse por primera vez. Cierre Radio Setup, verifique que el sistema operativo reconoce el dispositivo y vuelva a abrir `Settings > Radio Setup...` y haga clic en la pestaña Audio.
- **El audio de recepción se reproduce en el dispositivo incorrecto** — Es posible que el menú desplegable Output aún esté configurado con un dispositivo seleccionado anteriormente. Abra la pestaña Audio y vuelva a seleccionar la salida correcta.
- **El radio no escucha el micrófono** — Confirme que el dispositivo correcto está seleccionado en el menú desplegable **Input:** y que el sistema operativo no ha silenciado ni bloqueado el acceso a ese dispositivo.

## Temas relacionados

- [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar audio boost o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Activar la grabación automática al transmitir y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
