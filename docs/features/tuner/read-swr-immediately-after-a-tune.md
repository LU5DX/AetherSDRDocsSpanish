# Leer la ROE inmediatamente después de un ajuste automático

Cuando un ajuste automático finaliza, el botón TUNE muestra brevemente la ROE final estabilizada para que pueda confirmar la adaptación sin necesidad de mirar el medidor de ROE.

## Antes de comenzar

- Es necesario que haya un sintonizador 4O3A Tuner Genius XL conectado y detectado. El botón TUN en la bandeja aparece en la barra lateral derecha únicamente cuando hay un TGXL presente.
- El applet Tuner debe estar abierto. Haga clic en el botón TUN de la bandeja para abrirlo.
- El sintonizador debe estar en estado OPERATE (el botón OPERATE aparece en verde).

## Pasos

1. Haga clic en TUNE.
2. Espere. El botón se pone rojo y muestra "TUNING..." mientras se ejecuta el barrido de ajuste automático.
3. Cuando el ajuste finaliza, el botón recupera su estilo normal y muestra brevemente "TUNING..." durante hasta 400 ms mientras AetherSDR captura el valor final de ROE estabilizada proveniente del TGXL.
4. A continuación, el botón muestra el resultado como "SWR x.xx" — por ejemplo, "SWR 1.34". Lea este valor directamente desde el botón.
5. Transcurridos 2.5 segundos, la etiqueta del botón vuelve a "TUNE".

Si no alcanza a ver el destello, el medidor de ROE continúa mostrando el valor de ROE reportado en vivo por el TGXL después del ajuste.

## Qué hace cada control

| Control | Tipo | Comportamiento | Rango válido |
|---|---|---|---|
| TUNE | Botón | Inicia el ajuste automático. Se pone rojo y muestra "TUNING..." durante el barrido. Destella "SWR x.xx" durante 2.5 s al finalizar. Regresa a "TUNE" posteriormente. | — |
| SWR | Medidor | Muestra continuamente la ROE reportada en vivo por el TGXL. Se pone rojo por encima de 2.5. | 1.0–3.0 |

## Consejos

- La ventana de captura de 400 ms después de tuning=0 existe porque el valor de ROE final estabilizada del TGXL suele llegar por TCP ligeramente después de la señal de ajuste completado. El valor que se muestra en el botón refleja esta lectura estabilizada, no una muestra tomada durante el barrido.
- Si la ventana de captura expira antes de que llegue una lectura de ROE válida, AetherSDR recurre al último valor de ROE en vivo del medidor.

## Solución de problemas

- **El botón TUNE regresa a "TUNE" sin mostrar un valor de ROE** — La transición de estado de ajuste no fue precedida por un ajuste activo (por ejemplo, el estado del modelo cambió externamente). Haga clic en TUNE nuevamente para ejecutar un ajuste automático nuevo.
- **El medidor de ROE marca por encima de 2.5 (rojo) después del ajuste** — El sintonizador no pudo encontrar una adaptación satisfactoria en la banda y antena actuales. Verifique la conexión de la antena e inténtelo de nuevo, o revise las posiciones de los relés C1, L y C2.

## Temas relacionados

- [Ejecutar un ajuste automático en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
