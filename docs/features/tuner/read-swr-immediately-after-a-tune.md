# Leer la ROE inmediatamente después de una sintonización

Una vez que finaliza la autosintonización, el botón TUNE muestra brevemente la ROE final estabilizada para que pueda confirmar la adaptación sin mirar el indicador de ROE.

## Antes de comenzar

- Debe estar conectado y detectado un Tuner Genius XL de 4O3A. El botón de la bandeja TUN aparece en la barra lateral derecha solo cuando hay un TGXL presente.
- El applet del sintonizador debe estar abierto. Haga clic en el botón de la bandeja TUN para abrirlo.
- El sintonizador debe estar en estado OPERATE (el botón OPERATE se muestra en verde).

## Pasos

1. Haga clic en TUNE.
2. Espere. El botón se vuelve rojo y muestra "TUNING..." mientras se ejecuta el barrido de autosintonización.
3. Cuando la sintonización finaliza, el botón vuelve a su estilo normal y muestra brevemente "TUNING..." durante un máximo de 400 ms mientras AetherSDR captura el valor final de ROE estabilizada del TGXL.
4. El botón muestra entonces el resultado como "SWR x.xx" — por ejemplo, "SWR 1.34". Lea este valor directamente del botón.
5. Después de 2.5 segundos, la etiqueta del botón vuelve a "TUNE".

Si pierde el destello, el indicador de ROE continúa mostrando el valor de ROE en vivo reportado por el TGXL después de la sintonización.

## Función de cada control

| Control | Tipo | Comportamiento | Rango válido |
|---|---|---|---|
| TUNE | Botón | Inicia la autosintonización. Se vuelve rojo y muestra "TUNING..." durante el barrido. Muestra "SWR x.xx" durante 2.5 s al finalizar. Vuelve a "TUNE" después. | — |
| SWR | Medidor | Muestra continuamente la ROE en vivo reportada por el TGXL. Se vuelve rojo por encima de 2.5. | 1.0–3.0 |

## Consejos

- La ventana de captura de 400 ms después de tuning=0 existe porque el valor final de ROE estabilizada del TGXL a menudo llega por TCP ligeramente después de la señal de fin de sintonización. El valor mostrado en el botón refleja esta lectura estabilizada, no una muestra durante el barrido.
- Si la ventana de captura expira antes de que llegue una lectura de ROE válida, AetherSDR recurre al último valor de ROE en vivo del indicador.

## Solución de problemas

- **El botón TUNE vuelve a "TUNE" sin mostrar un valor de ROE** — La transición del estado de sintonización no fue precedida por una sintonización activa (por ejemplo, el estado del modelo cambió externamente). Haga clic en TUNE nuevamente para realizar una autosintonización nueva.
- **El indicador de ROE marca por encima de 2.5 (rojo) después de la sintonización** — El sintonizador no pudo encontrar una adaptación satisfactoria en la banda y antena actuales. Verifique la conexión de la antena e intente nuevamente, o verifique las posiciones de los relés C1, L y C2.

## Relacionados

- [Ejecutar una autosintonización en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
