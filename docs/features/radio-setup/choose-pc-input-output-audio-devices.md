# Seleccionar dispositivos de audio de entrada/salida del PC

Esta página explica cómo seleccionar qué tarjeta de sonido o interfaz de audio del PC utiliza AetherSDR para reproducir el audio recibido y capturar la entrada del micrófono. Debe hacerlo cada vez que agregue un nuevo dispositivo de audio o cuando el dispositivo predeterminado del sistema no sea el que desea usar con la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. La pestaña Audio no es accesible cuando no hay ninguna radio conectada.
- Los dispositivos de audio que desea usar ya deben estar reconocidos por el sistema operativo y aparecer en su lista de dispositivos.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice la sección **PC Audio Devices:**. Contiene dos listas desplegables etiquetadas **Input:** y **Output:**.
4. Haga clic en la lista desplegable **Output:** y seleccione el dispositivo que desea que AetherSDR use para la reproducción del audio recibido.
5. Haga clic en la lista desplegable **Input:** y seleccione el dispositivo que desea que AetherSDR use para la entrada del micrófono al transmitir.

Los cambios surten efecto de inmediato. No se requiere ningún paso adicional de confirmación.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango / Valores | Clave de configuración |
|---|---|---|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de audio del sistema usado para la captura del micrófono. | Sistema predeterminado | Todos los dispositivos reportados por el SO | — |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de audio del sistema usado para la reproducción del audio recibido. | Sistema predeterminado | Todos los dispositivos reportados por el SO | — |
| **Audio Boost:** | Aplica ganancia adicional en la ruta de audio del lado del cliente. | Off | On / Off | `AudioBoost` |
| **Audio Buffer:** | Aumenta el búfer de audio del cliente para reducir interrupciones en conexiones VPN o SmartLink. | — | 50–1000 ms | `AudioBuffer` |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | Auto | Auto / Uncompressed / Opus | `AudioCompression` |
| **Recording: Radio Side / Client Side** | Elige si las grabaciones se capturan en la radio o en el PC. | — | Radio Side / Client Side | `RecordMode` |
| **Save to:** | Ruta de la carpeta donde se guardan las grabaciones. | — | Cualquier directorio con permisos de escritura | `RecordDir` |
| **...** | Abre un explorador de carpetas para seleccionar el directorio de grabación. | — | — | — |
| **Auto-record on TX** | Inicia automáticamente la grabación cada vez que transmite. | Off | Checked / Unchecked | `AutoRecordTx` |
| **Idle timeout:** | Segundos de silencio tras los cuales se detiene automáticamente una grabación activa. | — | — | `RecordIdleTimeout` |

## Sugerencias

- Si el dispositivo preferido no aparece en la lista desplegable **Input:** o **Output:**, cierre el cuadro de diálogo, verifique que el SO reconozca el dispositivo y luego vuelva a abrir `Settings > Radio Setup...` para revisar la pestaña **Audio**. La lista de dispositivos se carga cuando se abre la pestaña por primera vez.
- Si el audio recibido suena distorsionado a volumen normal, habilite **Audio Boost:** solo después de confirmar que el nivel de salida del SO no está ya cerca del máximo.
- Cuando opere a través de una conexión VPN o SmartLink con audio entrecortado, aumente **Audio Buffer:** en incrementos pequeños (por ejemplo, 100 ms a la vez) hasta que las interrupciones se detengan.

## Solución de problemas

- **No se escucha audio al recibir aunque haya un dispositivo seleccionado** — Confirme que el dispositivo **Output:** seleccionado no esté silenciado a nivel del SO. Verifique también que el control deslizante **Line Out:** y el control deslizante **Headphone:** de la radio en la misma pestaña Audio no estén en cero ni silenciados.
- **La lista de dispositivos de entrada está vacía o falta un dispositivo** — La lista se construye cuando se muestra la pestaña Audio por primera vez. Cierre y vuelva a abrir `Settings > Radio Setup...` después de conectar o habilitar el dispositivo en el SO.
- **El audio se interrumpe a través de SmartLink** — Aumente **Audio Buffer:** (rango válido 50–1000 ms) y considere cambiar **Audio Compression (SmartLink):** de Auto a Opus.

## Temas relacionados

- [Elegir audio Opus o sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar grabación automática al transmitir y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
