# Ajustar el volumen del tono lateral (sidetone) de CW

En AetherSDR v0.9.2.1, el tono lateral local del lado del cliente y el monitor de tono lateral alimentado por DAX del radio se controlan juntos mediante un único conjunto de controles. Se han eliminado el botón Local STn independiente, el control deslizante de volumen del tono lateral local, el interruptor Follow y el control deslizante de tono del tono lateral local. El interruptor **Sidetone** y el control deslizante **Sidetone volume** en el subpanel de CW ahora controlan simultáneamente tanto el monitor del radio como el generador de tono lateral local de baja latencia del lado del cliente (~10 ms de latencia). El tono y el paneo siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al subpanel de CW cuando se selecciona un modo CW.

## Pasos

1. Haga clic en el botón de bandeja `P/CW` en la barra lateral derecha para abrir el applet Phone/CW.
2. Confirme que el subpanel de CW es visible. Si el slice activo está en un modo CW, el panel cambia automáticamente a los controles de CW.
3. Haga clic en **Sidetone** para habilitar el monitoreo del tono lateral. Esto activa simultáneamente el monitor alimentado por DAX del radio y el generador de tono lateral local de baja latencia.
4. Arrastre el control deslizante **Sidetone volume** hacia la izquierda o la derecha para establecer el nivel deseado. El rango es 0–100. El nivel del monitor del lado del radio (`mon_gain_cw`) y el volumen del generador de tono lateral local cambian juntos.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Notas |
|---|---|---|---|
| Sidetone | Off | On / Off | Controla simultáneamente el monitor del radio y el generador de tono lateral local. |
| Sidetone volume | — | 0–100 | Establece `mon_gain_cw` y el volumen del tono lateral local de forma simultánea. |
| L / R pan (CW) | 50 | 0–100 | Aplica paneo de potencia constante tanto al monitor del radio como al tono lateral local. Haga doble clic para recentrar. |
| Pitch < / > | 600 Hz | 100–6000 Hz (paso 10) | Sigue automáticamente el ajuste `cw_pitch` del radio. |

**Sidetone** — Activa o desactiva el monitoreo del tono lateral de CW. Cuando está habilitado, el monitor alimentado por DAX del radio y el generador de tono lateral del lado del cliente (~10 ms de latencia) están ambos activos. Cuando está deshabilitado, ninguno produce audio.

**Sidetone volume** — Establece el volumen tanto del monitor del radio como del generador de tono lateral local con un único control deslizante. Ya no existe un control de volumen independiente para cada uno.

**L / R pan (CW)** — Establece la posición de paneo estéreo. El mismo valor de paneo se aplica tanto al monitor del radio como al generador de tono lateral local mediante paneo de potencia constante. El paneo siempre refleja el ajuste `mon_pan_cw` del radio. Haga doble clic en el control deslizante para devolverlo al centro (50).

**Pitch < / >** — Incrementa o decrementa el tono del tono lateral y de decodificación de CW en 10 Hz por clic. El tono siempre está sincronizado con el ajuste `cw_pitch` del radio y se aplica automáticamente tanto al monitor del radio como al generador de tono lateral local. No se necesita un interruptor de seguimiento independiente ni un control deslizante de tono manual.

## Sugerencias

- Debido a que el monitor del radio y el generador de tono lateral local están ahora vinculados, no es posible establecer niveles de volumen diferentes para cada uno. Si escucha audio duplicado o con efecto de fase, confirme que la salida de audio del sistema y la salida de audio DAX del radio no estén enrutadas simultáneamente a los mismos altavoces o auriculares.
- La generación de tono lateral local permanece activa para transmisiones con paleta, manipulador manual y generadas por CWX siempre que **Sidetone** esté habilitado.
- La latencia del tono lateral local de aproximadamente 10 ms no ha cambiado. A velocidades más altas en PPM, esto sigue siendo preferible a la latencia de ida y vuelta del DAX del radio.

## Relacionado

- [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)
- [Cambiar el tono de CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
