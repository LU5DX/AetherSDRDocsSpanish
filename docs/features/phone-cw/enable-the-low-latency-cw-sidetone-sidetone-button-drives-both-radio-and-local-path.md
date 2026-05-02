# Activar el sidetone de CW de baja latencia (el botón Sidetone controla tanto la radio como la ruta local)

Activar el sidetone de CW en AetherSDR habilita dos rutas simultáneamente: el monitor de la radio alimentado por DAX y un generador de tono del lado del cliente con aproximadamente 10 ms de latencia. Un único botón y un único control deslizante de volumen controlan ambas rutas en sincronía, de modo que se escucha un tono uniforme independientemente del jitter de red.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone/CW requiere una conexión activa con la radio.
- El slice activo debe estar en un modo CW. El panel del applet cambia automáticamente del subpanel Phone al subpanel CW cuando se detecta el modo CW.

## Pasos

1. Si el applet Phone/CW no está visible, haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrirlo.
2. Confirme que se muestra el subpanel CW. Si se muestra el subpanel Phone, cambie el slice activo a un modo CW en la radio; el panel cambia automáticamente.
3. Haga clic en **Sidetone** para activar el sidetone. El botón se ilumina cuando está activo.
4. Ajuste el control deslizante **Sidetone volume** a un nivel cómodo. El control deslizante regula simultáneamente el volumen del monitor del lado de la radio y el volumen del generador de tono del lado del cliente.
5. Opcionalmente, ajuste **Pitch < / >** para establecer la frecuencia del sidetone. El tono sigue automáticamente el ajuste `cw_pitch` de la radio, pero puede variarlo en incrementos de 10 Hz usando los controles **<** y **>**.

## Función de cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|---|
| Sidetone | Botón de alternancia | — | On / Off | — | Activa o desactiva el sidetone de CW. Controla en sincronía el monitor de la radio alimentado por DAX y el generador de tono local de baja latencia. |
| Sidetone volume | Deslizador | — | 0–100 | — | Establece el volumen tanto para el monitor del lado de la radio (`mon_gain_cw`) como para el generador de tono del lado del cliente simultáneamente. |
| Pitch < / > | Spinbox | 600 Hz | 100–6000 Hz (paso 10) | — | Varía el tono del sidetone y de decodificación en 10 Hz. Sigue automáticamente el ajuste `cw_pitch` de la radio. |
| L / R pan (CW) | Deslizador | 50 (centro) | 0–100 | — | Establece la panorámica estéreo tanto para el monitor del lado de la radio como para el generador de tono local. Doble clic para recentrar en 50. |

## Consejos

- El tono y la panorámica del generador de tono del lado del cliente siempre siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio. No es necesario configurarlos por separado para la ruta local.
- Hacer doble clic en el control deslizante **L / R pan (CW)** lo restablece al centro (50).

## Solución de problemas

- **No se escucha tono aunque Sidetone esté activado** — Confirme que el control deslizante **Sidetone volume** esté por encima de 0. Verifique también que el dispositivo de salida de audio del sistema esté configurado correctamente, ya que el generador del lado del cliente utiliza la ruta de audio local.
- **El botón Sidetone no está visible** — El subpanel CW solo aparece cuando el slice activo está en modo CW. Cambie el slice activo a CW en la radio; el panel del applet cambia automáticamente.
- **El tono no coincide con lo esperado** — El tono sigue el ajuste `cw_pitch` de la radio. Ajústelo usando **Pitch < / >** en el applet, que actualiza el ajuste de la radio en pasos de 10 Hz.

## Temas relacionados

- [Cambiar el tono CW / frecuencia del sidetone](change-cw-pitch-sidetone-frequency.md)
- [Desplazar el sidetone de CW a la izquierda o derecha](pan-the-cw-sidetone-left-or-right.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in de CW](set-cw-break-in-delay.md)
