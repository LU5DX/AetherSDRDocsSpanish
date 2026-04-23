# Ejecutar un ajuste automático en el TGXL externo

Esta página explica cómo iniciar el ciclo de ajuste automático del 4O3A Tuner Genius XL desde AetherSDR y cómo leer el resultado cuando finaliza.

## Antes de comenzar

- El radio debe detectar el Tuner Genius XL. El botón TUN en la bandeja del panel lateral derecho aparece únicamente cuando el TGXL está presente.
- El radio debe estar conectado. El TunerApplet requiere una conexión de radio activa.
- El sintonizador debe estar en estado OPERATE antes de ejecutar un ajuste automático. Si el botón muestra "BYPASS" o "STANDBY", consulte [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md).

## Pasos

1. Haga clic en el botón TUN de la bandeja del panel lateral derecho para abrir el applet Tuner.
2. Confirme que el botón OPERATE muestre "OPERATE" (en verde). Si no es así, haga clic en el botón hasta que cicle a "OPERATE".
3. Haga clic en TUNE.
4. El botón TUNE se torna rojo y muestra "TUNING..." mientras se ejecuta el ciclo de ajuste.
5. Cuando el ciclo finaliza, el botón muestra brevemente "SWR x.xx" — la ROS final estabilizada tras el ajuste — durante 2.5 segundos y luego regresa a "TUNE".

## Qué hace cada control

| Control | Descripción | Rango válido |
|---|---|---|
| TUNE | Inicia el ciclo de ajuste automático. Se torna rojo y muestra "TUNING..." durante el ciclo. Parpadea con el resultado final de ROS durante 2.5 s al terminar. | — |
| Fwd Pwr | Muestra la potencia directa reportada por el TGXL durante el ajuste. | 0–200 W barefoot, 0–600 W Aurora, 0–2000 W con PGXL |
| SWR | Muestra la ROS reportada por el TGXL en tiempo real. | 1.0–3.0 (rojo por encima de 2.5) |
| C1 | Muestra la posición del banco de relés C1 después de que el ajuste se completa. | 0–255 |
| L | Muestra la posición del banco de relés L después de que el ajuste se completa. | 0–255 |
| C2 | Muestra la posición del banco de relés C2 después de que el ajuste se completa. | 0–255 |

## Consejos

- El valor de ROS que se muestra tras el ajuste refleja un valor estabilizado capturado hasta 400 ms después de que el ciclo de ajuste termina, no la ROS durante el barrido de relés. Esto proporciona una lectura final más precisa.
- Si desea leer la ROS posterior al ajuste independientemente del destello de 2.5 segundos, observe el medidor de ROS directamente después de que el botón TUNE regrese a "TUNE".

## Solución de problemas

- **El botón TUN de la bandeja no aparece** — El radio no ha detectado el TGXL. Verifique que el sintonizador esté encendido y correctamente conectado al radio Flex.
- **El botón TUNE regresa a "TUNE" inmediatamente sin mostrar un resultado de ROS** — Es posible que el ciclo de ajuste se haya cancelado o que el TGXL no haya reportado una ROS estabilizada. Verifique el estado físico del sintonizador e intente de nuevo.
- **El botón TUNE muestra "SWR 3.00" o un valor muy alto** — El sintonizador no pudo encontrar una coincidencia aceptable en la frecuencia y antena actuales. Verifique que la antena esté conectada y que la banda esté dentro del rango de ajuste del sintonizador.

## Relacionados

- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Leer la ROS inmediatamente después de un ajuste](read-swr-immediately-after-a-tune.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Descripción general del sintonizador](overview.md)
