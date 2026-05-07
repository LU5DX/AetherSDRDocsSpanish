# Establecer el volumen del tono de CW

En AetherSDR v0.9.2.1, el tono local del lado del cliente y el monitor de tono alimentado por DAX de la radio se controlan juntos mediante un único conjunto de controles. Se han eliminado el botón Local STn independiente, el control deslizante de volumen de tono local, el conmutador Follow y el control deslizante de tono local. El conmutador **Sidetone** y el control deslizante **Sidetone volume** en el subpanel CW ahora controlan tanto el monitor de la radio como el generador de tono de baja latencia del lado del cliente (~10 ms de latencia) de forma sincronizada. El tono y la panorámica siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al subpanel CW cuando se selecciona un modo CW.

## Pasos

1. Haga clic en el botón de la bandeja `P/CW` en la barra lateral derecha para abrir el applet Phone/CW.
2. Confirme que el subpanel CW esté visible. Si el slice activo está en un modo CW, el panel cambia a los controles CW automáticamente.
3. Haga clic en **Sidetone** para habilitar la monitorización del tono. Esto activa tanto el monitor alimentado por DAX de la radio como el generador de tono de baja latencia del lado del cliente al mismo tiempo.
4. Arrastre el control deslizante **Sidetone volume** hacia la izquierda o la derecha para establecer el nivel deseado. El rango es de 0 a 100. Tanto el nivel del monitor del lado de la radio (`mon_gain_cw`) como el volumen del generador de tono local cambian juntos.

## Qué hace cada control

| Control         | Valor predeterminado | Rango válido         |
|-----------------|----------------------|----------------------|
| Sidetone        | —                    | On / Off             |
| Sidetone volume | —                    | 0–100                |
| L / R pan (CW)  | 50                   | 0–100                |
| Pitch < / >     | 600 Hz               | 100–6000 Hz (paso 10) |

**Sidetone** — Activa o desactiva la monitorización del tono de CW. Cuando está habilitado, tanto el monitor alimentado por DAX de la radio como el generador de tono del lado del cliente (~10 ms de latencia) están activos. Cuando está deshabilitado, ninguno produce audio. En Windows, el flujo de tono se inicia inmediatamente al conectar (v0.9.3, #2105 — corrección del orden de inicialización de AudioEngine).

**Sidetone volume** — Establece el volumen tanto del monitor de la radio como del generador de tono local con un solo control deslizante. Ya no existe un control de volumen separado para cada uno.

**L / R pan (CW)** — Establece la posición de panorámica estéreo. El mismo valor de panorámica se aplica tanto al monitor de la radio como al generador de tono local mediante panorámica de potencia constante. La panorámica siempre refleja el ajuste `mon_pan_cw` de la radio. Haga doble clic en el control deslizante para volver al centro (50).

**Pitch < / >** — Ajusta el tono de CW y el tono de decodificación en incrementos de 10 Hz por clic. El tono siempre está sincronizado con el ajuste `cw_pitch` de la radio y se aplica tanto al monitor de la radio como al generador de tono local automáticamente. No se necesita un conmutador Follow independiente ni un control deslizante de tono manual.

## Notas del panel Phone

**Level gauge** — Muestra el nivel pico de entrada del micrófono en dBFS (rango −40 a +10 dBFS; rojo por encima de 0). El indicador se suprime a −150 cuando `met_in_rx` está desactivado y la radio no está transmitiendo, excepto cuando la fuente del micrófono está configurada en **PC**: en ese caso, el indicador utiliza la medición del lado del cliente y aparece inmediatamente al conectar, independientemente del estado de `met_in_rx` (v0.9.3, #2086).

**VOX** — Cuando VOX se activa o desactiva mediante un atajo de teclado, el panel Phone ahora se actualiza instantáneamente para reflejar el nuevo estado (v0.9.3, #2084).

## Consejos

- Debido a que el monitor de la radio y el generador de tono local ahora están vinculados, no puede establecer diferentes niveles de volumen para cada uno. Si escucha audio duplicado o con fase, confirme que la salida de audio de su sistema y la salida de audio DAX de la radio no estén enrutadas ambas a los mismos altavoces o auriculares simultáneamente.
- La generación de tono local permanece activa para transmisiones con paleta, llave recta y CWX generadas siempre que **Sidetone** esté habilitado.
- La latencia local del tono de aproximadamente 10 ms no ha cambiado. A WPM más altos, esto sigue siendo preferible a la latencia de ida y vuelta DAX de la radio.

## Relacionado

- [Listen to a TX sidetone monitor](listen-to-a-tx-sidetone-monitor.md)
- [Change CW pitch / sidetone frequency](change-cw-pitch-sidetone-frequency.md)
