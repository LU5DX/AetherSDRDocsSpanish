# Seleccionar Opus o audio sin comprimir para SmartLink

Elija el códec de audio que AetherSDR utiliza al conectarse a través de SmartLink o una LAN. Opus reduce el ancho de banda a costa de una ligera compresión; sin comprimir transmite el audio sin procesamiento de códec. Auto permite que el radio negocie la mejor opción.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Audio en Radio Setup no está disponible sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice el control **Audio Compression (SmartLink):**. Alterna entre tres estados: **Auto**, **Uncompressed** y **Opus**.
4. Haga clic en el botón hasta que muestre el modo deseado.
5. Cierre el diálogo. La configuración se guarda automáticamente en `AudioCompression`.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Audio Compression (SmartLink):** | Auto | Auto / Uncompressed / Opus | `AudioCompression` | Selecciona el códec de audio para las transmisiones de audio SmartLink y LAN. |
| **Audio Boost:** | — | On / Off | `AudioBoost` | Activa ganancia adicional en la ruta de audio del cliente. |
| **Audio Buffer:** | — | 50–1000 ms | `AudioBuffer` | Aumenta el búfer de reproducción para absorber la fluctuación de VPN o SmartLink. |
| **Recording: Radio Side / Client Side** | — | Radio Side / Client Side | `RecordMode` | Elige si las grabaciones se capturan en el radio o en el cliente. |
| **Save to:** | — | Ruta de carpeta | `RecordDir` | Carpeta donde se guardan las grabaciones. |
| **Auto-record on TX** | — | On / Off | `AutoRecordTx` | Inicia la grabación automáticamente al transmitir. |
| **Idle timeout:** | — | Segundos | `RecordIdleTimeout` | Detiene una grabación después de esta cantidad de segundos de silencio. |

## Consejos

- En una red local rápida, **Uncompressed** ofrece la menor carga de procesamiento. En un enlace congestionado o de alta latencia, **Opus** reduce la tasa de datos.
- Si el audio se interrumpe durante la operación remota, aumente **Audio Buffer:** además de seleccionar **Opus**. El rango válido es 50–1000 ms.

## Relacionado

- [Activar la mejora de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir los dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Activar la grabación automática al transmitir y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Cambiar la MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
