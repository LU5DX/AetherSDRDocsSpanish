# Ajustar densidad, posición, tamaño de fuente y duración de los spots

La pestaña Display de SpotHub controla cómo aparecen las etiquetas de spots en el panadapter: cuántas se apilan verticalmente, dónde se ubican, qué tan grande es el texto y cuánto tiempo permanece visible cada spot antes de desvanecerse. Ajuste estos parámetros para reducir la saturación visual en una banda concurrida o para hacer los spots más legibles en una pantalla pequeña.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a la radio para modificar estos ajustes.
- Al menos una fuente de spots (clúster DX, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe estar activa para que pueda ver el efecto de los cambios en tiempo real.
- La superposición principal de spots debe estar activada. En la pestaña Display, confirme que `IsSpotsEnabled` esté activo (el botón "Spots:" muestra Enabled).

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Confirme que **Spots:** esté en Enabled. Si no lo está, haga clic en él para activar la superposición.
4. Para controlar cuántos spots se apilan verticalmente antes de superponerse, arrastre el control deslizante **Levels:**. Los valores más altos permiten más filas de etiquetas de spots.
5. Para mover las etiquetas de spots hacia arriba o hacia abajo en el panadapter, arrastre el control deslizante **Position:**.
6. Para cambiar el tamaño del texto de las etiquetas de spots, arrastre el control deslizante **Font Size:**.
7. Para establecer cuánto tiempo permanece visible un spot antes de desaparecer, arrastre el control deslizante **Spot Lifetime:**. El valor se expresa en segundos.
8. Si desea que AetherSDR ajuste automáticamente la densidad de spots según el nivel de zoom actual del panadapter, haga clic en **Auto Mode:** para activarlo. Cuando Auto Mode está activado, el control deslizante **Levels:** no tiene efecto.
9. Cierre el diálogo. Los cambios surten efecto de inmediato.

## Qué hace cada control

| Control | Clave de ajuste | Comportamiento | Valor predeterminado | Rango/Unidades |
|---|---|---|---|---|
| **Spots:** | `IsSpotsEnabled` | Interruptor principal de la superposición de spots en el panadapter. | Enabled | On / Off |
| **Auto Mode:** | `SpotsAutoMode` | Ajusta automáticamente la densidad de spots según el nivel de zoom. Anula Levels. | — | On / Off |
| **Levels:** | `SpotsStackLevels` | Número de filas de apilamiento vertical para las etiquetas de spots. | — | Deslizador |
| **Position:** | `SpotsPosition` | Posición vertical de la banda de etiquetas de spots en el panadapter. | — | Deslizador |
| **Font Size:** | `SpotsFontSize` | Tamaño del texto en cada etiqueta de spot. | — | Deslizador |
| **Spot Lifetime:** | `SpotsLifetime` | Segundos que permanece visible una etiqueta de spot antes de desvanecerse. | — | Segundos (deslizador) |

## Sugerencias

- Si las etiquetas de spots se superponen en exceso en una banda concurrida, aumente **Levels:** para agregar más filas de apilamiento, o disminuya **Spot Lifetime:** para que los spots antiguos desaparezcan más rápido.
- **Auto Mode:** es útil cuando alterna con frecuencia entre vistas con mucho y poco zoom. Desactívelo si prefiere controlar manualmente la densidad.
- Los spots de WSJT-X tienen su propio ajuste de duración por fuente (**Spot Life:** en la pestaña WSJT-X, almacenado como `WsjtxSpotLife`). El control deslizante **Spot Lifetime:** de la pestaña Display se aplica a todas las demás fuentes.

## Solución de problemas

- **Las etiquetas de spots no son visibles en absoluto** — Verifique que **Spots:** en la pestaña Display esté en Enabled (`IsSpotsEnabled`). Confirme también que al menos una fuente de spots esté conectada y recibiendo spots.
- **Cambiar Levels: no tiene efecto** — Es probable que **Auto Mode:** esté activado. Haga clic en **Auto Mode:** para desactivarlo y luego ajuste **Levels:** manualmente.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Seleccionar colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
