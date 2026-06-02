# Ejecutar un Sintonizador Automático en el TGXL Externo

Esta página explica cómo iniciar un ciclo de sintonización automática en un 4O3A Tuner Genius XL conectado. Use el sintonizador automático para encontrar la mejor combinación de relés C1/L/C2 para su frecuencia y antena actuales.

## Antes de comenzar

- AetherSDR debe detectar un Tuner Genius XL. El botón de la bandeja TUN aparece en la barra lateral derecha solo cuando hay un TGXL presente.
- La radio debe estar conectada. El applet del sintonizador requiere una conexión activa con la radio.
- El TGXL debe estar en estado OPERATE (el botón muestra "OPERATE" en verde). El sintonizador automático no producirá un resultado útil si el sintonizador está en BYPASS o STANDBY.

## Pasos

1. Haga clic en el botón de la bandeja TUN en la barra lateral derecha para abrir el applet del sintonizador.
2. Confirme que el botón OPERATE muestre "OPERATE" (verde). Si muestra "BYPASS" o "STANDBY", haga clic en él hasta que aparezca "OPERATE".
3. Haga clic en TUNE.
4. Espere mientras el botón se vuelve rojo y muestra "TUNING...". No transmita manualmente durante este tiempo.
5. Cuando la sintonización finalice, el botón mostrará brevemente el resultado —por ejemplo, "SWR 1.42"— durante aproximadamente 2.5 segundos, y luego volverá a "TUNE".
6. Verifique el indicador SWR para confirmar el valor final de SWR estabilizado.

## Función de cada control

| Control | Descripción | Rango válido |
|---|---|---|
| TUNE | Inicia el ciclo de sintonización automática. Se vuelve rojo y muestra "TUNING..." mientras está activo. Al finalizar, muestra el SWR posterior a la sintonización durante 2.5 segundos y luego vuelve a "TUNE". Desde v0.9.2.1, cuando se configura una conexión directa al TGXL (puerto 9010), envía el comando nativo "autotune" directamente al TGXL en lugar de enrutarlo a través del firmware de la radio. Configure esto en **Radio Setup → Tuner**. Utiliza la ruta de la radio como alternativa cuando no hay una conexión directa disponible. | — |
| OPERATE | Cambia el estado del sintonizador: OPERATE (verde) → BYPASS (naranja) → STANDBY → OPERATE. Debe estar en OPERATE para una sintonización significativa. | — |
| ANT 1, ANT 2, ANT 3 | Selecciona el puerto de antena 1, 2 o 3 en el conmutador 3x1 del TGXL. Fila oculta a menos que la conexión directa al TGXL esté activa y el conmutador de antena esté presente. | — |
| PWR | Muestra la potencia directa reportada por el TGXL. La escala depende de su configuración: 0–200 W sin amplificador (amarillo > 80 W, rojo > 125 W), 0–600 W Aurora (amarillo > 400 W, rojo > 500 W), 0–2000 W con PGXL (amarillo > 1000 W, rojo > 1500 W). Las etiquetas se actualizan en tiempo real; el texto se borra 800 ms después de que la potencia caiga por debajo del umbral para evitar parpadeos. | 0–2000 W |
| SWR | Muestra la SWR reportada por el TGXL. El indicador se vuelve rojo por encima de 2.5. Las etiquetas se actualizan en tiempo real; el texto se borra 800 ms después de que la SWR caiga por debajo del umbral para evitar parpadeos. | 1.0–3.0 |
| C1 | Muestra la posición del banco de relés C1; la rueda del mouse ajusta el relé cuando la conexión directa al TGXL está activa. | 0–255 |
| L | Muestra la posición del banco de relés L; la rueda del mouse ajusta el relé cuando la conexión directa al TGXL está activa. | 0–255 |
| C2 | Muestra la posición del banco de relés C2; la rueda del mouse ajusta el relé cuando la conexión directa al TGXL está activa. | 0–255 |

## Consejos

- La SWR mostrada en el botón TUNE después de la sintonización refleja un valor estabilizado capturado hasta 400 ms después de que finaliza el ciclo. Esta es la cifra final reportada por el TGXL, no una lectura durante el barrido.
- Si necesita leer la SWR posterior a la sintonización después de que hayan pasado los 2.5 segundos de visualización, observe directamente el indicador SWR.
- El indicador PWR tiene un comportamiento "balístico": la barra sube rápidamente con los picos de RF, pero decae durante aproximadamente 800 ms, proporcionando una lectura suave.
- Aparece un marcador de retención de pico (marca blanca) en el indicador PWR en el nivel de potencia directa más alto observado. Se borra automáticamente después de 2.5 segundos sin nuevos picos.

## Solución de problemas

- **El botón de la bandeja TUN no aparece** — AetherSDR no ha detectado un TGXL. Verifique que el sintonizador esté encendido y comunicándose con la radio o directamente con AetherSDR.
- **El botón TUNE vuelve a "TUNE" inmediatamente sin mostrar un resultado de SWR** — Es posible que el sintonizador no estuviera en estado OPERATE, o que el ciclo de sintonización finalizara sin devolver datos de SWR válidos. Confirme que el botón OPERATE muestre "OPERATE" (verde) antes de hacer clic en TUNE.
- **El indicador SWR se muestra en rojo (por encima de 2.5) después de la sintonización** — El sintonizador no pudo encontrar una adaptación satisfactoria. Verifique las conexiones de la antena y confirme que se encuentra dentro de una banda que cubra la antena.

## Relacionados

- [Leer la SWR inmediatamente después de una sintonización](read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del mouse](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Resumen del sintonizador](overview.md)
