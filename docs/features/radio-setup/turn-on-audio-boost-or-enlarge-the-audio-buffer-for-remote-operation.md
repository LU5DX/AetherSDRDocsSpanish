# Activar el aumento de audio o ampliar el búfer de audio para operación remota

Use estos ajustes para compensar el bajo volumen de recepción o las interrupciones de audio al operar AetherSDR a través de una conexión VPN o SmartLink. Audio Boost añade ganancia adicional en la ruta de audio del cliente; un Audio Buffer mayor absorbe el jitter de red a costa de una mayor latencia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Estos controles no están disponibles cuando no hay ningún radio conectado.
- Abra `Settings > Radio Setup...` y seleccione la pestaña **Audio** antes de seguir los pasos a continuación.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Para aumentar el volumen de recepción, haga clic en **Audio Boost:** para activarlo. El botón muestra su estado activo cuando está habilitado.
4. Para reducir las interrupciones o cortes de audio, haga clic en el control giratorio **Audio Buffer:** e ingrese un valor entre 50 y 1000 ms. Los valores más altos añaden más almacenamiento en búfer a costa de mayor latencia.
5. Cierre el diálogo. Los ajustes surten efecto de inmediato.

## Qué hace cada control

| Control | Función | Rango válido | Clave de ajuste |
|---|---|---|---|
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente. | On / Off | `AudioBoost` |
| **Audio Buffer:** | Establece el búfer de audio del lado del cliente para absorber el jitter de red. Auméntelo al usar conexiones VPN o SmartLink con latencia inestable. | 50–1000 ms | `AudioBuffer` |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | Auto \| Uncompressed \| Opus | `AudioCompression` |

## Consejos

- Comience con un aumento moderado del búfer (200–300 ms) antes de subir más. Los valores muy grandes hacen que el audio se sienta notablemente lento durante los QSOs.
- Si la calidad de audio es deficiente a través de SmartLink, revise también el ajuste del códec (**Audio Compression (SmartLink):**). Cambiar de Auto a Opus puede reducir el ancho de banda y mejorar la estabilidad en conexiones lentas.

## Solución de problemas

- **Los controles Audio Boost y Audio Buffer están atenuados o no aparecen** — Estos controles se encuentran en la pestaña **Audio**. Confirme que ha seleccionado esa pestaña y no otra, como **RX** o **Phone/CW**.
- **Aumentar el Audio Buffer no tiene efecto sobre los cortes** — El búfer absorbe el jitter, pero no puede compensar la pérdida sostenida de paquetes. Verifique la ruta de red; consulte también [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md).

## Relacionado

- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Seleccionar dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
