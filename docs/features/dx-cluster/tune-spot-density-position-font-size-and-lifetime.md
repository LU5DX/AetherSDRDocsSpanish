# Ajustar la densidad, posición, tamaño de fuente y duración de los spots

La pestaña Display en SpotHub controla cómo aparecen los spots en el panadapter: cuántos se apilan verticalmente, dónde se ubican, qué tan grande es el texto y cuánto tiempo permanecen visibles antes de desvanecerse. Ajuste estos parámetros para reducir el desorden visual o mejorar la legibilidad en su pantalla.

## Antes de comenzar

- Abra AetherSDR y confirme que al menos una fuente de spots esté activa (clúster DX, RBN, WSJT-X, POTA, SpotCollector o FreeDV).
- Confirme que la superposición de spots no esté deshabilitada — `IsSpotsEnabled` debe estar activado (consulte el control Spots más adelante).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Confirme que **Spots:** esté configurado en Enabled. Si muestra Disabled, haga clic para activarlo.
4. Para que AetherSDR ajuste automáticamente la densidad al hacer zoom, haga clic en **Auto Mode:** para habilitarlo. Omita los pasos 5–6 si utiliza Auto Mode.
5. Para configurar la densidad manualmente, arrastre el control deslizante **Levels:** hasta el número de filas de apilamiento vertical que desee.
6. Arrastre el control deslizante **Position:** para mover la fila de spots hacia arriba o hacia abajo en el panadapter.
7. Arrastre el control deslizante **Font Size:** para aumentar o reducir el tamaño del texto de las etiquetas de spots.
8. Arrastre el control deslizante **Spot Lifetime:** para definir cuántos segundos permanece visible un spot antes de desvanecerse.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Spots:** | Control principal para la superposición de spots en el panadapter. Valor predeterminado: Enabled. | `IsSpotsEnabled` |
| **Auto Mode:** | Ajusta automáticamente la densidad de spots según el nivel de zoom actual. | `SpotsAutoMode` |
| **Levels:** | Número de filas de apilamiento vertical que se usan cuando los spots se superponen en la misma frecuencia. | `SpotsStackLevels` |
| **Position:** | Posición vertical de la fila de spots en el panadapter. | `SpotsPosition` |
| **Font Size:** | Tamaño del texto de la etiqueta dibujada en cada spot. | `SpotsFontSize` |
| **Spot Lifetime:** | Segundos que un spot permanece en el panadapter antes de ser eliminado. | `SpotsLifetime` |

Nota: La pestaña **Display** también contiene controles de color personalizado y coloración DXCC que no se tratan aquí. Consulte las páginas relacionadas más abajo.

## Consejos

- Cuando **Auto Mode:** está habilitado, el control deslizante **Levels:** no tiene efecto. Deshabilite **Auto Mode:** primero si desea control manual sobre la densidad de apilamiento.
- Si el panadapter se ve congestionado con un zoom amplio, reduzca **Levels:** o aumente **Spot Lifetime:** solo hasta lo que requiera su tasa de spots. Una duración más corta también reduce el desorden cuando la tasa de spots es alta.
- Los spots de WSJT-X tienen su propia duración independiente, configurada mediante **Spot Life:** en la pestaña **WSJT-X**, almacenada en `WsjtxSpotLife`. El control deslizante **Spot Lifetime:** de la pestaña Display se aplica a todas las demás fuentes.

## Solución de problemas

- **No se ven spots en el panadapter a pesar de tener conexiones activas** — Verifique que **Spots:** en la pestaña Display esté en Enabled (`IsSpotsEnabled`). Confirme también que la banda correcta sea visible en el panadapter y que existan spots para esa banda en la pestaña **Spot List**.
- **Los spots desaparecen casi de inmediato** — El control deslizante **Spot Lifetime:** está configurado con un valor muy bajo. Arrástrelo hacia la derecha para aumentar la duración.
- **Los spots se apilan en una sola fila sin importar el valor de Levels:** — **Auto Mode:** está habilitado y anula el valor manual de Levels. Haga clic en **Auto Mode:** para deshabilitarlo y luego ajuste **Levels:**.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Habilitar coloración DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas propias](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
