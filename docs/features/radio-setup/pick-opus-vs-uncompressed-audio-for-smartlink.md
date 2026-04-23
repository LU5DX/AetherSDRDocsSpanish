# Elegir Opus o audio sin comprimir para SmartLink

Elija si AetherSDR comprime el audio sobre SmartLink usando Opus, lo envía sin comprimir, o deja que la radio decida automáticamente. La elección correcta depende del ancho de banda disponible y la latencia aceptable.

## Antes de comenzar

- Esté conectado a una radio Flex.
- Si usa SmartLink por internet o una VPN, tenga una estimación del ancho de banda de subida disponible.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Ubique el control **Audio Compression (SmartLink):**. Alterna entre tres estados: **Auto**, **Uncompressed** y **Opus**.
4. Haga clic en el botón hasta que muestre el modo deseado.

La selección se guarda inmediatamente en `AudioCompression`.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Audio Compression (SmartLink):** | Auto | Auto / Uncompressed / Opus | `AudioCompression` | Selecciona el códec de audio utilizado sobre SmartLink. Auto permite que la radio negocie el códec. Uncompressed envía PCM sin procesar. Opus utiliza audio comprimido de baja tasa de bits. |
| **Audio Boost:** | — | On / Off | `AudioBoost` | Activa ganancia adicional en la ruta de audio del cliente. |
| **Audio Buffer:** | — | 50–1000 ms | `AudioBuffer` | Aumenta el búfer de audio del lado del cliente para absorber la fluctuación en conexiones VPN o SmartLink. |
| **Recording: Radio Side / Client Side** | — | Radio Side / Client Side | `RecordMode` | Selecciona si las grabaciones se capturan en la radio o en este cliente. |
| **Save to:** | — | Ruta de carpeta | `RecordDir` | Carpeta donde se guardan las grabaciones. Haga clic en **...** para explorar. |
| **Auto-record on TX** | — | Checked / Unchecked | `AutoRecordTx` | Inicia automáticamente la grabación cada vez que transmite. |
| **Idle timeout:** | — | segundos | `RecordIdleTimeout` | Detiene una grabación después de este número de segundos de silencio. |

## Consejos

- Use **Opus** en conexiones a internet lentas o congestionadas para reducir el ancho de banda a costa de una ligera latencia de codificación adicional.
- Use **Uncompressed** en una LAN local rápida si desea la menor latencia de audio posible y dispone de ancho de banda suficiente.
- Si no está seguro de cuál elegir, deje la configuración en **Auto** y permita que la radio negocie.
- Si el audio se interrumpe de forma intermitente sobre una VPN, aumente **Audio Buffer:** antes de cambiar el modo de compresión.

## Solución de problemas

- **El audio tartamudea o se corta sobre SmartLink** — Intente aumentar **Audio Buffer:** hacia 200–500 ms para absorber la fluctuación de red. Si el problema persiste, cambie **Audio Compression (SmartLink):** a **Opus** para reducir la demanda de ancho de banda.
- **El audio suena distorsionado o procesado** — Si cambió a **Opus** y la calidad es inaceptable, establezca **Audio Compression (SmartLink):** en **Uncompressed** y asegúrese de que su enlace tenga ancho de banda suficiente.

## Temas relacionados

- [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Activar la grabación automática en TX y elegir una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
