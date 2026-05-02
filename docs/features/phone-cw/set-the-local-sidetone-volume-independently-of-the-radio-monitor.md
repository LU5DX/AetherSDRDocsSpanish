# Ajustar el volumen del sidetone de CW

En AetherSDR v0.9.2.1, el sidetone local del cliente y el monitor de sidetone del radio alimentado por DAX se controlan conjuntamente mediante un único conjunto de controles. Se han eliminado el botón separado Local STn, el deslizador de volumen de sidetone local, el botón Follow y el deslizador de tono de sidetone local. El botón **Sidetone** y el deslizador **Sidetone volume** en el subpanel de CW controlan ahora tanto el monitor del radio como el generador de sidetone local de baja latencia (~10 ms de latencia) de forma sincronizada. El tono y el paneo siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice (segmento de frecuencia) activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al subpanel de CW cuando se selecciona un modo CW.

## Pasos

1. Haga clic en el botón de bandeja `P/CW` en la barra lateral derecha para abrir el applet Phone/CW.
2. Confirme que el subpanel de CW es visible. Si el slice activo está en un modo CW, el panel cambia automáticamente a los controles de CW.
3. Haga clic en **Sidetone** para activar la monitorización del sidetone. Esto activa simultáneamente el monitor del radio alimentado por DAX y el generador de sidetone local de baja latencia.
4. Arrastre el deslizador **Sidetone volume** hacia la izquierda o la derecha para establecer el nivel deseado. El rango es 0–100. El nivel del monitor en el lado del radio (`mon_gain_cw`) y el volumen del generador de sidetone local cambian juntos.

## Función de cada control

| Control         | Valor predeterminado | Rango válido          |
|-----------------|----------------------|-----------------------|
| Sidetone        | —                    | On / Off              |
| Sidetone volume | —                    | 0–100                 |
| L / R pan (CW)  | 50                   | 0–100                 |
| Pitch < / >     | 600 Hz               | 100–6000 Hz (paso 10) |

**Sidetone** — Activa o desactiva la monitorización del sidetone de CW. Cuando está habilitado, el monitor del radio alimentado por DAX y el generador de sidetone local (~10 ms de latencia) están ambos activos. Cuando está deshabilitado, ninguno produce audio. En Windows, el flujo de sidetone comienza inmediatamente al conectarse (v0.9.3, #2105 — corrección del orden de inicialización de AudioEngine).

**Sidetone volume** — Establece el volumen tanto del monitor del radio como del generador de sidetone local mediante un único deslizador. Ya no existe un control de volumen independiente para cada uno.

**L / R pan (CW)** — Establece la posición de paneo estéreo. El mismo valor de paneo se aplica tanto al monitor del radio como al generador de sidetone local mediante paneo de potencia constante. El paneo refleja siempre el ajuste `mon_pan_cw` del radio. Haga doble clic en el deslizador para volver al centro (50).

**Pitch < / >** — Ajusta el tono del sidetone y de la decodificación de CW en pasos de 10 Hz por clic. El tono siempre está sincronizado con el ajuste `cw_pitch` del radio y se aplica automáticamente tanto al monitor del radio como al generador de sidetone local. No se necesita ningún botón de seguimiento separado ni un deslizador de tono manual.

## Notas del panel Phone

**Level gauge** — Muestra el nivel de pico de la entrada del micrófono en dBFS (rango de −40 a +10 dBFS; rojo por encima de 0). El indicador se suprime a −150 cuando `met_in_rx` está desactivado y el radio no está transmitiendo, excepto cuando la fuente de micrófono está configurada como **PC**: en ese caso, el indicador utiliza la medición del lado del cliente y aparece inmediatamente al conectarse, independientemente del estado de `met_in_rx` (v0.9.3, #2086).

**VOX** — Cuando se activa o desactiva VOX mediante un atajo de teclado, el panel Phone ahora se actualiza instantáneamente para reflejar el nuevo estado (v0.9.3, #2084).

## Consejos

- Dado que el monitor del radio y el generador de sidetone local están ahora vinculados, no es posible establecer niveles de volumen diferentes para cada uno. Si escucha audio duplicado o con efecto de fase, confirme que la salida de audio del sistema y la salida de audio DAX del radio no se estén enrutando simultáneamente a los mismos altavoces o auriculares.
- La generación de sidetone local permanece activa para transmisiones con paddle, manipulador recto y transmisiones generadas por CWX siempre que **Sidetone** esté habilitado.
- La latencia de sidetone local de aproximadamente 10 ms no ha cambiado. A velocidades de CW más altas en WPM, esto sigue siendo preferible a la latencia de ida y vuelta del DAX del radio.

## Relacionado

- [Escuchar un monitor de sidetone en TX](listen-to-a-tx-sidetone-monitor.md)
- [Cambiar el tono de CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
