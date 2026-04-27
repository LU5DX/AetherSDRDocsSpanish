# Ejecutar un ajuste automático en el TGXL externo

Esta página explica cómo iniciar un ciclo de sintonización automática en un 4O3A Tuner Genius XL conectado. Use el ajuste automático para encontrar la mejor combinación de relés C1/L/C2 para su frecuencia y antena actuales.

## Antes de comenzar

- AetherSDR debe haber detectado un Tuner Genius XL. El botón TUN en la bandeja del panel lateral derecho aparece únicamente cuando hay un TGXL presente.
- La radio debe estar conectada. El applet del sintonizador requiere una conexión de radio activa.
- El TGXL debe estar en estado OPERATE (el botón muestra "OPERATE" en verde). El ajuste automático no producirá un resultado útil si el sintonizador se encuentra en BYPASS o STANDBY.

## Pasos

1. Haga clic en el botón TUN de la bandeja del panel lateral derecho para abrir el applet del sintonizador.
2. Confirme que el botón OPERATE muestra "OPERATE" (verde). Si muestra "BYPASS" o "STANDBY", haga clic en él hasta que aparezca "OPERATE".
3. Haga clic en TUNE.
4. Espere mientras el botón se pone rojo y muestra "TUNING...". No transmita manualmente durante este tiempo.
5. Cuando la sintonización finalice, el botón muestra brevemente el resultado — por ejemplo, "SWR 1.42" — durante aproximadamente 2.5 segundos y luego vuelve a "TUNE".
6. Compruebe el indicador de SWR para confirmar el valor final de SWR estabilizado.

## Qué hace cada control

| Control | Descripción | Rango válido |
|---|---|---|
| TUNE | Inicia el ciclo de sintonización automática. Se pone rojo y muestra "TUNING..." mientras está activo. Muestra el SWR posterior a la sintonización durante 2.5 segundos al completarse y luego regresa a "TUNE". | — |
| OPERATE | Cambia el estado del sintonizador: OPERATE (verde) → BYPASS (naranja) → STANDBY → OPERATE. Debe estar en OPERATE para una sintonización con resultado válido. | — |
| Fwd Pwr | Muestra la potencia hacia adelante reportada por el TGXL durante la sintonización. La escala depende de su configuración: 0–200 W sin amplificador, 0–600 W Aurora, 0–2000 W con PGXL. | 0–2000 W |
| SWR | Muestra el SWR reportado por el TGXL. El indicador se pone rojo por encima de 2.5. | 1.0–3.0 |
| C1 | Muestra la posición del banco de relés C1 una vez completada la sintonización. | 0–255 |
| L | Muestra la posición del banco de relés L una vez completada la sintonización. | 0–255 |
| C2 | Muestra la posición del banco de relés C2 una vez completada la sintonización. | 0–255 |

## Consejos

- El SWR que aparece en el botón TUNE tras la sintonización refleja un valor estabilizado capturado hasta 400 ms después de que finaliza el ciclo de sintonización. Este es el valor final reportado por el TGXL, no una lectura tomada durante el barrido.
- Si necesita leer el SWR posterior a la sintonización una vez que hayan transcurrido los 2.5 segundos del destello, observe el indicador de SWR directamente.

## Solución de problemas

- **El botón TUN de la bandeja no aparece** — AetherSDR no ha detectado un TGXL. Verifique que el sintonizador esté encendido y que se esté comunicando con la radio o directamente con AetherSDR.
- **El botón TUNE vuelve a "TUNE" inmediatamente sin mostrar un resultado de SWR** — Es posible que el sintonizador no haya estado en estado OPERATE, o que el ciclo de sintonización haya finalizado sin devolver datos de SWR válidos. Confirme que el botón OPERATE muestre "OPERATE" (verde) antes de hacer clic en TUNE.
- **El indicador de SWR se muestra en rojo (por encima de 2.5) tras la sintonización** — El sintonizador no pudo encontrar una adaptación satisfactoria. Revise las conexiones de antena y confirme que se encuentra dentro de una banda que la antena cubre.

## Relacionado

- [Leer el SWR inmediatamente después de una sintonización](read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Descripción general del sintonizador](overview.md)
