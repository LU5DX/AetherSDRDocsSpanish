# Habilitar el silbato CW de baja latencia para trabajo rápido con manípulo, llave recta o CWX

El silbato CW en AetherSDR opera con una latencia de aproximadamente 10 ms. A partir de la versión v0.9.2.1, el silbato local del lado del cliente ya no es un subsistema separado con sus propios controles. En su lugar, el único botón **Sidetone** y el control deslizante **Sidetone volume** en el subpanel CW controlan tanto el monitor alimentado por DAX de la radio como el generador de tonos de baja latencia del lado del cliente (CwSidetoneGenerator) de forma sincronizada. El tono y la panoramización siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio.

Utilice esta función cuando la ruta del silbato de la radio introduzca demasiado retraso para una operación cómoda con manípulo, llave recta o CWX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- La porción activa debe estar en un modo CW. El applet Phone/CW cambia automáticamente a su subpanel CW cuando una porción CW está activa.
- El applet Phone/CW debe ser visible en el Panel de applets. Si no lo está, haga clic en el botón de bandeja **P/CW** en la barra lateral derecha.

## Pasos

1. Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha. El subpanel CW aparece automáticamente cuando la porción activa está en modo CW.
2. Haga clic en **Sidetone** para habilitar el silbato. Tanto el monitor alimentado por DAX de la radio como el generador de tonos de baja latencia del lado del cliente se habilitan juntos.
3. Ajuste el control deslizante **Sidetone volume** a un nivel de escucha cómodo (0–100). Tanto la ganancia del monitor del lado de la radio (`mon_gain_cw`) como el volumen del generador de silbato local cambian juntos.
4. Para ajustar la colocación estéreo, arrastre el control deslizante **L / R pan (CW)** (0–100, valor predeterminado 50 = centro). Haga doble clic en el control deslizante para devolverlo al centro. El valor de panoramización se aplica tanto al monitor de la radio como al generador de silbato local utilizando panoramización de potencia constante.
5. Para cambiar el tono del silbato, use el cuadro de giro **Pitch < / >** (100–6000 Hz, paso de 10 Hz). El tono siempre sigue automáticamente el ajuste `cw_pitch` de la radio.

## Qué hace cada control

| Control             | Valor predeterminado | Rango válido         |
|---------------------|----------------------|----------------------|
| **Sidetone**        | Apagado              | Encendido / Apagado  |
| **Sidetone volume** | —                    | 0–100                |
| **L / R pan (CW)**  | 50                   | 0–100                |
| **Pitch < / >**     | 600 Hz               | 100–6000 Hz (paso 10)|

## Consejos

- El silbato local funciona tanto para texto generado por CWX como para entrada con manípulo y llave recta. No se necesita configuración separada para CWX.
- Debido a que el tono y la panoramización siguen automáticamente los ajustes de la radio, cambiar el cuadro de giro **Pitch < / >** o `mon_pan_cw` en la radio siempre mantiene el silbato local sincronizado. No hay anulación manual del tono ni un botón de seguimiento.
- El control deslizante **Delay (CW)** (0–2000 ms, paso de 10) controla el retardo de inserción de CW y es independiente del comportamiento del silbato.

## Solución de problemas

- **El botón Sidetone no es visible** — El subpanel CW solo aparece cuando la porción activa está en un modo CW. Cambie el modo de la porción a CW y el applet se actualizará automáticamente.
- **No hay audio del silbato a pesar de que Sidetone está habilitado** — Verifique que el dispositivo de salida de audio de su sistema esté configurado y no esté silenciado. El silbato local se reproduce a través del audio del sistema cliente, no a través de la salida del altavoz de la radio. En Windows, si el silbato no se inicia inmediatamente después de la conexión, verifique que ninguna otra aplicación tenga acceso exclusivo al dispositivo de audio; este problema de orden de inicialización se solucionó en la versión v0.9.3 (#2105).
- **El tono del silbato no es el esperado** — El tono sigue el ajuste `cw_pitch` de la radio. Ajuste el cuadro de giro **Pitch < / >** para cambiarlo.
- **El indicador de nivel no aparece al conectar** — Si su fuente de micrófono está configurada en **PC**, el indicador de nivel ahora aparece inmediatamente al conectar a partir de la versión v0.9.3 (#2086). Si el indicador todavía falta, confirme que la fuente de micrófono esté configurada en **PC** en el selector **Mic source** y que AetherSDR esté conectado a la radio.

## Relacionados

- [Cambiar el tono CW / frecuencia del silbato](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de silbato de TX](listen-to-a-tx-sidetone-monitor.md)
- [Habilitar la manipulación con manípulo iámbico](enable-iambic-paddle-keying.md)
