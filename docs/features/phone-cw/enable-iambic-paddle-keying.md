# Habilitar el keying de paleta iámbica

Habilite el keyer iámbico integrado del radio para que una paleta de dos palancas conectada al FLEX-8600 pueda enviar CW en modo iámbico. Esto le permite establecer la velocidad de keying y el comportamiento de break-in desde AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al sub-panel CW cuando un slice CW está activo.
- Una paleta de dos palancas debe estar conectada físicamente al jack de key del FLEX-8600.

## Pasos

1. Haga clic en el botón **P/CW** de la bandeja en la barra lateral derecha para abrir el applet Phone/CW. Si el applet ya está visible, omita este paso.
2. Confirme que se muestra el sub-panel CW. Si el slice activo está en modo CW, el applet muestra controles CW incluyendo **Iambic**, **Speed (CW)**, **Delay (CW)** y **Breakin**.
3. Haga clic en **Iambic** para habilitar el keyer de paleta iámbica. El botón se resalta cuando está activo.

## Qué hace cada control

| Control         | Descripción                                      | Por defecto |
|-----------------|--------------------------------------------------|---------|
| **Iambic**      | Activa/desactiva el keyer de paleta iámbica del radio.    | —       |
| **Speed (CW)**  | Establece la velocidad de keying CW.                            | —       |
| **Delay (CW)**  | Establece el retardo de break-in CW.                          | —       |
| **Breakin**     | Activa/desactiva break-in completo (QSK).                     | —       |
| **Pitch < / >** | Ajusta el tono CW y la frecuencia de decodificación en 10 Hz. | 600 Hz  |

## Consejos

- Para feedback de sidetone de baja latencia al usar una paleta, habilite **Sidetone** en el sub-panel CW. El botón único **Sidetone** y el deslizador **Sidetone volume** controlan en conjunto el monitor DAX-fed del radio y el sidetone de baja latencia del lado del cliente (latencia aproximada de 10 ms). El pitch y el pan siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio. En Windows, el stream de sidetone ahora se inicia inmediatamente al conectar (v0.9.3, fix #2105). Consulte [Escuchar un monitor de sidetone TX](listen-to-a-tx-sidetone-monitor.md).
- Ajuste **Speed (CW)** antes de habilitar **Iambic** para evitar enviar a una velocidad inesperada. Consulte [Establecer la velocidad de keying CW en WPM](set-cw-keying-speed-in-wpm.md).
- Si desea operación QSK completa, habilite también **Breakin**. Para establecer un tiempo de espera en su lugar, deshabilite **Breakin** y establezca **Delay (CW)** en un valor distinto de cero. Consulte [Establecer el retardo de break-in CW](set-cw-break-in-delay.md).

## Resolución de problemas

- **El sub-panel CW no es visible, solo aparecen controles de Phone** — El slice activo no está en modo CW. Cambie el modo del slice a CW o CW-USB/CW-LSB en el radio o en AetherSDR; el applet cambiará automáticamente.
- **El botón Iambic está presente pero la paleta no envía keys** — Verifique que la paleta está conectada al jack de key correcto en el FLEX-8600. El keyer iámbico es una función del lado del radio; AetherSDR envía el comando de habilitación pero el keying físico depende de la conexión de hardware.
- **El medidor Level no aparece después de conectar con la fuente de micrófono establecida en PC** — En v0.9.3 el medidor Level aparece inmediatamente al conectar cuando la fuente de micrófono es PC (#2086). Si falta el medidor, confirme que la fuente de micrófono está establecida en **PC** en el selector **Mic source** y que está ejecutando v0.9.3 o posterior. Cuando la fuente es PC, el medidor usa metering del lado del cliente y no se suprime por el ajuste `met_in_rx`.

## Relacionado

- [Establecer la velocidad de keying CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Cambiar el pitch CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone TX](listen-to-a-tx-sidetone-monitor.md)
