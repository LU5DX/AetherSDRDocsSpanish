# Ejecutar un sintonizador automático en el TGXL externo

Esta página explica cómo iniciar un ciclo de sintonización automática en un 4O3A Tuner Genius XL conectado. Use el sintonizador automático para encontrar la mejor combinación de relés C1/L/C2 para su frecuencia y antena actuales.

## Antes de comenzar

- AetherSDR debe detectar un Tuner Genius XL. El botón de la bandeja TUN aparece en la barra lateral derecha solo cuando hay un TGXL presente.
- La radio debe estar conectada. La applet Tuner requiere una conexión de radio activa.
- El TGXL debe estar en estado OPERATE (el botón muestra "OPERATE" en verde). El sintonizador automático no producirá un resultado útil si el sintonizador está en BYPASS o STANDBY.

## Pasos

1. Haga clic en el botón de la bandeja TUN en la barra lateral derecha para abrir la applet Tuner.
2. Confirme que el botón OPERATE muestre "OPERATE" (verde). Si muestra "BYPASS" o "STANDBY", haga clic en él hasta que aparezca "OPERATE".
3. Haga clic en TUNE.
4. Espere mientras el botón se vuelve rojo y muestra "TUNING...". No transmita manualmente durante este tiempo.
5. Cuando la sintonización se complete, el botón muestra brevemente el resultado — por ejemplo, "SWR 1.42" — durante aproximadamente 2,5 segundos, luego vuelve a "TUNE".
6. Revise el indicador SWR para confirmar el valor de SWR final estabilizado.

## Función de cada control

| Control | Descripción | Rango válido |
|---|---|---|
| TUNE | Inicia el ciclo de sintonización automática. Se vuelve rojo y muestra "TUNING..." mientras está activo. Muestra intermitentemente la SWR posterior a la sintonización durante 2,5 segundos al finalizar, luego se restablece a "TUNE". | — |
| OPERATE | Cicla el estado del sintonizador: OPERATE (verde) → BYPASS (naranja) → STANDBY → OPERATE. Debe estar en OPERATE para una sintonización significativa. | — |
| Fwd Pwr | Muestra la potencia directa reportada por el TGXL durante la sintonización. La escala depende de su configuración: 0–200 W sin amplificador, 0–600 W Aurora, 0–2000 W con PGXL. | 0–2000 W |
| SWR | Muestra la SWR reportada por el TGXL. El indicador se vuelve rojo por encima de 2.5. | 1.0–3.0 |
| C1 | Muestra la posición del banco de relés C1 después de que se complete la sintonización. | 0–255 |
| L | Muestra la posición del banco de relés L después de que se complete la sintonización. | 0–255 |
| C2 | Muestra la posición del banco de relés C2 después de que se complete la sintonización. | 0–255 |

## Consejos

- La SWR mostrada en el botón TUNE después de la sintonización refleja un valor estabilizado capturado hasta 400 ms después de que finaliza el ciclo de sintonización. Este es el valor final reportado por el TGXL, no una lectura de barrido intermedio.
- Si necesita leer la SWR posterior a la sintonización después de que haya expirado el destello de 2,5 segundos, observe directamente el indicador SWR.

## Solución de problemas

- **El botón de la bandeja TUN no aparece** — AetherSDR no ha detectado un TGXL. Verifique que el sintonizador esté encendido y comunicándose con la radio o directamente con AetherSDR.
- **El botón TUNE vuelve a "TUNE" inmediatamente sin mostrar un resultado de SWR** — Es posible que el sintonizador no estuviera en estado OPERATE, o que el ciclo de sintonización se haya completado sin devolver datos de SWR válidos. Confirme que el botón OPERATE muestre "OPERATE" (verde) antes de hacer clic en TUNE.
- **El indicador SWR se lee en rojo (por encima de 2.5) después de la sintonización** — El sintonizador no pudo encontrar una coincidencia satisfactoria. Verifique las conexiones de la antena y confirme que se encuentra dentro de una banda que cubre la antena.

## Relacionado

- [Leer la SWR inmediatamente después de una sintonización](read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del mouse](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Visión general del sintonizador](overview.md)
