# Ajustar la velocidad de tecleo CW en PPM

Use el control deslizante Speed en el applet Phone/CW para ajustar la velocidad a la que la radio transmite CW, medida en palabras por minuto (PPM). Esto controla el manipulador interno de la radio y afecta las transmisiones con paleta, llave recta y CWX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El slice activo debe estar en un modo CW. El applet Phone/CW muestra el subpanel CW únicamente cuando el slice activo está en modo CW; de lo contrario, se muestra el panel Phone.
- Abra el applet Phone/CW haciendo clic en el botón P/CW de la barra lateral derecha, o confirme que ya está visible.

## Pasos

1. Verifique que el slice activo esté en un modo CW. El applet cambia automáticamente al subpanel CW cuando el modo CW está activo.
2. Localice el control deslizante **Speed (CW)** en el subpanel CW.
3. Arrastre el control deslizante **Speed (CW)** hacia la izquierda para disminuir las PPM o hacia la derecha para aumentarlas. El rango válido es de 5–100 PPM.

## Qué hace cada control

| Control    | Descripción                                                                 | Valor predeterminado |
|------------|-----------------------------------------------------------------------------|----------------------|
| Speed (CW) | Establece la velocidad de tecleo CW enviada al manipulador interno de la radio. | —                    |

## Sugerencias

- El control deslizante Speed (CW) opera la velocidad del manipulador de la radio. Los cambios surten efecto de inmediato y se aplican a la paleta, la llave recta y cualquier transmisión de texto CWX.
- El botón **Sidetone** y el control deslizante **Sidetone volume** controlan de forma sincronizada tanto el monitor de la radio alimentado por DAX como el sidetone de baja latencia del lado del cliente. Ajustar la velocidad no afecta el tono del sidetone; el tono siempre sigue automáticamente la configuración `cw_pitch` de la radio.
- El indicador **Level** aparece inmediatamente al conectarse cuando la fuente de micrófono está configurada como PC. Cuando la fuente de micrófono es PC, el indicador utiliza medición del lado del cliente y no es suprimido por la configuración `met_in_rx`, incluso cuando no se está transmitiendo.

## Relacionados

- [Ajustar el retardo de break-in CW](set-cw-break-in-delay.md)
- [Habilitar el tecleo con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia del sidetone](change-cw-pitch-sidetone-frequency.md)
