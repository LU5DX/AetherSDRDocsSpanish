# Ejecutar un Ajuste Automático en el TGXL Externo

Esta página explica cómo iniciar un ciclo de ajuste automático en un 4O3A Tuner Genius XL conectado a su FLEX-8600. Use el ajuste automático para encontrar la mejor combinación de relés C1/L/C2 para su frecuencia y antena actuales.

## Antes de comenzar

- AetherSDR debe detectar el Tuner Genius XL. El botón TUN en la barra lateral derecha aparece únicamente cuando hay un TGXL presente.
- El radio debe estar conectado. El applet Tuner no está disponible sin una conexión activa al radio.
- Establezca su frecuencia de operación antes de ajustar. El TGXL se ajusta a la frecuencia de transmisión actual.
- Asegúrese de que el sintonizador no esté en STANDBY. El botón OPERATE debe mostrar "OPERATE" (verde) para que el ajuste automático sea efectivo.

## Pasos

1. Haga clic en el botón **TUN** de la barra lateral derecha para abrir el applet Tuner.
2. Confirme que el botón OPERATE muestre "OPERATE" (verde). Si muestra "BYPASS" o "STANDBY", haga clic en él hasta que regrese a "OPERATE".
3. Haga clic en **TUNE**.
4. El botón se pone rojo y muestra "TUNING..." mientras el ciclo de ajuste se ejecuta.
5. Cuando el ciclo termina, el botón muestra brevemente "SWR x.xx" — el valor de ROE estabilizado tras el ajuste — durante aproximadamente 2.5 segundos y luego regresa a "TUNE".

## Qué hace cada control

| Control | Descripción | Rango válido |
|---|---|---|
| **TUNE** | Inicia el ciclo de ajuste automático. Se pone rojo y muestra "TUNING..." durante el ajuste; destella el resultado final de ROE durante 2.5 s al terminar. | — |
| **Fwd Pwr** | Muestra la potencia hacia adelante reportada por el TGXL durante el pulso de ajuste. | 0–200 W (barefoot), 0–600 W (Aurora), 0–2000 W (con PGXL) |
| **SWR** | Muestra la ROE reportada por el TGXL en tiempo real. | 1.0–3.0 (rojo por encima de 2.5) |
| **C1** | Muestra la posición del banco de relés C1 después del ajuste. | 0–255 |
| **L** | Muestra la posición del banco de relés L después del ajuste. | 0–255 |
| **C2** | Muestra la posición del banco de relés C2 después del ajuste. | 0–255 |

## Consejos

- El valor de ROE que destella en el botón TUNE después de un ciclo es la lectura estabilizada capturada hasta 400 ms después de que el TGXL reporta que el ajuste ha concluido. Esto le da al sintonizador tiempo para reportar su valor final en lugar de una lectura tomada en medio del barrido.
- Observe las barras de relés C1, L y C2 para confirmar que el TGXL ha cambiado a una nueva red después del ajuste. Si las tres permanecen en 0, es posible que el sintonizador no haya actuado.

## Solución de problemas

- **El botón TUN no es visible** — El TGXL no ha sido detectado. Verifique la conexión física entre el FLEX-8600 y el TGXL, y confirme que el firmware del radio sea la versión 4.1.5.
- **El botón TUNE regresa a "TUNE" inmediatamente sin destellar un resultado de ROE** — El ciclo de ajuste se completó, pero no llegó ninguna lectura válida de ROE desde el TGXL. Verifique la conexión del TGXL y que el sintonizador esté en OPERATE, no en BYPASS o STANDBY.
- **El botón muestra "TUNING..." pero nunca termina** — El TGXL no reportó el fin del ajuste. Verifique la continuidad de RF — una antena abierta o en cortocircuito puede hacer que el sintonizador agote el tiempo de espera.

## Relacionados

- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Leer la ROE inmediatamente después de un ajuste](read-swr-immediately-after-a-tune.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
