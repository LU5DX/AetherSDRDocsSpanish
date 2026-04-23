# Descripción general del sintonizador

El applet Tuner le permite controlar un sintonizador de antena externo 4O3A Tuner Genius XL (TGXL) directamente desde AetherSDR. Desde un solo panel puede ejecutar un sintonizado automático, monitorear la potencia directa y la ROS, inspeccionar o ajustar las posiciones de los relés C1/L/C2, establecer el estado operativo del sintonizador y seleccionar entre tres puertos de antena.

## Antes de comenzar

- Conéctese a una radio Flex. El applet permanece oculto hasta que se detecta un Tuner Genius XL.
- Confirme que el TGXL está encendido y comunicándose con la radio o directamente con AetherSDR.

## Cómo funciona

Cuando se detecta un Tuner Genius XL, el botón `TUN` aparece en la barra lateral derecha. Haga clic en `TUN` para abrir o cerrar el applet Tuner.

El applet tiene tres secciones organizadas de arriba hacia abajo:

1. **Medidores de potencia y ROS** — lecturas en tiempo real reportadas por el TGXL.
2. **Barras de relés y botones de modo** — posiciones de los relés C1, L y C2 a la izquierda; botones TUNE y OPERATE/BYPASS/STANDBY a la derecha.
3. **Fila del conmutador de antenas** — botones ANT 1, ANT 2 y ANT 3. Esta fila permanece oculta a menos que haya una conexión directa con el TGXL activa y el TGXL reporte un conmutador de antenas.

El desplazamiento con la rueda del ratón en las barras de relés solo está habilitado cuando hay una conexión directa con el TGXL activa.

## Qué hace cada control

| Control | Tipo | Comportamiento | Rango / Estados |
|---|---|---|---|
| Fwd Pwr | Medidor | Muestra la potencia directa reportada por el TGXL. La escala se ajusta según la configuración de la radio y el amplificador. | 0–200 W (sin amplificador); 0–600 W (Aurora); 0–2000 W (con PGXL) |
| SWR | Medidor | Muestra la ROS reportada por el TGXL. El indicador se pone rojo por encima de 2.5. | 1.0–3.0 |
| C1 | Barra de relé | Muestra la posición del banco de relés C1. Desplace la rueda del ratón para ajustar (se requiere conexión directa). | 0–255 |
| L | Barra de relé | Muestra la posición del banco de relés L. Desplace la rueda del ratón para ajustar (se requiere conexión directa). | 0–255 |
| C2 | Barra de relé | Muestra la posición del banco de relés C2. Desplace la rueda del ratón para ajustar (se requiere conexión directa). | 0–255 |
| TUNE | Botón | Envía un comando de sintonizado automático al TGXL. El botón se pone rojo y muestra "TUNING..." durante el ciclo de sintonizado. Al finalizar, muestra brevemente la ROS capturada como "SWR x.xx" durante 2.5 segundos y luego vuelve a "TUNE". | TUNE / TUNING... / SWR x.xx |
| OPERATE | Botón | Cambia cíclicamente el estado del sintonizador: OPERATE (verde) → BYPASS (naranja) → STANDBY (predeterminado) → OPERATE. | OPERATE / BYPASS / STANDBY |
| ANT 1 | Botón | Selecciona el puerto de antena 1 en el conmutador 3x1 del TGXL. | — |
| ANT 2 | Botón | Selecciona el puerto de antena 2 en el conmutador 3x1 del TGXL. | — |
| ANT 3 | Botón | Selecciona el puerto de antena 3 en el conmutador 3x1 del TGXL. | — |

## Consejos

- El valor de ROS que se muestra después de un sintonizado se captura durante una ventana breve al finalizar el ciclo de sintonizado, dándole tiempo al TGXL para reportar su lectura final estabilizada. El valor mostrado refleja la ROS posterior al sintonizado, no la ROS máxima registrada durante el barrido.
- La fila del conmutador de antenas y el desplazamiento con la rueda del ratón en las barras de relés requieren ambos una conexión directa con el TGXL. Si no ve los botones ANT 1/2/3 o no puede desplazarse por las barras de relés, el applet se está comunicando a través de la radio en lugar de una conexión directa.

## Relacionados

- [Ejecutar un sintonizado automático en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Leer la ROS inmediatamente después de un sintonizado](read-swr-immediately-after-a-tune.md)
- [Cambiar entre tres antenas en un TGXL 3x1](switch-between-three-antennas-on-a-tgxl-3x1.md)
