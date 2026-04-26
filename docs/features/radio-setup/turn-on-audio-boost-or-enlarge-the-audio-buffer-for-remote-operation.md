# Activar el aumento de audio o ampliar el búfer de audio para operación remota

Use estas configuraciones cuando opere AetherSDR a través de SmartLink, una VPN o cualquier enlace de alta latencia donde el audio recibido sea demasiado bajo o presente interrupciones debido a inestabilidad de la red.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio no es accesible cuando está desconectado.
- Abra `Settings > Radio Setup...` y haga clic en la pestaña **Audio**.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Para aumentar el nivel del audio recibido, haga clic en **Audio Boost:** para activarlo. El botón alterna entre activado y desactivado; no se requiere ningún valor adicional.
4. Para reducir las interrupciones de audio causadas por inestabilidad de la red, localice **Audio Buffer:** y establezca un valor más alto en milisegundos. El rango válido es de 50–1000 ms. Aumente el valor de forma gradual hasta que las interrupciones cesen.
5. Cierre el cuadro de diálogo. La configuración se guarda automáticamente.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Audio Boost:** | Activa ganancia adicional en la ruta de audio del cliente. Actívelo para aumentar el nivel del audio recibido sin ajustar el nivel de salida de la radio. | Desactivado | Activado / Desactivado | `AudioBoost` |
| **Audio Buffer:** | Establece el tamaño del búfer de audio del lado del cliente. Los valores más altos absorben mayor inestabilidad de red, pero añaden latencia. | — | 50–1000 ms | `AudioBuffer` |
| **Audio Compression (SmartLink):** | Selecciona el códec de audio utilizado a través de SmartLink o LAN. Las opciones son Auto, Uncompressed y Opus. | Auto | Auto / Uncompressed / Opus | `AudioCompression` |

## Consejos

- Para enlaces SmartLink o VPN con tiempo de ida y vuelta elevado, comience con un valor de **Audio Buffer:** de aproximadamente 200–300 ms y redúzcalo si la latencia resulta molesta.
- **Audio Boost:** actúa únicamente sobre la ruta del cliente y no modifica la ganancia de la salida de línea ni de los auriculares de la radio.
- Si el audio sigue cortándose después de ampliar el búfer, cambiar **Audio Compression (SmartLink):** de Auto a Opus puede ayudar en conexiones de bajo ancho de banda.

## Solución de problemas

- **Los controles de la pestaña Audio aparecen desactivados o la pestaña no está visible** — AetherSDR no está conectado a una radio. Conéctese primero mediante `Settings > Connect to Radio...` y luego vuelva a abrir `Settings > Radio Setup...`.
- **Audio Boost está activado pero el audio sigue siendo bajo** — Verifique la selección de **PC Audio Devices: Output:** en la misma pestaña; es posible que esté seleccionado el dispositivo de salida incorrecto. Consulte [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md).
- **Las interrupciones persisten después de aumentar Audio Buffer:** — Considere cambiar **Audio Compression (SmartLink):** a Opus, o revise el MTU de la red. Consulte [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md).

## Relacionados

- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
