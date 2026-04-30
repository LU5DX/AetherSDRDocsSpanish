# Establecer la velocidad de transmisión CW en PPM

Use el regulador Speed en el applet Phone/CW para ajustar la velocidad a la que la radio transmite CW, medida en palabras por minuto. Esto controla el keyer interno de la radio y afecta las transmisiones por paleta, manipulador recto y CWX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El slice activo debe estar en un modo CW. El applet Phone/CW muestra el subpanel CW solo cuando el slice activo está en modo CW; en caso contrario, se muestra el panel Phone.
- Abra el applet Phone/CW haciendo clic en el botón P/CW en la barra lateral derecha, o confirme que ya está visible.

## Pasos

1. Verifique que el slice activo esté en un modo CW. El applet cambia automáticamente al subpanel CW cuando el modo CW está activo.
2. Localice el regulador **Speed (CW)** en el subpanel CW.
3. Arrastre el regulador **Speed (CW)** hacia la izquierda para disminuir PPM o hacia la derecha para aumentar PPM. El rango válido es 5–100 PPM.

## Qué hace cada control

| Control    | Descripción                                              | Predeterminado |
|------------|----------------------------------------------------------|---------|
| Speed (CW) | Establece la velocidad de transmisión CW enviada al keyer interno de la radio. | —       |

## Consejos

- El regulador Speed (CW) controla la velocidad del keyer de la radio. Los cambios toman efecto inmediatamente y se aplican a la paleta, manipulador recto y cualquier transmisión de texto CWX.
- El interruptor **Sidetone** y el regulador **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el sidetone de baja latencia del lado del cliente de manera sincronizada. Ajustar la velocidad no afecta el tono del sidetone; el tono siempre sigue automáticamente la configuración `cw_pitch` de la radio.
- El medidor **Level** aparece inmediatamente al conectarse cuando la fuente de micrófono está configurada en PC. Cuando la fuente de micrófono es PC, el medidor utiliza mediciones del lado del cliente y no se suprime con la configuración `met_in_rx`, incluso cuando no se está transmitiendo.

## Relacionado

- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Habilitar la transmisión con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia del sidetone](change-cw-pitch-sidetone-frequency.md)
