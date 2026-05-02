# Activar el manipulador de paleta iámbica

Active el manipulador iámbico integrado del radio para que una paleta de doble palanca conectada al FLEX-8600 transmita CW en modo iámbico. Esto permite configurar la velocidad de manipulación y el comportamiento de break-in desde AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al subpanel de CW cuando hay un slice CW activo.
- Una paleta de doble palanca debe estar conectada físicamente al conector de llave del FLEX-8600.

## Pasos

1. Haga clic en el botón **P/CW** de la bandeja en la barra lateral derecha para abrir el applet Phone/CW. Si el applet ya está visible, omita este paso.
2. Confirme que el subpanel de CW está visible. Si el slice activo está en modo CW, el applet muestra los controles de CW, incluidos **Iambic**, **Speed (CW)**, **Delay (CW)** y **Breakin**.
3. Haga clic en **Iambic** para activar el manipulador de paleta iámbica. El botón se resalta cuando está activo.

## Qué hace cada control

| Control         | Descripción                                                        | Predeterminado |
|-----------------|--------------------------------------------------------------------|----------------|
| **Iambic**      | Activa o desactiva el manipulador de paleta iámbica en el radio.   | —              |
| **Speed (CW)**  | Establece la velocidad de manipulación CW.                         | —              |
| **Delay (CW)**  | Establece el retardo de break-in CW.                               | —              |
| **Breakin**     | Activa o desactiva el break-in completo (QSK).                     | —              |
| **Pitch < / >** | Ajusta el tono del sidetone y la frecuencia de decodificación CW en pasos de 10 Hz. | 600 Hz |

## Consejos

- Para una retroalimentación de sidetone con baja latencia al usar una paleta, active **Sidetone** en el subpanel de CW. El botón **Sidetone** y el control deslizante **Sidetone volume** controlan simultáneamente tanto el monitor alimentado por DAX del radio como el sidetone de baja latencia del lado del cliente (aproximadamente 10 ms de latencia). El tono y el paneo siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio. En Windows, el flujo de sidetone ahora comienza inmediatamente al conectarse (v0.9.3, corrección #2105). Consulte [Escuchar un monitor de sidetone TX](listen-to-a-tx-sidetone-monitor.md).
- Ajuste **Speed (CW)** antes de activar **Iambic** para evitar transmitir a una velocidad inesperada. Consulte [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md).
- Si desea operación QSK completa, active también **Breakin**. Para establecer un tiempo de retención en su lugar, desactive **Breakin** y configure **Delay (CW)** con un valor distinto de cero. Consulte [Establecer el retardo de break-in CW](set-cw-break-in-delay.md).

## Solución de problemas

- **El subpanel de CW no es visible, solo aparecen los controles de Phone** — El slice activo no está en modo CW. Cambie el modo del slice a CW o CW-USB/CW-LSB en el radio o en AetherSDR; el applet cambiará automáticamente.
- **El botón Iambic está presente pero la paleta no transmite** — Verifique que la paleta esté conectada al conector de llave correcto del FLEX-8600. El manipulador iámbico es una función del lado del radio; AetherSDR envía el comando de activación, pero la manipulación física depende de la conexión de hardware.
- **El indicador Level no aparece después de conectarse con la fuente de micrófono configurada como PC** — En v0.9.3, el indicador Level aparece inmediatamente al conectarse cuando la fuente de micrófono es PC (#2086). Si el indicador no aparece, confirme que la fuente de micrófono está configurada como **PC** en el selector **Mic source** y que está ejecutando v0.9.3 o posterior. Cuando la fuente es PC, el medidor utiliza medición del lado del cliente y no es suprimido por el ajuste `met_in_rx`.

## Relacionados

- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone TX](listen-to-a-tx-sidetone-monitor.md)
