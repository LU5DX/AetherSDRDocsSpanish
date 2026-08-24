# Lea la ROE inmediatamente después de una sintonización

Después de que finaliza el autosintonizador, el botón TUNE muestra brevemente el valor final de ROE estabilizado para que pueda confirmar la concordancia sin mirar el indicador de ROE.

## Antes de comenzar

- Debe haber un Tuner Genius XL de 4O3A conectado y detectado. El botón de bandeja TUN aparece en la barra lateral derecha solo cuando hay un TGXL presente.
- El applet del sintonizador debe estar abierto. Haga clic en el botón de bandeja TUN para abrirlo.
- El sintonizador debe estar en estado OPERATE (el botón OPERATE se muestra en verde).

## Pasos

1. Haga clic en TUNE.
2. Espere. El botón se pone rojo y muestra "TUNING..." mientras se ejecuta el barrido del autosintonizador.
3. Cuando la sintonización finaliza, el botón restaura su estilo normal y muestra brevemente "TUNING..." durante hasta 400 ms mientras AetherSDR captura el valor final de ROE estabilizado del TGXL.
4. El botón muestra entonces el resultado como "SWR x.xx" — por ejemplo, "SWR 1.34". Lea este valor directamente del botón.
5. Después de 2.5 segundos, la etiqueta del botón vuelve a "TUNE".

Si pierde el destello, el indicador de ROE continúa mostrando el valor de ROE en vivo reportado por el TGXL después de la sintonización. La escala del indicador solo se redibuja cuando las entradas relevantes para la escala (potencia o estado del amplificador) realmente cambian, por lo que la escala mostrada se mantiene estable durante la operación normal.

## Qué hace cada control

| Control | Tipo | Comportamiento | Rango válido |
|---|---|---|---|
| Fwd Pwr | Medidor | Muestra la potencia directa reportada por el TGXL. La escala es de 0–200 W sin amplificador, 0–600 W con amplificador Aurora, 0–2000 W con amplificador PGXL. La barra sube rápidamente con ráfagas de RF y decae en aproximadamente 800 ms para evitar parpadeos por ruido entre paquetes. Una marca blanca muestra el pico de potencia directa, que se borra después de 2.5 segundos sin nuevos picos. Tiene un nombre accesible de "Forward power" para lectores de pantalla. | Ver escala |
| SWR | Medidor | Muestra continuamente la ROE en vivo reportada por el TGXL. Se pone rojo por encima de 2.5. La barra sube rápidamente y decae en aproximadamente 800 ms. Una marca blanca muestra el pico de ROE, que se borra después de 2.5 segundos sin nuevos picos. Cuando la potencia directa es inferior a 5 W (piso de ruido), el indicador se fija en 1.0 (vacío) para evitar que el ruido en reposo ilumine la barra. Tiene un nombre accesible de "SWR" para lectores de pantalla. | 1.0–3.0 |
| C1 | Medidor | Muestra la posición del banco de relés C1. El desplazamiento de la rueda del ratón ajusta la posición del relé cuando hay una conexión TGXL directa activa. Tiene un nombre accesible de "Tuner capacitor C1" para lectores de pantalla. | 0–255 |
| L | Medidor | Muestra la posición del banco de relés L. El desplazamiento de la rueda del ratón ajusta la posición del relé. Tiene un nombre accesible de "Tuner inductor L" para lectores de pantalla. | 0–255 |
| C2 | Medidor | Muestra la posición del banco de relés C2. El desplazamiento de la rueda del ratón ajusta la posición del relé. Tiene un nombre accesible de "Tuner capacitor C2" para lectores de pantalla. | 0–255 |
| TUNE | Botón | Inicia el autosintonizador. Se pone rojo y muestra "TUNING..." durante el barrido. Muestra "SWR x.xx" durante 2.5 s después de la finalización. Vuelve a "TUNE" después. Cuando una conexión TGXL directa (puerto 9010) está configurada en Radio Setup → Tuner, el comando de autosintonía se envía directamente al TGXL, omitiendo la ruta del firmware de la radio. Vuelve a la ruta de la radio cuando no hay conexión directa disponible. | — |
| OPERATE | Botón | Cicla por tres estados: OPERATE (verde), BYPASS (naranja) y STANDBY (predeterminado). Cada clic avanza al siguiente estado. | — |
| ANT 1, ANT 2, ANT 3 | Botón | Selecciona el puerto de antena correspondiente en el conmutador 3x1 del TGXL. Estos botones aparecen solo cuando hay una conexión TGXL directa activa y el conmutador de antena está presente. | — |

## Consejos

- La ventana de captura de 400 ms después de la sintonización existe porque el valor final de ROE estabilizado del TGXL suele llegar por TCP ligeramente después de la señal de sintonización completada. El valor mostrado en el botón refleja esta lectura estabilizada, no una muestra a mitad del barrido.
- Si la ventana de captura expira antes de que llegue una lectura de ROE válida, AetherSDR recurre al último valor de ROE en vivo del indicador.
- La marca de retención de pico en los indicadores le ayuda a ver la potencia o ROE más alta alcanzada durante una transmisión, que se borra automáticamente después de 2.5 segundos.
- La decadencia lenta en las barras de los indicadores (800 ms) evita el molesto parpadeo que podría ocurrir por breves intervalos entre paquetes UDP.
- El indicador de ROE se restablece automáticamente a 1.0 cuando la potencia directa cae por debajo de 5 W, evitando que el ruido en reposo cause lecturas de ROE falsas.
- La escala del indicador de potencia directa se redibuja solo cuando la escala real cambia (por ejemplo, cuando se conecta o desconecta un amplificador), reduciendo redibujados innecesarios durante las actualizaciones de telemetría de rutina.

## Solución de problemas

- **El botón TUNE vuelve a "TUNE" sin mostrar un valor de ROE** — La transición del estado de sintonización no fue precedida por una sintonización activa (por ejemplo, el estado del modelo cambió externamente). Haga clic en TUNE nuevamente para ejecutar una autosintonía nueva.
- **El indicador de ROE marca por encima de 2.5 (rojo) después de la sintonización** — El sintonizador no pudo encontrar una concordancia satisfactoria en la banda y antena actuales. Verifique la conexión de la antena e intente nuevamente, o revise las posiciones de los relés C1, L y C2.

## Relacionados

- [Ejecute una autosintonía en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Ponga el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
