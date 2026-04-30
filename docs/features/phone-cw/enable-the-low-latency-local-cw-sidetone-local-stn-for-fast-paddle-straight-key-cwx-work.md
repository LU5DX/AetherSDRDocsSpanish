# Habilite el sidetone CW de baja latencia para trabajo rápido con paleta / llave recta / CWX

El sidetone CW en AetherSDR opera con una latencia de aproximadamente 10 ms. A partir de la v0.9.2.1, el sidetone del lado del cliente ya no es un subsistema separado con sus propios controles. En su lugar, el único botón **Sidetone** y el control deslizante **Sidetone volume** en el sub-panel CW controlan conjuntamente tanto el monitor alimentado por DAX de la radio como el generador de tonos de baja latencia del lado del cliente (CwSidetoneGenerator). El tono y la panoramización siempre siguen automáticamente los parámetros `cw_pitch` y `mon_pan_cw` de la radio.

Utilice esta función cuando la ruta de sidetone de la radio introduce demasiado retardo para una operación cómoda con paleta, llave recta o CWX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- La slice activa debe estar en un modo CW. El applet Phone/CW cambia automáticamente a su sub-panel CW cuando una slice CW está activa.
- El applet Phone/CW debe estar visible en el Applet Panel. Si no está visible, haga clic en el botón de bandeja **P/CW** en la barra lateral derecha.

## Pasos

1. Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha. El sub-panel CW aparece automáticamente cuando la slice activa está en modo CW.
2. Haga clic en **Sidetone** para habilitar el sidetone. Tanto el monitor alimentado por DAX de la radio como el generador de tonos de baja latencia del lado del cliente se habilitan conjuntamente.
3. Ajuste el control deslizante **Sidetone volume** a un nivel de escucha cómodo (0–100). Tanto la ganancia del monitor del lado de la radio (`mon_gain_cw`) como el volumen del generador de sidetone local cambian conjuntamente.
4. Para ajustar la ubicación estéreo, arrastre el control deslizante **L / R pan (CW)** (0–100, predeterminado 50 = centro). Haga doble clic en el control deslizante para devolverlo al centro. El valor de panoramización se aplica tanto al monitor de radio como al generador de sidetone local mediante panoramización de potencia constante.
5. Para cambiar el tono del sidetone, utilice el cuadro de giro **Pitch < / >** (100–6000 Hz, paso 10 Hz). El tono siempre sigue automáticamente el parámetro `cw_pitch` de la radio.

## Qué hace cada control

| Control             | Predeterminado | Rango válido          |
|---------------------|---------|-----------------------|
| **Sidetone**        | Desactivado     | Activado / Desactivado              |
| **Sidetone volume** | —       | 0–100                 |
| **L / R pan (CW)**  | 50      | 0–100                 |
| **Pitch < / >**     | 600 Hz  | 100–6000 Hz (paso 10) |

## Consejos

- El sidetone local funciona tanto para texto generado por CWX como para entrada de paleta y llave recta. No se requiere configuración separada para CWX.
- Debido a que el tono y la panoramización siguen automáticamente los parámetros de la radio, cambiar el cuadro de giro **Pitch < / >** o `mon_pan_cw` en la radio siempre mantiene el sidetone local sincronizado. No hay anulación manual de tono ni conmutador de seguimiento.
- El control deslizante **Delay (CW)** (0–2000 ms, paso 10) controla el retardo de ruptura CW y es independiente del comportamiento del sidetone.

## Solución de problemas

- **El botón Sidetone no es visible** — El sub-panel CW solo aparece cuando la slice activa está en un modo CW. Cambie el modo de slice a CW y el applet se actualizará automáticamente.
- **Sin audio del sidetone a pesar de que Sidetone está habilitado** — Verifique que el dispositivo de salida de audio del sistema esté configurado y no silenciado. El sidetone local se reproduce a través del audio del sistema del cliente, no de la salida del altavoz de la radio. En Windows, si el sidetone no se inicia inmediatamente después de conectarse, verifique que ninguna otra aplicación tenga acceso exclusivo al dispositivo de audio; este problema de orden de inicialización se corrigió en la v0.9.3 (#2105).
- **El tono del sidetone no es el que espera** — El tono sigue el parámetro `cw_pitch` de la radio. Ajuste el cuadro de giro **Pitch < / >** para cambiarlo.
- **El medidor de nivel no aparece al conectarse** — Si su fuente de micrófono está configurada en **PC**, el medidor de nivel ahora aparece inmediatamente al conectarse a partir de la v0.9.3 (#2086). Si el medidor aún falta, confirme que la fuente de micrófono está configurada en **PC** en el selector **Mic source** y que AetherSDR está conectado a la radio.

## Relacionado

- [Cambiar el tono CW / frecuencia del sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone TX](listen-to-a-tx-sidetone-monitor.md)
- [Habilitar el keying de paleta iámbica](enable-iambic-paddle-keying.md)
