# Descripción general del Tuner

El applet Tuner le permite controlar un acoplador de antena externo 4O3A Tuner Genius XL (TGXL) directamente desde AetherSDR. Desde un solo panel puede ejecutar un autoajuste, monitorear la potencia directa y el ROS, ajustar los bancos de relés individuales, cambiar entre puertos de antena y establecer el estado de operación del acoplador.

## Cómo funciona

El applet Tuner permanece oculto hasta que AetherSDR detecta un TGXL conectado. Cuando el acoplador está presente, haga clic en el botón TUN de la barra lateral derecha para mostrar u ocultar el applet.

El applet tiene tres áreas funcionales dispuestas de arriba hacia abajo:

**Medidores de potencia y ROS** — Dos indicadores horizontales en la parte superior muestran lecturas en tiempo real reportadas por el TGXL. La escala de potencia directa se ajusta automáticamente según la configuración de su radio y amplificador (consulte la tabla a continuación). El indicador de ROS se vuelve rojo por encima de 2.5.

**Barras de relés y botones de control** — El área de barras de relés y los botones TUNE / OPERATE ocupan la parte inferior en paralelo. Las barras C1, L y C2 muestran las posiciones actuales de los bancos de relés. Cuando hay una conexión directa al TGXL activa, puede desplazar la rueda del ratón sobre cualquier barra para incrementar o decrementar ese banco de relés. Los botones TUNE y OPERATE siempre son visibles.

**Fila de selección de antena** — Una fila de tres botones de antena (ANT 1, ANT 2, ANT 3) aparece debajo de las barras de relés únicamente cuando hay una conexión directa al TGXL activa y el TGXL informa que hay un conmutador de antena 3x1 presente. De lo contrario, la fila permanece oculta.

## Qué hace cada control

| Control | Tipo | Comportamiento | Rango / Estados |
|---|---|---|---|
| Fwd Pwr | Medidor | Muestra la potencia directa reportada por el TGXL. La escala se ajusta según la configuración de radio/amplificador. | 0–200 W sin amplificador; 0–600 W Aurora; 0–2000 W con PGXL |
| SWR | Medidor | Muestra el ROS reportado por el TGXL. El indicador se vuelve rojo por encima de 2.5. | 1.0–3.0 |
| C1 | Barra de relé | Muestra la posición del banco de relés C1. El desplazamiento con la rueda del ratón ajusta el relé cuando hay una conexión directa al TGXL activa. | 0–255 |
| L | Barra de relé | Muestra la posición del banco de relés L. El desplazamiento con la rueda del ratón ajusta el relé cuando hay una conexión directa al TGXL activa. | 0–255 |
| C2 | Barra de relé | Muestra la posición del banco de relés C2. El desplazamiento con la rueda del ratón ajusta el relé cuando hay una conexión directa al TGXL activa. | 0–255 |
| TUNE | Botón | Envía un comando de autoajuste al TGXL. El botón se vuelve rojo y muestra "TUNING..." durante el ajuste. Al finalizar, muestra el ROS logrado como "SWR x.xx" durante 2.5 segundos y luego regresa a "TUNE". | TUNE / TUNING... / SWR x.xx |
| OPERATE | Botón | Cambia el estado de los relés del TGXL. Cada clic avanza al siguiente estado: OPERATE (verde) → BYPASS (naranja) → STANDBY (predeterminado) → OPERATE. | OPERATE / BYPASS / STANDBY |
| ANT 1 | Botón | Selecciona el puerto de antena 1 en el conmutador 3x1 del TGXL. Visible solo cuando hay una conexión directa al TGXL activa y hay un conmutador de antena presente. | — |
| ANT 2 | Botón | Selecciona el puerto de antena 2. | — |
| ANT 3 | Botón | Selecciona el puerto de antena 3. | — |

## Consejos

- La escala de potencia directa se establece automáticamente. La operación sin amplificador utiliza una escala de 0–200 W con umbral rojo en 125 W. Un amplificador Aurora cambia la escala a 0–600 W (rojo por encima de 500 W). Un amplificador PGXL utiliza 0–2000 W (rojo por encima de 1500 W).
- El ajuste de relés con la rueda del ratón en C1, L y C2 solo está disponible cuando hay una conexión directa al TGXL activa. Si el desplazamiento no tiene efecto, el tipo de conexión no admite control manual de relés.
- Tras completar un ajuste, AetherSDR espera brevemente antes de mostrar el ROS final, para permitir que llegue desde el TGXL la lectura estabilizada posterior al ajuste.

## Relacionados

- [Ejecutar un autoajuste en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el acoplador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Cambiar entre tres antenas en un TGXL 3x1](switch-between-three-antennas-on-a-tgxl-3x1.md)
- [Leer el ROS inmediatamente después de un ajuste](read-swr-immediately-after-a-tune.md)
