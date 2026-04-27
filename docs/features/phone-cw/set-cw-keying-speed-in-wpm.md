# Configurar la velocidad de transmisión CW en PPM

Use el control deslizante Speed en el applet Phone/CW para establecer la velocidad a la que el radio transmite CW, medida en palabras por minuto. Esto controla el keyer interno del radio y afecta las transmisiones con paddle, llave recta y CWX.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El slice activo debe estar en un modo CW. El applet Phone/CW muestra el subpanel CW únicamente cuando el slice activo está en modo CW; de lo contrario, se muestra el panel Phone.
- Abra el applet Phone/CW haciendo clic en el botón de bandeja P/CW en la barra lateral derecha, o confirme que ya está visible.

## Pasos

1. Verifique que el slice activo esté en un modo CW. El applet cambia automáticamente al subpanel CW cuando el modo CW está activo.
2. Localice el control deslizante **Speed (CW)** en el subpanel CW.
3. Arrastre el control deslizante **Speed (CW)** hacia la izquierda para disminuir las PPM o hacia la derecha para aumentarlas. El rango válido es de 5–100 WPM.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Speed (CW) | Establece la velocidad de transmisión CW enviada al keyer interno del radio. | — | 5–100 WPM | — |

## Consejos

- El control deslizante Speed (CW) opera la velocidad del keyer del radio. Los cambios surten efecto de inmediato y se aplican al paddle, la llave recta y cualquier transmisión de texto CWX.
- Si utiliza el sidetone local de baja latencia (Local STn), su tono y la velocidad del keyer del radio funcionan de forma independiente: ajustar la velocidad aquí no afecta el tono del sidetone.

## Relacionados

- [Configurar el retardo de break-in CW](set-cw-break-in-delay.md)
- [Habilitar el tecleo con paddle iámbico](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia del sidetone](change-cw-pitch-sidetone-frequency.md)
- [Habilitar el sidetone CW local de baja latencia (Local STn) para uso rápido con paddle, llave recta o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
