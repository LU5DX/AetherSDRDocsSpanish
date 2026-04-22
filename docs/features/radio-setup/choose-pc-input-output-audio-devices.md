# Seleccionar dispositivos de audio de entrada/salida del PC

Seleccione qué dispositivo de audio del PC recibe el audio recibido por la radio y qué dispositivo captura la entrada del micrófono. Ambos se configuran en la pestaña Audio de Radio Setup.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio no es accesible sin una conexión de radio activa.
- Asegúrese de que los dispositivos de audio del PC (auriculares, micrófono, altavoces) sean reconocidos por el sistema operativo antes de abrir este diálogo.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **PC Audio Devices:**, haga clic en el menú desplegable **Input:** y seleccione el dispositivo que capturará su audio de transmisión (micrófono o auriculares).
4. Haga clic en el menú desplegable **Output:** y seleccione el dispositivo que reproducirá el audio recibido (altavoces o auriculares).
5. Cierre el diálogo. AetherSDR aplica la selección de inmediato.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del PC (micrófono/auriculares) utilizado para el audio de transmisión. | Predeterminado del sistema | Dispositivos disponibles | — |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del PC (altavoces/auriculares) utilizado para la reproducción del audio recibido. | Predeterminado del sistema | Dispositivos disponibles | — |
| **Audio Boost:** | Aplica ganancia adicional a la ruta de audio del cliente. | Off | On / Off | `AudioBoost` |
| **Audio Buffer:** | Establece el tamaño del búfer de audio en el lado del cliente. Auméntelo para reducir interrupciones en VPN o SmartLink. | — | 50–1000 ms | `AudioBuffer` |
| **Audio Compression (SmartLink):** | Selecciona el códec de audio utilizado sobre SmartLink o LAN. Tres opciones: Auto, Uncompressed, Opus. | Auto | Auto / Uncompressed / Opus | `AudioCompression` |
| **Recording: Radio Side / Client Side** | Determina si las grabaciones se capturan en la radio o en el cliente del PC. | — | Radio Side / Client Side | `RecordMode` |
| **Save to:** | Ruta de la carpeta donde se guardan las grabaciones. Haga clic en **...** para explorar. | — | Cualquier ruta con permisos de escritura | `RecordDir` |
| **Auto-record on TX** | Inicia la grabación automáticamente cada vez que transmite. | Off | On / Off | `AutoRecordTx` |
| **Idle timeout:** | Segundos de silencio tras los cuales se detiene una grabación automática. | — | — | `RecordIdleTimeout` |

## Sugerencias

- Si sus auriculares aparecen en los menús desplegables Input y Output, selecciónelos en ambos para mantener el audio de transmisión y recepción en el mismo dispositivo.
- Si el audio se interrumpe durante sesiones de SmartLink o VPN, aumente **Audio Buffer:** antes de cambiar de códec. El rango válido es 50–1000 ms.
- **Audio Boost:** agrega ganancia solo en la ruta del cliente. Si el nivel de audio en el lado de la radio ya es suficiente, déjelo desactivado para evitar saturación.

## Solución de problemas

- **No aparecen dispositivos en el menú desplegable Input u Output** — La pestaña Audio pospone la detección de hardware hasta que se abre por primera vez. Si los dispositivos siguen sin aparecer, confirme que el sistema operativo reconoce el dispositivo (verifique la configuración de sonido del sistema) y luego cierre y vuelva a abrir Radio Setup.
- **El audio de salida está en silencio después de seleccionar un dispositivo** — Verifique que el dispositivo de salida seleccionado no esté silenciado en el mezclador del sistema operativo. Compruebe también los controles deslizantes **Line Out:** y **Headphone:** en la misma pestaña Audio, y confirme que ninguno esté silenciado mediante el botón **Mute** correspondiente.
- **El dispositivo de entrada no produce nivel durante TX** — Confirme que el dispositivo de entrada correcto esté seleccionado. En Linux (PipeWire/PulseAudio), el dispositivo no debe estar siendo usado de forma exclusiva por otra aplicación.

## Temas relacionados

- [Activar Audio Boost o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre Opus y audio sin compresión para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar la grabación automática en TX y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
