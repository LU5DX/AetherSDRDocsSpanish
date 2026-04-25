# Seleccionar Opus o audio sin comprimir para SmartLink

Elija qué códec de audio utiliza AetherSDR al conectarse a su FLEX-8600 a través de SmartLink o una LAN. Opus reduce el ancho de banda a cambio de un pequeño procesamiento de audio; sin comprimir (PCM) preserva el flujo de audio sin procesar. Auto permite que la radio negocie la mejor opción.

## Antes de comenzar

- La radio debe estar conectada. `Settings > Radio Setup...` no está disponible cuando no hay ninguna radio conectada.
- Debe estar usando una conexión SmartLink o LAN. Esta configuración no tiene efecto en el audio USB directo.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice el control **Audio Compression (SmartLink):**.
4. Haga clic en el botón para alternar entre **Auto**, **Uncompressed** y **Opus** hasta que la etiqueta muestre el modo deseado.
5. Cierre el cuadro de diálogo. La configuración se guarda inmediatamente en `AudioCompression`.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Audio Compression (SmartLink):** | Auto | Auto / Uncompressed / Opus | `AudioCompression` | Selecciona el códec de audio utilizado para los flujos de audio de SmartLink y LAN. |
| **Audio Boost:** | — | On / Off | `AudioBoost` | Activa ganancia adicional en la ruta de audio del cliente. |
| **Audio Buffer:** | — | 50–1000 ms | `AudioBuffer` | Aumenta el búfer del lado del cliente para absorber la fluctuación de latencia en conexiones VPN o SmartLink. |
| **Recording: Radio Side / Client Side** | — | Radio Side / Client Side | `RecordMode` | Selecciona si el audio se graba en la radio o en esta PC. |
| **Save to:** | — | Cualquier ruta de carpeta con permisos de escritura | `RecordDir` | Carpeta donde se guardan las grabaciones. |
| **Auto-record on TX** | — | Checked / Unchecked | `AutoRecordTx` | Inicia la grabación automáticamente cada vez que transmite. |
| **Idle timeout:** | — | Segundos | `RecordIdleTimeout` | Detiene una grabación activa después de este número de segundos de silencio. |

## Consejos

- **Auto** es la opción más segura para la mayoría de las configuraciones. La radio y el cliente negocian el códec en el momento de la conexión.
- Si escucha artefactos o interrupciones en un enlace lento o congestionado, pruebe **Opus** explícitamente. Si la calidad de audio importa más que el ancho de banda — por ejemplo, en una LAN gigabit local — elija **Uncompressed**.
- Si su conexión tiene latencia variable (VPN, red celular), aumente **Audio Buffer:** para reducir los cortes de audio. El rango válido es 50–1000 ms.

## Solución de problemas

- **El botón Audio Compression (SmartLink): no aparece o está desactivado** — El cuadro de diálogo requiere una conexión de radio activa. Conéctese a la radio primero y luego abra `Settings > Radio Setup...` y vaya a la pestaña **Audio**.
- **Cambiar el códec no produce ningún efecto audible** — El cambio de códec surte efecto en la siguiente conexión. Desconéctese de la radio y vuelva a conectarse.

## Relacionado

- [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir dispositivos de audio de entrada/salida de la PC](choose-pc-input-output-audio-devices.md)
- [Activar la grabación automática en TX y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Cambiar la MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
