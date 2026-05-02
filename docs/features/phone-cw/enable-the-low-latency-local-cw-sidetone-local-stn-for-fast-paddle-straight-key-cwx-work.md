# Activar la señal lateral de CW de baja latencia para paleta rápida / manipulador recto / CWX

La señal lateral (sidetone) de CW en AetherSDR opera con una latencia de aproximadamente 10 ms. A partir de la versión v0.9.2.1, la señal lateral local del lado del cliente ya no es un subsistema independiente con sus propios controles. En su lugar, el único botón **Sidetone** y el control deslizante **Sidetone volume** del subpanel de CW controlan de forma sincronizada tanto el monitor del radio alimentado por DAX como el generador de tono de baja latencia del lado del cliente (CwSidetoneGenerator). El tono y el paneo siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio.

Use esta función cuando la ruta de señal lateral del radio introduzca demasiado retardo para una operación cómoda con paleta, manipulador recto o CWX.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente a su subpanel de CW cuando hay un slice de CW activo.
- El applet Phone/CW debe estar visible en el Panel de Applets. Si no lo está, haga clic en el botón de bandeja **P/CW** de la barra lateral derecha.

## Pasos

1. Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** de la barra lateral derecha. El subpanel de CW aparece automáticamente cuando el slice activo está en modo CW.
2. Haga clic en **Sidetone** para activar la señal lateral. Tanto el monitor del radio alimentado por DAX como el generador de tono de baja latencia del lado del cliente se habilitan juntos.
3. Ajuste el control deslizante **Sidetone volume** hasta un nivel de escucha cómodo (0–100). La ganancia del monitor del lado del radio (`mon_gain_cw`) y el volumen del generador de señal lateral local cambian al mismo tiempo.
4. Para ajustar la posición estéreo, arrastre el control deslizante **L / R pan (CW)** (0–100, valor predeterminado 50 = centro). Haga doble clic en el control para volver al centro. El valor de paneo se aplica tanto al monitor del radio como al generador de señal lateral local mediante paneo de potencia constante.
5. Para cambiar el tono de la señal lateral, utilice el spinbox **Pitch < / >** (100–6000 Hz, paso de 10 Hz). El tono siempre sigue automáticamente el ajuste `cw_pitch` del radio.

## Función de cada control

| Control             | Valor predeterminado | Rango válido          |
|---------------------|---------------------|-----------------------|
| **Sidetone**        | Off                 | On / Off              |
| **Sidetone volume** | —                   | 0–100                 |
| **L / R pan (CW)**  | 50                  | 0–100                 |
| **Pitch < / >**     | 600 Hz              | 100–6000 Hz (paso 10) |

## Consejos

- La señal lateral local funciona tanto para texto generado por CWX como para entrada de paleta y manipulador recto. No se necesita configuración adicional para CWX.
- Dado que el tono y el paneo siguen los ajustes del radio automáticamente, cambiar el spinbox **Pitch < / >** o `mon_pan_cw` en el radio siempre mantiene la señal lateral local sincronizada. No existe anulación manual del tono ni un interruptor de seguimiento.
- El control deslizante **Delay (CW)** (0–2000 ms, paso 10) controla el retardo de break-in de CW y es independiente del comportamiento de la señal lateral.

## Solución de problemas

- **El botón Sidetone no es visible** — El subpanel de CW solo aparece cuando el slice activo está en modo CW. Cambie el modo del slice a CW y el applet se actualizará automáticamente.
- **No hay audio de la señal lateral a pesar de que Sidetone está activado** — Verifique que el dispositivo de salida de audio del sistema esté configurado y no esté silenciado. La señal lateral local se reproduce a través del audio del sistema del cliente, no por el altavoz del radio. En Windows, si la señal lateral no se inicia inmediatamente después de conectar, compruebe que ninguna otra aplicación tenga acceso exclusivo al dispositivo de audio; este problema de orden de inicialización se corrigió en v0.9.3 (#2105).
- **El tono de la señal lateral no es el esperado** — El tono sigue el ajuste `cw_pitch` del radio. Ajuste el spinbox **Pitch < / >** para modificarlo.
- **El indicador de nivel no aparece al conectar** — Si la fuente de micrófono está configurada en **PC**, el indicador de nivel aparece inmediatamente al conectar a partir de la versión v0.9.3 (#2086). Si el indicador sigue sin aparecer, confirme que la fuente de micrófono esté configurada en **PC** en el selector **Mic source** y que AetherSDR esté conectado al radio.

## Temas relacionados

- [Cambiar el tono de CW / frecuencia de señal lateral](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de señal lateral de TX](listen-to-a-tx-sidetone-monitor.md)
- [Activar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
