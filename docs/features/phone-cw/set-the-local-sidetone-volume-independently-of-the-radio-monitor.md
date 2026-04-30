# Establecer el volumen del sidetone en CW

En AetherSDR v0.9.2.1, el sidetone local del lado del cliente y el monitor de sidetone alimentado por DAX de la radio se controlan conjuntamente mediante un único conjunto de controles. Se han eliminado el botón Local STn separado, el deslizador de volumen de sidetone local, el botón Follow y el deslizador de tono de sidetone local. El botón **Sidetone** y el deslizador **Sidetone volume** en el sub-panel de CW ahora controlan tanto el monitor de la radio como el generador de sidetone de baja latencia del lado del cliente (~10 ms de latencia) de manera sincronizada. El tono y el panoramizado siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al sub-panel de CW cuando se selecciona un modo CW.

## Pasos

1. Haga clic en el botón de bandeja `P/CW` en la barra lateral derecha para abrir el applet Phone/CW.
2. Confirme que el sub-panel de CW es visible. Si el slice activo está en un modo CW, el panel cambia a controles de CW automáticamente.
3. Haga clic en **Sidetone** para activar el monitoreo de sidetone. Esto activa tanto el monitor alimentado por DAX de la radio como el generador de sidetone de baja latencia del lado del cliente al mismo tiempo.
4. Arrastre el deslizador **Sidetone volume** hacia la izquierda o hacia la derecha para establecer el nivel deseado. El rango es 0–100. Tanto el nivel del monitor del lado de la radio (`mon_gain_cw`) como el volumen del generador de sidetone local cambian juntos.

## Qué hace cada control

| Control         | Predeterminado | Rango válido          |
|-----------------|---------|-----------------------|
| Sidetone        | —       | On / Off              |
| Sidetone volume | —       | 0–100                 |
| L / R pan (CW)  | 50      | 0–100                 |
| Pitch < / >     | 600 Hz  | 100–6000 Hz (paso 10) |

**Sidetone** — Activa o desactiva el monitoreo de sidetone en CW. Cuando está habilitado, tanto el monitor alimentado por DAX de la radio como el generador de sidetone del lado del cliente (~10 ms de latencia) están activos. Cuando está deshabilitado, ninguno produce audio. En Windows, la secuencia de sidetone se inicia inmediatamente al conectarse (v0.9.3, #2105 — corrección del orden de inicialización de AudioEngine).

**Sidetone volume** — Establece el volumen tanto del monitor de la radio como del generador de sidetone local con un único deslizador. Ya no hay un control de volumen separado para cada uno.

**L / R pan (CW)** — Establece la posición de panoramización estéreo. El mismo valor de panoramización se aplica tanto al monitor de la radio como al generador de sidetone local usando panoramización de potencia constante. El panoramizado siempre refleja el ajuste `mon_pan_cw` de la radio. Haga doble clic en el deslizador para devolverlo al centro (50).

**Pitch < / >** — Ajusta el sidetone de CW y la frecuencia de decodificación en incrementos de 10 Hz por clic. El tono siempre está sincronizado con el ajuste `cw_pitch` de la radio y se aplica automáticamente tanto al monitor de la radio como al generador de sidetone local. No se necesita un botón Follow separado ni un deslizador de tono manual.

## Notas del panel Phone

**Level gauge** — Muestra el nivel de pico de entrada del micrófono en dBFS (rango −40 a +10 dBFS; rojo por encima de 0). El indicador se suprime a −150 cuando `met_in_rx` está desactivado y la radio no está transmitiendo, excepto cuando la fuente de micrófono se establece en **PC**: en ese caso, el indicador utiliza medición del lado del cliente y aparece inmediatamente al conectarse independientemente del estado de `met_in_rx` (v0.9.3, #2086).

**VOX** — Cuando VOX se activa o desactiva mediante un atajo de teclado, el panel Phone ahora se actualiza instantáneamente para reflejar el nuevo estado (v0.9.3, #2084).

## Consejos

- Debido a que el monitor de la radio y el generador de sidetone local ahora están vinculados, no puede establecer niveles de volumen diferentes para cada uno. Si escucha audio duplicado o desfasado, confirme que la salida de audio del sistema y la salida de audio DAX de la radio no estén enrutadas simultáneamente a los mismos altavoces o auriculares.
- La generación de sidetone local permanece activa para transmisiones generadas por paddle, clave recta y CWX siempre que **Sidetone** esté habilitado.
- La latencia aproximada de 10 ms del sidetone local se mantiene sin cambios. A velocidades WPM más altas, esto sigue siendo preferible a la latencia de ida y vuelta de DAX de la radio.

## Relacionado

- [Escuchar un monitor de sidetone de transmisión](listen-to-a-tx-sidetone-monitor.md)
- [Cambiar la frecuencia de pitch / sidetone en CW](change-cw-pitch-sidetone-frequency.md)
