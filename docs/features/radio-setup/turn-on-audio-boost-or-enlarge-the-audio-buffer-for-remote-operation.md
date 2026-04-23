# Activar el refuerzo de audio o ampliar el búfer de audio para operación remota

Use esta página para habilitar el refuerzo de audio (Audio Boost) para obtener ganancia adicional en recepción, o para aumentar el tamaño del búfer de audio (Audio Buffer) y reducir interrupciones en conexiones VPN o SmartLink con alta latencia o fluctuación (jitter).

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Estos controles no están disponibles si no hay ningún radio conectado.
- Identifique si su problema es bajo volumen de recepción (use Audio Boost) o audio entrecortado o con interrupciones (aumente Audio Buffer).

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Para habilitar ganancia adicional en recepción, haga clic en **Audio Boost:** para activarlo. El botón muestra **Enabled** cuando está activo. Esta configuración se guarda como `AudioBoost`.
4. Para reducir las interrupciones causadas por jitter, ubique **Audio Buffer:** y establezca el valor en milisegundos. El rango válido es 50–1000 ms. Esta configuración se guarda como `AudioBuffer`.
5. Cierre el diálogo. Los cambios surten efecto de inmediato.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente. Actívelo para aumentar el volumen de recepción. | — | On / Off | `AudioBoost` |
| **Audio Buffer:** | Establece el tamaño del búfer de audio del lado del cliente. Valores más grandes absorben el jitter de red a costa de mayor latencia. | — | 50–1000 ms | `AudioBuffer` |
| **Audio Compression (SmartLink):** | Selecciona el códec de audio utilizado sobre SmartLink o LAN (Auto / Uncompressed / Opus). | Auto | — | `AudioCompression` |

## Consejos

- Aumente **Audio Buffer:** en incrementos de 50–100 ms hasta que las interrupciones desaparezcan. Use el valor más pequeño que proporcione audio limpio para mantener la latencia baja.
- Si el audio ya tiene suficiente volumen y las interrupciones son el problema, aumente **Audio Buffer:** antes de habilitar **Audio Boost:**. Reforzar una señal que ya está recortada (clipping) no ayudará.
- Para la selección de códec sobre SmartLink, consulte [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md).

## Solución de problemas

- **Los controles Audio Boost: y Audio Buffer: aparecen atenuados o no están disponibles** — La pestaña Audio requiere una conexión activa al radio. Conéctese al radio primero y luego vuelva a abrir `Settings > Radio Setup...`.
- **El audio sigue entrecortado después de aumentar Audio Buffer:** — Verifique las condiciones de la red. Un enlace con alto jitter o con pérdida de paquetes puede beneficiarse también al cambiar **Audio Compression (SmartLink):** a **Opus**, que es más resistente a la pérdida de paquetes que el audio sin comprimir.

## Relacionados

- [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Seleccionar dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Habilitar la grabación automática en TX y elegir una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
