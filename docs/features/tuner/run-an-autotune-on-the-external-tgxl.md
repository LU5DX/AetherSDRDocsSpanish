# Ejecutar un sintonizado automático en el TGXL externo

Esta página explica cómo iniciar un ciclo de sintonización automática en un 4O3A Tuner Genius XL conectado. Use el sintonizado automático para encontrar la mejor combinación de relés C1/L/C2 para su frecuencia y antena actuales.

## Antes de comenzar

- AetherSDR debe haber detectado un Tuner Genius XL. El botón TUN en la bandeja aparece en la barra lateral derecha únicamente cuando hay un TGXL presente.
- La radio debe estar conectada. El applet Tuner requiere una conexión de radio activa.
- El TGXL debe estar en estado OPERATE (el botón muestra "OPERATE" en verde). El sintonizado automático no producirá un resultado útil si el sintonizador está en BYPASS o STANDBY.

## Pasos

1. Haga clic en el botón TUN de la barra lateral derecha para abrir el applet Tuner.
2. Confirme que el botón OPERATE muestra "OPERATE" (verde). Si muestra "BYPASS" o "STANDBY", haga clic en él hasta que aparezca "OPERATE".
3. Haga clic en TUNE.
4. Espere mientras el botón se pone rojo y muestra "TUNING...". No transmita manualmente durante este tiempo.
5. Cuando la sintonización finaliza, el botón muestra brevemente el resultado — por ejemplo, "SWR 1.42" — durante aproximadamente 2.5 segundos y luego regresa a "TUNE".
6. Verifique el indicador de SWR para confirmar el valor final de SWR estabilizado.

## Qué hace cada control

| Control | Descripción | Rango válido |
|---|---|---|
| TUNE | Inicia el ciclo de sintonización automática. Se pone rojo y muestra "TUNING..." mientras está activo. Destella el SWR posterior a la sintonización durante 2.5 segundos al completarse y luego regresa a "TUNE". | — |
| OPERATE | Cambia el estado del sintonizador: OPERATE (verde) → BYPASS (naranja) → STANDBY → OPERATE. Debe estar en OPERATE para una sintonización significativa. | — |
| Fwd Pwr | Muestra la potencia directa reportada por el TGXL durante la sintonización. La escala depende de su configuración: 0–200 W sin amplificador, 0–600 W Aurora, 0–2000 W con PGXL. | 0–2000 W |
| SWR | Muestra el SWR reportado por el TGXL. El indicador se pone rojo por encima de 2.5. | 1.0–3.0 |
| C1 | Muestra la posición del banco de relés C1 después de que finaliza la sintonización. | 0–255 |
| L | Muestra la posición del banco de relés L después de que finaliza la sintonización. | 0–255 |
| C2 | Muestra la posición del banco de relés C2 después de que finaliza la sintonización. | 0–255 |

## Consejos

- El SWR que se muestra en el botón TUNE después de la sintonización refleja un valor estabilizado capturado hasta 400 ms después de que finaliza el ciclo de sintonización. Este es el valor final reportado por el TGXL, no una lectura tomada a mitad del barrido.
- Si necesita leer el SWR posterior a la sintonización después de que hayan transcurrido los 2.5 segundos del destello, observe directamente el indicador de SWR.

## Solución de problemas

- **El botón TUN de la bandeja no aparece** — AetherSDR no ha detectado un TGXL. Compruebe que el sintonizador esté encendido y comunicándose con la radio o directamente con AetherSDR.
- **El botón TUNE regresa a "TUNE" inmediatamente sin mostrar un resultado de SWR** — Es posible que el sintonizador no estuviera en estado OPERATE, o que el ciclo de sintonización se haya completado sin que se devolvieran datos de SWR válidos. Confirme que el botón OPERATE muestra "OPERATE" (verde) antes de hacer clic en TUNE.
- **El indicador de SWR muestra rojo (por encima de 2.5) después de la sintonización** — El sintonizador no pudo encontrar una adaptación satisfactoria. Verifique las conexiones de la antena y confirme que está dentro de una banda que la antena cubre.

## Relacionados

- [Leer el SWR inmediatamente después de una sintonización](read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Descripción general del sintonizador](overview.md)
