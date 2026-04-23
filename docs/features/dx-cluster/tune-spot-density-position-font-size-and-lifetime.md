# Ajustar la densidad, posición, tamaño de fuente y tiempo de vida de los spots

Use la pestaña **Display** en SpotHub para controlar cuántas etiquetas de spot aparecen en el panadapter, su posición vertical, el tamaño del texto y cuánto tiempo permanece visible cada spot antes de desvanecerse.

## Antes de comenzar

- Abra AetherSDR y asegúrese de que al menos una fuente de spots esté configurada (clúster DX, RBN, WSJT-X, POTA, SpotCollector o FreeDV).
- Los spots deben estar habilitados: el interruptor `IsSpotsEnabled` debe estar activado (valor predeterminado: Enabled).

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo de SpotHub.
2. Haga clic en la pestaña **Display**.
3. Confirme que el interruptor **Spots:** muestra **Enabled**. Si no es así, haga clic en él para habilitar la superposición de spots.
4. Para que AetherSDR ajuste automáticamente la densidad de spots al hacer zoom en el panadapter, haga clic en **Auto Mode:** para activarlo. Omita los pasos 5 y 6 si usa Auto Mode.
5. Para ajustar la densidad manualmente, arrastre el control deslizante **Levels:** para elegir el número de filas de apilamiento vertical para los spots.
6. Arrastre el control deslizante **Position:** para mover el bloque de filas de spots hacia arriba o hacia abajo en el panadapter.
7. Arrastre el control deslizante **Font Size:** para aumentar o disminuir el tamaño del texto de las etiquetas de spot.
8. Arrastre el control deslizante **Spot Lifetime:** para establecer cuántos segundos permanece visible un spot antes de desvanecerse.

## Qué hace cada control

| Control | Función | Clave persistida |
|---|---|---|
| **Spots:** | Interruptor principal de la superposición de spots. Valor predeterminado: Enabled. | `IsSpotsEnabled` |
| **Auto Mode:** | Ajusta automáticamente la densidad de spots según el nivel de zoom del panadapter. | `SpotsAutoMode` |
| **Levels:** | Número de filas de apilamiento vertical utilizadas cuando los spots se agrupan en frecuencias cercanas. | `SpotsStackLevels` |
| **Position:** | Posición vertical de la superposición de spots en el panadapter. | `SpotsPosition` |
| **Font Size:** | Tamaño del texto utilizado para las etiquetas de spot. | `SpotsFontSize` |
| **Spot Lifetime:** | Segundos que un spot permanece en el panadapter antes de ser eliminado. | `SpotsLifetime` |

## Consejos

- Cuando **Auto Mode:** está habilitado, el control deslizante **Levels:** no tiene efecto. Deshabilite **Auto Mode:** primero si desea controlar manualmente la densidad de apilamiento.
- La fuente WSJT-X tiene su propia configuración independiente de tiempo de vida de spots (**Spot Life:** en la pestaña WSJT-X), almacenada como `WsjtxSpotLife`. Ajustar **Spot Lifetime:** en la pestaña Display no afecta los spots de WSJT-X.
- Si el panadapter se ve saturado en una frecuencia de concurso con mucha actividad, reduzca **Levels:** o acorte **Spot Lifetime:** en lugar de deshabilitar los spots por completo.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Seleccionar colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Iniciar el listener UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Eliminar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
