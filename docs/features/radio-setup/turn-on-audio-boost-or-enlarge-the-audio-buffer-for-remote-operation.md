# Activar el refuerzo de audio o ampliar el búfer de audio para operación remota

Use esta página para habilitar el refuerzo de audio o ajustar el tamaño del búfer de audio cuando opere de forma remota a través de SmartLink o una VPN. El refuerzo de audio aumenta la ganancia en el lado del cliente; un búfer más grande reduce los cortes de audio causados por la fluctuación de la red.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Estos controles no están disponibles sin una conexión activa a la radio.
- Abra la pestaña **Audio** en Radio Setup. Vaya a `Settings > Radio Setup...` y haga clic en la pestaña **Audio**.

## Pasos

1. Vaya a `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Para habilitar el refuerzo de audio, haga clic en **Audio Boost:** para activarlo.
4. Para aumentar el búfer de audio, localice **Audio Buffer:** y establezca el valor en milisegundos. El rango válido es 50–1000 ms. Aumente este valor si escucha cortes o interrupciones a través de una VPN o una conexión SmartLink.
5. Cierre el cuadro de diálogo. Los ajustes se guardan automáticamente.

## Qué hace cada control

| Control | Descripción | Rango válido / predeterminado | Clave de ajuste |
|---|---|---|---|
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente. | Activado / Desactivado | `AudioBoost` |
| **Audio Buffer:** | Establece el tamaño del búfer de audio en el lado del cliente. Los valores más altos absorben mayor fluctuación de red a costa de añadir latencia. | 50–1000 ms | `AudioBuffer` |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | Auto (predeterminado), Uncompressed, Opus | `AudioCompression` |

## Consejos

- Si utiliza un enlace de alta latencia, como una VPN celular o satelital, aumente **Audio Buffer:** de forma incremental (por ejemplo, 200 ms, luego 400 ms) hasta que los cortes cesen. Evite subir más de lo necesario, ya que añade retardo de escucha.
- **Audio Boost:** afecta únicamente la ruta de audio del cliente, no las salidas de línea ni de auriculares de la radio. Ajuste esas salidas por separado usando **Line Out:** y **Headphone:** en la misma pestaña.
- Para la selección de códec en conexiones SmartLink, consulte [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md).

## Solución de problemas

- **Los cortes de audio persisten después de aumentar Audio Buffer:** — Verifique el ajuste del códec. Si **Audio Compression (SmartLink):** está configurado en Uncompressed, intente cambiar a Opus, que tolera mejor la pérdida de paquetes. Consulte [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md).
- **El botón Audio Boost: no tiene efecto** — Confirme que la radio esté conectada. El control está inactivo sin una conexión activa.
- **El cuadro de número Audio Buffer: aparece en gris** — La radio debe estar conectada para que este control acepte cambios.

## Relacionado

- [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Elegir los dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
