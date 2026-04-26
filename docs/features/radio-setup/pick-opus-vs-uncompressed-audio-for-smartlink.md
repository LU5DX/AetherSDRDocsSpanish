# Elegir Opus o audio sin comprimir para SmartLink

Elija cómo comprime AetherSDR el audio en una conexión SmartLink o LAN. Seleccionar el códec adecuado reduce el ancho de banda en enlaces lentos o con alta latencia, o preserva la calidad de audio completa en redes locales rápidas.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña **Audio** no es accesible sin una conexión activa.
- Abra `Settings > Radio Setup...` y haga clic en la pestaña **Audio**.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice el control **Audio Compression (SmartLink):**.
4. Haga clic en el botón para avanzar al modo deseado: **Auto**, **Uncompressed** u **Opus**.
5. Cierre el diálogo. La configuración se guarda inmediatamente en `AudioCompression`.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Audio Compression (SmartLink):** | Auto | Auto / Uncompressed / Opus | `AudioCompression` | Selecciona el códec de audio utilizado a través de SmartLink o LAN. Auto permite que el radio negocie el códec. Uncompressed envía audio sin procesar. Opus aplica compresión con pérdida para reducir el ancho de banda. |
| **Audio Boost:** | — | On / Off | `AudioBoost` | Habilita ganancia adicional en la ruta de audio del cliente. |
| **Audio Buffer:** | — | 50–1000 ms | `AudioBuffer` | Aumenta el búfer del lado del cliente para absorber la fluctuación en conexiones VPN o SmartLink. |
| **Recording: Radio Side / Client Side** | — | Radio Side / Client Side | `RecordMode` | Elige si las grabaciones se capturan en el radio o en el PC cliente. |
| **Save to:** | — | Ruta de carpeta | `RecordDir` | Establece la carpeta donde se guardan las grabaciones. |
| **Auto-record on TX** | — | Checked / Unchecked | `AutoRecordTx` | Inicia automáticamente la grabación cada vez que el radio transmite. |
| **Idle timeout:** | — | Segundos | `RecordIdleTimeout` | Detiene una grabación después de este número de segundos de silencio. |

## Consejos

- Use **Opus** al conectarse a través de Internet o una VPN donde el ancho de banda es limitado. Opus reduce significativamente la tasa de datos de audio en comparación con el audio sin comprimir.
- Use **Uncompressed** en una red local rápida cuando la fidelidad de audio es la prioridad y el ancho de banda no es una preocupación.
- **Auto** es adecuado para la mayoría de los usuarios y permite que el firmware del radio elija el códec según el tipo de conexión.
- Si el audio se interrumpe o se corta en una conexión remota, aumente **Audio Buffer:** antes de cambiar el códec. El rango válido es 50–1000 ms.

## Solución de problemas

- **El control Audio Compression aparece deshabilitado o la pestaña Audio no aparece** — El radio no está conectado. Conéctese al radio primero y luego vuelva a abrir `Settings > Radio Setup...`.
- **El audio está entrecortado después de cambiar a Uncompressed** — El enlace no tiene suficiente ancho de banda para el audio sin comprimir. Cambie a **Opus** o aumente **Audio Buffer:**.
- **Opus está seleccionado pero la calidad de audio es deficiente** — Aumente **Audio Buffer:** para compensar la fluctuación, o verifique la ruta de red en busca de pérdida de paquetes.

## Temas relacionados

- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir los dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Habilitar la grabación automática al transmitir y elegir una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
