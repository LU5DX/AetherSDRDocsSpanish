# Seleccionar audio Opus o sin comprimir para SmartLink

Elija si AetherSDR comprime el flujo de audio a Opus, lo envía sin comprimir, o deja que el radio decida automáticamente al usar SmartLink o una conexión LAN. La opción correcta depende del ancho de banda disponible y la latencia aceptable.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Audio no está disponible cuando está desconectado.
- Abra `Settings > Radio Setup...` y haga clic en la pestaña **Audio**.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice el control **Audio Compression (SmartLink):**. Este alterna entre tres estados: **Auto**, **Uncompressed** y **Opus**.
4. Haga clic en el botón repetidamente hasta que muestre el modo deseado.
5. Cierre el diálogo. El ajuste surte efecto inmediatamente y se guarda de forma automática en `AudioCompression`.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave de ajuste | Comportamiento |
|---|---|---|---|---|
| **Audio Compression (SmartLink):** | Auto | Auto / Uncompressed / Opus | `AudioCompression` | Selecciona el códec de audio para el flujo de audio SmartLink o LAN. **Auto** permite que el radio negocie. **Uncompressed** envía PCM sin procesar — menor latencia, mayor ancho de banda. **Opus** comprime el flujo — menor ancho de banda, latencia ligeramente mayor. |
| **Audio Boost:** | — | On / Off | `AudioBoost` | Activa ganancia adicional en la ruta de audio del cliente. |
| **Audio Buffer:** | — | 50–1000 ms | `AudioBuffer` | Incrementa el búfer de reproducción para absorber la fluctuación en conexiones VPN o SmartLink. |
| **Recording: Radio Side / Client Side** | — | Radio Side / Client Side | `RecordMode` | Selecciona si las grabaciones se capturan en el radio o en la PC cliente. |
| **Save to:** | — | ruta de carpeta | `RecordDir` | Carpeta donde se escriben las grabaciones. Haga clic en **...** para explorar. |
| **Auto-record on TX** | — | marcado / desmarcado | `AutoRecordTx` | Inicia la grabación automáticamente cuando el radio transmite. |
| **Idle timeout:** | — | segundos | `RecordIdleTimeout` | Detiene una grabación automática después de este número de segundos de silencio. |

## Consejos

- Use **Opus** en conexiones lentas o con datos limitados, como enlaces celulares o VPN donde el ancho de banda es reducido.
- Use **Uncompressed** en una LAN gigabit local o cuando necesite la menor latencia de audio posible.
- Si no está seguro, deje el ajuste en **Auto** y permita que el radio elija según el tipo de conexión.
- Si el audio de SmartLink se escucha entrecortado, aumente el valor de **Audio Buffer:** antes de cambiar de códec. El rango válido es 50–1000 ms.

## Solución de problemas

- **El control Audio Compression aparece atenuado o no está visible** — El radio debe estar conectado antes de que la pestaña Audio se rellene. Verifique la conexión y vuelva a abrir `Settings > Radio Setup...`.
- **Audio entrecortado después de cambiar a Uncompressed** — Es posible que el enlace no tenga ancho de banda suficiente para PCM sin comprimir. Cambie a **Opus** o aumente **Audio Buffer:**.
- **No hay diferencia audible después de cambiar el ajuste** — El cambio se aplica a los nuevos flujos de audio. Si el audio ya estaba fluyendo, desconéctese del radio y vuelva a conectarse para forzar la renegociación del códec.

## Temas relacionados

- [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Seleccionar dispositivos de audio de entrada/salida de la PC](choose-pc-input-output-audio-devices.md)
- [Habilitar la grabación automática al transmitir y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Cambiar el MTU de red para configuraciones VPN o remotas](change-network-mtu-for-vpn-remote-setups.md)
