# Leer la ROE inmediatamente después de una sintonización

Una vez que finaliza la autosintonización, el botón TUNE muestra brevemente el valor final de ROE estabilizado para que pueda confirmar la adaptación sin necesidad de mirar el indicador de ROE.

## Antes de comenzar

- Debe estar conectado y detectado un Tuner Genius XL de 4O3A. El botón de la bandeja TUN aparece en la barra lateral derecha solo cuando hay un TGXL presente.
- El applet del sintonizador debe estar abierto. Haga clic en el botón de la bandeja TUN para abrirlo.
- El sintonizador debe estar en estado OPERATE (el botón OPERATE se muestra en verde).

## Pasos

1. Haga clic en TUNE.
2. Espere. El botón se vuelve rojo y muestra "TUNING..." mientras se ejecuta el barrido de autosintonización.
3. Cuando finaliza la sintonización, el botón recupera su estilo normal y muestra brevemente "TUNING..." durante un máximo de 400 ms mientras AetherSDR captura el valor final de ROE estabilizado desde el TGXL.
4. A continuación, el botón muestra el resultado como "SWR x.xx" — por ejemplo, "SWR 1.34". Lea este valor directamente desde el botón.
5. Después de 2.5 segundos, la etiqueta del botón vuelve a "TUNE".

Si pierde la visualización breve, el indicador de ROE continúa mostrando el valor de ROE en vivo reportado por el TGXL después de la sintonización.

## Qué hace cada control

| Control | Tipo | Comportamiento | Rango válido |
|---|---|---|---|
| Fwd Pwr | Medidor | Muestra la potencia directa reportada por el TGXL. La escala es 0–200 W sin amplificador, 0–600 W con amplificador Aurora, 0–2000 W con amplificador PGXL. La barra sube rápidamente con las ráfagas de RF y disminuye en aproximadamente 800 ms para evitar parpadeos por ruido entre paquetes. Una marca blanca muestra el pico de potencia directa, que se borra después de 2.5 segundos sin nuevos picos. | Ver escala |
| SWR | Medidor | Muestra continuamente la ROE en vivo reportada por el TGXL. Se vuelve rojo por encima de 2.5. La barra sube rápidamente y disminuye en aproximadamente 800 ms. Una marca blanca muestra el pico de ROE, que se borra después de 2.5 segundos sin nuevos picos. | 1.0–3.0 |
| C1 | Medidor | Muestra la posición del banco de relés C1. La rueda del ratón ajusta la posición del relé cuando hay una conexión directa al TGXL activa. | 0–255 |
| L | Medidor | Muestra la posición del banco de relés L. La rueda del ratón ajusta la posición del relé. | 0–255 |
| C2 | Medidor | Muestra la posición del banco de relés C2. La rueda del ratón ajusta la posición del relé. | 0–255 |
| TUNE | Botón | Inicia la autosintonización. Se vuelve rojo y muestra "TUNING..." durante el barrido. Muestra "SWR x.xx" durante 2.5 s al finalizar. Luego vuelve a "TUNE". Cuando hay una conexión directa al TGXL (puerto 9010) configurada en Radio Setup → Tuner, el comando de autosintonización se envía directamente al TGXL, omitiendo la ruta del firmware de la radio. Vuelve a la ruta de la radio cuando no hay conexión directa disponible. | — |
| OPERATE | Botón | Cicla por tres estados: OPERATE (verde), BYPASS (naranja) y STANDBY (predeterminado). Cada clic avanza al siguiente estado. | — |
| ANT 1, ANT 2, ANT 3 | Botón | Selecciona el puerto de antena correspondiente en el conmutador 3x1 del TGXL. Estos botones aparecen solo cuando hay una conexión directa al TGXL activa y el conmutador de antena está presente. | — |

## Consejos

- La ventana de captura de 400 ms después de sintonización=0 existe porque el valor final de ROE estabilizado del TGXL a menudo llega a través de TCP ligeramente después de la señal de sintonización completa. El valor mostrado en el botón refleja esta lectura estabilizada, no una muestra tomada durante el barrido.
- Si la ventana de captura expira antes de que llegue una lectura de ROE válida, AetherSDR recurre al último valor de ROE en vivo del indicador.
- La marca de retención de pico en los indicadores le ayuda a ver la máxima potencia o ROE alcanzada durante una transmisión, que se borra automáticamente después de 2.5 segundos.
- La disminución lenta en las barras del indicador (800 ms) evita molestos parpadeos que podrían ocurrir por breves intervalos entre paquetes UDP.

## Solución de problemas

- **El botón TUNE vuelve a "TUNE" sin mostrar un valor de ROE** — La transición del estado de sintonización no fue precedida por una sintonización activa (por ejemplo, el estado del modelo cambió externamente). Haga clic en TUNE nuevamente para ejecutar una nueva autosintonización.
- **El indicador de ROE marca por encima de 2.5 (rojo) después de la sintonización** — El sintonizador no pudo encontrar una adaptación satisfactoria en la banda y antena actuales. Verifique la conexión de la antena e intente nuevamente, o revise las posiciones de los relés C1, L y C2.

## Relacionados

- [Ejecutar una autosintonización en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
