# Habilitar el tono lateral CW de baja latencia para trabajo con paddle / manipulador recto / CWX

El tono lateral CW en AetherSDR opera con una latencia de aproximadamente 10 ms. A partir de la versión v0.9.2.1, el tono lateral local del lado del cliente ya no es un subsistema independiente con sus propios controles. En su lugar, el botón **Sidetone** y el control deslizante **Sidetone volume** del subpanel CW controlan de forma sincronizada tanto el monitor del radio alimentado por DAX como el generador de tono de baja latencia del lado del cliente (CwSidetoneGenerator). El tono (pitch) y el paneo siguen siempre automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio.

Use esta función cuando la ruta del tono lateral del radio introduzca demasiado retardo para operar cómodamente con paddle, manipulador recto o CWX.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- La slice activa debe estar en un modo CW. El applet Phone/CW cambia automáticamente a su subpanel CW cuando hay una slice CW activa.
- El applet Phone/CW debe estar visible en el Panel de Applets. Si no lo está, haga clic en el botón de bandeja **P/CW** de la barra lateral derecha.

## Pasos

1. Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** de la barra lateral derecha. El subpanel CW aparece automáticamente cuando la slice activa está en modo CW.
2. Haga clic en **Sidetone** para habilitar el tono lateral. Tanto el monitor del radio alimentado por DAX como el generador de tono de baja latencia del lado del cliente se activan juntos.
3. Ajuste el control deslizante **Sidetone volume** a un nivel de escucha cómodo (0–100). La ganancia del monitor del lado del radio (`mon_gain_cw`) y el volumen del generador de tono lateral local cambian de forma simultánea.
4. Para ajustar la posición estéreo, arrastre el control deslizante **L / R pan (CW)** (0–100, valor predeterminado 50 = centro). Haga doble clic en el control para volver al centro. El valor de paneo se aplica tanto al monitor del radio como al generador de tono lateral local mediante paneo de potencia constante.
5. Para cambiar el tono del tono lateral, use el selector **Pitch < / >** (100–6000 Hz, paso de 10 Hz). El tono siempre sigue automáticamente el ajuste `cw_pitch` del radio.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| **Sidetone** | Desactivado | Activado / Desactivado | Habilita el tono lateral CW. Controla de forma sincronizada tanto el monitor del radio alimentado por DAX como el CwSidetoneGenerator del lado del cliente. |
| **Sidetone volume** | — | 0–100 | Establece el volumen de reproducción del tono lateral. Se aplica simultáneamente a `mon_gain_cw` en el radio y al generador de tono lateral local. |
| **L / R pan (CW)** | 50 | 0–100 | Establece el paneo estéreo para el monitor CW. Se aplica tanto al radio como al generador de tono lateral local mediante paneo de potencia constante. Haga doble clic para centrar. |
| **Pitch < / >** | 600 Hz | 100–6000 Hz (paso 10) | Ajusta el tono lateral CW y el tono de decodificación. El tono siempre sigue automáticamente el ajuste `cw_pitch` del radio. |

## Consejos

- El tono lateral local funciona tanto para texto generado por CWX como para entrada de paddle y manipulador recto. No se necesita ninguna configuración adicional para CWX.
- Como el tono y el paneo siguen automáticamente los ajustes del radio, cambiar el selector **Pitch < / >** o `mon_pan_cw` en el radio siempre mantiene el tono lateral local sincronizado. No existe anulación manual del tono ni interruptor de seguimiento.
- El control deslizante **Delay (CW)** (0–2000 ms, paso 10) controla el retardo de break-in CW y es independiente del comportamiento del tono lateral.

## Solución de problemas

- **El botón Sidetone no es visible** — El subpanel CW solo aparece cuando la slice activa está en modo CW. Cambie el modo de la slice a CW y el applet se actualizará automáticamente.
- **No hay audio del tono lateral aunque Sidetone esté habilitado** — Verifique que el dispositivo de salida de audio del sistema esté configurado y no silenciado. El tono lateral local se reproduce a través del audio del sistema del cliente, no por el altavoz del radio.
- **El tono del tono lateral no es el esperado** — El tono sigue el ajuste `cw_pitch` del radio. Ajuste el selector **Pitch < / >** para cambiarlo.

## Temas relacionados

- [Cambiar el tono CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)
- [Habilitar el manipulado con paddle iámbico](enable-iambic-paddle-keying.md)
