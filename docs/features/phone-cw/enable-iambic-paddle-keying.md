# Habilitar el manipulador de paleta iámbica

Habilite el manipulador iámbico integrado del radio para que una paleta de doble palanca conectada al FLEX-8600 transmita CW en modo iámbico. Esto le permite ajustar la velocidad de manipulación y el comportamiento de break-in desde AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al subpanel de CW cuando hay un slice CW activo.
- Una paleta de doble palanca debe estar conectada físicamente al conector de llave del FLEX-8600.

## Pasos

1. Haga clic en el botón **P/CW** de la barra lateral derecha para abrir el applet Phone/CW. Si el applet ya está visible, omita este paso.
2. Confirme que se muestra el subpanel de CW. Si el slice activo está en modo CW, el applet muestra los controles de CW, incluidos **Iambic**, **Speed (CW)**, **Delay (CW)** y **Breakin**.
3. Haga clic en **Iambic** para habilitar el manipulador de paleta iámbica. El botón se resalta cuando está activo.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| **Iambic** | Activa o desactiva el manipulador de paleta iámbica en el radio. | — | On / Off | — |
| **Speed (CW)** | Establece la velocidad de manipulación CW. | — | 5–100 WPM | — |
| **Delay (CW)** | Establece el retardo de break-in en CW. | — | 0–2000 ms (paso 10) | — |
| **Breakin** | Activa o desactiva el break-in total (QSK). | — | On / Off | — |
| **Pitch < / >** | Ajusta el tono de sidetone y decodificación CW en incrementos de 10 Hz. | 600 Hz | 100–6000 Hz | — |

## Consejos

- Para obtener retroalimentación de sidetone con baja latencia al usar una paleta, habilite **Local STn** en el mismo subpanel de CW. El sidetone del lado del cliente tiene aproximadamente 10 ms de latencia, lo cual es significativamente menor que la ruta de monitor alimentada por DAX del radio. Consulte [Habilitar el sidetone CW local de baja latencia (Local STn) para trabajo con paleta, llave recta o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md).
- Ajuste **Speed (CW)** antes de habilitar **Iambic** para evitar transmitir a una velocidad inesperada. Consulte [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md).
- Si desea operación QSK completa, habilite también **Breakin**. Para establecer un tiempo de retención en su lugar, deshabilite **Breakin** y ajuste **Delay (CW)** a un valor distinto de cero. Consulte [Establecer el retardo de break-in en CW](set-cw-break-in-delay.md).

## Resolución de problemas

- **El subpanel de CW no es visible, solo aparecen los controles de Phone** — El slice activo no está en modo CW. Cambie el modo del slice a CW o CW-USB/CW-LSB en el radio o en AetherSDR; el applet cambiará automáticamente.
- **El botón Iambic está presente pero la paleta no manipula** — Verifique que la paleta esté conectada al conector de llave correcto en el FLEX-8600. El manipulador iámbico es una función del lado del radio; AetherSDR envía el comando de habilitación, pero la manipulación física depende de la conexión de hardware.

## Relacionados

- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in en CW](set-cw-break-in-delay.md)
- [Habilitar el sidetone CW local de baja latencia (Local STn) para trabajo con paleta, llave recta o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone TX](listen-to-a-tx-sidetone-monitor.md)
