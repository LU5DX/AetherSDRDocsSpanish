# Seleccionar Opus o audio sin comprimir para SmartLink

Seleccione el códec de audio que AetherSDR utiliza en conexiones SmartLink o LAN. Opus reduce el ancho de banda a costa de una pequeña cantidad de compresión; el PCM sin comprimir preserva la fidelidad total cuando el ancho de banda lo permite. Auto deja que el radio elija.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Audio no es accesible sin una conexión activa.
- Abra `Settings > Radio Setup...` y haga clic en la pestaña **Audio**.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Audio Compression (SmartLink):**, haga clic en **Auto**, **Uncompressed** u **Opus** para seleccionar el códec.
   - **Auto** — el radio negocia el códec automáticamente (valor predeterminado).
   - **Uncompressed** — envía audio PCM sin procesar; utiliza más ancho de banda.
   - **Opus** — envía audio codificado con Opus; menor ancho de banda, leve compresión.
4. Cierre el cuadro de diálogo. La configuración surte efecto de inmediato y se guarda.

## Qué hace cada control

| Control | Predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|
| **Audio Compression (SmartLink):** Auto / Uncompressed / Opus | Auto | Auto, Uncompressed, Opus | `AudioCompression` |
| **Audio Boost:** | — | Enabled / Disabled | `AudioBoost` |
| **Audio Buffer:** | — | 50–1000 ms | `AudioBuffer` |
| **Recording:** Radio Side / Client Side | — | Radio Side, Client Side | `RecordMode` |
| **Save to:** | — | Ruta de carpeta | `RecordDir` |
| **Auto-record on TX** | — | Checked / Unchecked | `AutoRecordTx` |
| **Idle timeout:** | — | segundos | `RecordIdleTimeout` |

## Consejos

- En una LAN local rápida, **Uncompressed** evita cualquier artefacto del códec y es la mejor opción para escucha crítica o decodificación de modos digitales.
- En un enlace lento o congestionado (VPN, SmartLink celular), **Opus** reduce los cortes de audio. Combínelo con un valor mayor de **Audio Buffer:** (50–1000 ms) para absorber el jitter.
- Si el audio suena delgado o bajo en SmartLink, pruebe activar **Audio Boost:** junto con Opus.

## Solución de problemas

- **Los botones de Audio Compression aparecen atenuados o no están visibles** — la pestaña Audio solo se construye después de hacer clic en ella, y únicamente cuando hay un radio conectado. Verifique la conexión y haga clic en la pestaña Audio nuevamente.
- **La calidad de audio es deficiente incluso con Uncompressed seleccionado** — verifique el ancho de banda y la latencia de la red. Considere aumentar **Audio Buffer:** para reducir los cortes por falta de datos. Consulte [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md).

## Relacionados

- [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir los dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Activar la grabación automática en TX y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
