# Activar el manipulador iámbico de paleta

Active el manipulador iámbico incorporado del radio para que una paleta de doble palanca conectada al FLEX-8600 transmita CW en modo iámbico. Esto permite configurar la velocidad de manipulación y el comportamiento de break-in desde AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El slice (canal de recepción) activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al subpanel de CW cuando hay un slice CW activo.
- Una paleta de doble palanca debe estar físicamente conectada al conector de llave del FLEX-8600.

## Pasos

1. Haga clic en el botón **P/CW** de la bandeja en la barra lateral derecha para abrir el applet Phone/CW. Si el applet ya está visible, omita este paso.
2. Confirme que el subpanel de CW está visible. Si el slice activo está en modo CW, el applet muestra los controles de CW, incluyendo **Iambic**, **Speed (CW)**, **Delay (CW)** y **Breakin**.
3. Haga clic en **Iambic** para activar el manipulador iámbico de paleta. El botón se resalta cuando está activo.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Iambic** | Activa o desactiva el manipulador iámbico de paleta en el radio. | — | On / Off | — |
| **Speed (CW)** | Establece la velocidad de manipulación CW. | — | 5–100 WPM | — |
| **Delay (CW)** | Establece el retardo de break-in en CW. | — | 0–2000 ms (paso 10) | — |
| **Breakin** | Activa o desactiva el break-in completo (QSK). | — | On / Off | — |
| **Pitch < / >** | Ajusta el tono de sidetone y decodificación CW en pasos de 10 Hz. | 600 Hz | 100–6000 Hz | — |

## Sugerencias

- Para una respuesta de sidetone de baja latencia al usar una paleta, active **Sidetone** en el subpanel de CW. A partir de la v0.9.2.1, el botón único **Sidetone** y el control deslizante **Sidetone volume** controlan de forma sincronizada tanto el monitor del radio alimentado por DAX como el sidetone de baja latencia en el lado del cliente (aproximadamente 10 ms de latencia). El tono y el paneo siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio. Consulte [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md).
- Ajuste **Speed (CW)** antes de activar **Iambic** para evitar transmitir a una velocidad inesperada. Consulte [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md).
- Si desea operación QSK completa, active también **Breakin**. Para establecer un tiempo de retención en lugar de QSK, desactive **Breakin** y configure **Delay (CW)** con un valor distinto de cero. Consulte [Establecer el retardo de break-in en CW](set-cw-break-in-delay.md).

## Solución de problemas

- **El subpanel de CW no está visible, solo aparecen los controles de Phone** — El slice activo no está en un modo CW. Cambie el modo del slice a CW o CW-USB/CW-LSB en el radio o en AetherSDR; el applet cambiará automáticamente.
- **El botón Iambic está presente pero la paleta no manipula** — Verifique que la paleta esté conectada al conector de llave correcto en el FLEX-8600. El manipulador iámbico es una función del lado del radio; AetherSDR envía el comando de activación, pero la manipulación física depende de la conexión de hardware.

## Relacionados

- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in en CW](set-cw-break-in-delay.md)
- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
