# Ejecutar un autotune en el TGXL externo

Esta página explica cómo iniciar un ciclo de sintonización automática en un 4O3A Tuner Genius XL conectado. Use el autotune para encontrar la mejor combinación de relés C1/L/C2 para su frecuencia y antena actuales.

## Antes de comenzar

- AetherSDR debe detectar un Tuner Genius XL. El botón de bandeja TUN aparece en la barra lateral derecha solo cuando hay un TGXL presente.
- La radio debe estar conectada. El applet Tuner requiere una conexión de radio activa.
- El TGXL debe estar en estado OPERATE (el botón muestra "OPERATE" en verde). El autotune no producirá un resultado útil si el sintonizador está en BYPASS o STANDBY.

## Pasos

1. Haga clic en el botón de bandeja TUN en la barra lateral derecha para abrir el applet Tuner.
2. Confirme que el botón OPERATE muestra "OPERATE" (verde). Si muestra "BYPASS" o "STANDBY", haga clic en él hasta que aparezca "OPERATE".
3. Haga clic en TUNE.
4. Espere mientras el botón se pone rojo y muestra "TUNING...". No transmita manualmente durante este tiempo.
5. Cuando la sintonización se complete, el botón mostrará brevemente el resultado — por ejemplo, "SWR 1.42" — durante aproximadamente 2,5 segundos, y luego volverá a "TUNE".
6. Verifique el medidor de SWR para confirmar el valor final estabilizado de SWR.

## Qué hace cada control

| Control | Descripción | Rango válido |
|---|---|---|
| TUNE | Inicia el ciclo de autotune. Se pone rojo y muestra "TUNING..." mientras está activo. Parpadea con el SWR posterior a la sintonización durante 2,5 segundos al completarse, y luego se restablece a "TUNE". Desde la versión 0.9.2.1, cuando se configura una conexión directa al TGXL (puerto 9010), envía el comando nativo "autotune" directamente al TGXL en lugar de enrutarlo a través de la ruta de firmware de la radio. Configúrelo en **Radio Setup → Tuner**. Vuelve a la ruta de la radio cuando no hay una conexión directa disponible. | — |
| OPERATE | Cicla el estado del sintonizador: OPERATE (verde) → BYPASS (naranja) → STANDBY → OPERATE. Debe estar en OPERATE para que la sintonización sea significativa. | — |
| ANT 1, ANT 2, ANT 3 | Selecciona el puerto de antena 1, 2 o 3 en el conmutador 3x1 del TGXL. La fila se oculta a menos que la conexión directa al TGXL esté activa y el conmutador de antena esté presente. | — |
| Fwd Pwr | Muestra la potencia directa informada por el TGXL. La escala depende de su configuración: 0–200 W sin amplificador, 0–600 W Aurora, 0–2000 W con PGXL. La escala de potencia se establece automáticamente según la radio y el amplificador conectados, y solo se actualiza cuando cambia la configuración correspondiente. El medidor tiene comportamiento balístico: la barra sube rápidamente con ráfagas de RF pero decae en aproximadamente 800 ms. El marcador de retención de pico (marca blanca) aparece en la potencia directa más alta observada; se borra después de 2,5 segundos sin nuevos picos. Cuando la potencia directa es inferior a 5 W, el medidor lee cero para evitar que el ruido de reposo encienda la barra. | 0–2000 W |
| SWR | Muestra el SWR informado por el TGXL. El medidor se pone rojo por encima de 2.5. Cuando la potencia directa es inferior a 5 W, el medidor de SWR se fija en 1.0 (vacío) para evitar que las lecturas de ruido de reposo enciendan la barra. El medidor se actualiza normalmente cuando la potencia directa es de 5 W o superior. | 1.0–3.0 |
| C1 | Muestra la posición del banco de relés C1; el desplazamiento de la rueda del mouse ajusta el relé cuando la conexión directa al TGXL está activa. Nombre accesible: "Tuner capacitor C1". | 0–255 |
| L | Muestra la posición del banco de relés L; el desplazamiento de la rueda del mouse ajusta el relé cuando la conexión directa al TGXL está activa. Nombre accesible: "Tuner inductor L". | 0–255 |
| C2 | Muestra la posición del banco de relés C2; el desplazamiento de la rueda del mouse ajusta el relé cuando la conexión directa al TGXL está activa. Nombre accesible: "Tuner capacitor C2". | 0–255 |

## Consejos

- El SWR mostrado en el botón TUNE después de la sintonización refleja un valor estabilizado capturado hasta 400 ms después de que finaliza el ciclo de sintonización. Esta es la cifra final informada por el TGXL, no una lectura intermedia del barrido.
- Si necesita leer el SWR posterior a la sintonización después de que haya expirado el parpadeo de 2,5 segundos, observe directamente el medidor de SWR.
- El medidor Fwd Pwr tiene comportamiento "balístico": la barra sube rápidamente con ráfagas de RF pero decae en aproximadamente 800 ms, lo que proporciona una lectura suave.
- Un marcador de retención de pico (marca blanca) aparece en el medidor Fwd Pwr en el nivel de potencia directa más alto observado. Se borra automáticamente después de 2,5 segundos sin nuevos picos.
- El medidor de SWR se establece automáticamente en 1.0 cuando la potencia directa es inferior a 5 W, lo que evita que el ruido de reposo muestre una lectura de SWR falsamente alta.

## Solución de problemas

- **El botón de bandeja TUN no aparece** — AetherSDR no ha detectado un TGXL. Verifique que el sintonizador esté encendido y comunicándose con la radio o directamente con AetherSDR.
- **El botón TUNE vuelve inmediatamente a "TUNE" sin mostrar un resultado de SWR** — Es posible que el sintonizador no estuviera en estado OPERATE, o que el ciclo de sintonización se completara sin devolver datos de SWR válidos. Confirme que el botón OPERATE muestre "OPERATE" (verde) antes de hacer clic en TUNE.
- **El medidor de SWR lee rojo (por encima de 2.5) después de la sintonización** — El sintonizador no pudo encontrar una concordancia satisfactoria. Verifique las conexiones de la antena y confirme que está dentro de una banda que la antena cubre.
- **El medidor de SWR muestra 1.0 incluso cuando espera una lectura más alta** — Verifique que su potencia directa sea superior a 5 W. El medidor de SWR está diseñado para mostrar 1.0 (vacío) siempre que la potencia directa sea inferior a 5 W para evitar que el ruido de reposo encienda la barra.

## Relacionados

- [Leer el SWR inmediatamente después de una sintonización](read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del mouse](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Descripción general del sintonizador](overview.md)
