# Ajustar densidad, posición, tamaño de fuente y duración de los spots

La pestaña Display de SpotHub controla cómo aparecen los spots en el panadapter: cuántos se apilan verticalmente, dónde se ubican, qué tan grande es el texto y cuánto tiempo permanece visible cada spot antes de desvanecerse. Ajuste estos parámetros para reducir el desorden visual o para que los spots sean más fáciles de leer de un vistazo.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para ajustar los parámetros de visualización.
- Al menos una fuente de spots (clúster DX, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe estar configurada para que pueda ver el efecto de los cambios en tiempo real.
- La superposición de spots debe estar habilitada (`IsSpotsEnabled` establecido en Enabled) para que los spots aparezcan en el panadapter.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Confirme que **Spots:** está establecido en Enabled. Si no es así, haga clic en él para habilitar la superposición.
4. Para controlar cuántas filas verticales pueden ocupar los spots, arrastre el control deslizante **Levels:**. Más niveles permiten que los spots se apilen sin solaparse; menos niveles mantienen la superposición compacta.
5. Para que AetherSDR ajuste automáticamente la densidad de apilamiento según el nivel de zoom actual del panadapter, haga clic en **Auto Mode:** para habilitarlo. Cuando Auto Mode está activo, el control deslizante **Levels:** no tiene efecto.
6. Para mover toda la superposición de spots hacia arriba o hacia abajo en el panadapter, arrastre el control deslizante **Position:**.
7. Para cambiar el tamaño del texto del indicativo de llamada de cada spot, arrastre el control deslizante **Font Size:**.
8. Para cambiar cuánto tiempo permanece visible un spot antes de desaparecer, arrastre el control deslizante **Spot Lifetime:**. El valor se expresa en segundos.

## Qué hace cada control

| Control | Función | Parámetro guardado |
|---|---|---|
| **Spots:** | Interruptor principal de la superposición de spots en el panadapter. Valor predeterminado: Enabled. | `IsSpotsEnabled` |
| **Auto Mode:** | Cuando está habilitado, AetherSDR ajusta automáticamente la densidad de apilamiento según el zoom. Anula **Levels:**. | `SpotsAutoMode` |
| **Levels:** | Número de filas verticales de apilamiento para los spots. No tiene efecto mientras Auto Mode está activo. | `SpotsStackLevels` |
| **Position:** | Posición vertical de la superposición de spots en el panadapter. | `SpotsPosition` |
| **Font Size:** | Tamaño del texto del indicativo de llamada en cada marcador de spot. | `SpotsFontSize` |
| **Spot Lifetime:** | Segundos que un spot permanece visible en el panadapter antes de desvanecerse. | `SpotsLifetime` |

## Consejos

- Si los spots se solapan entre sí con su nivel de zoom habitual, aumente **Levels:** o habilite **Auto Mode:** para que AetherSDR encuentre la profundidad de apilamiento óptima para la vista actual.
- Si la superposición oculta detalles de la señal, reduzca **Levels:** a una o dos filas y use **Position:** para desplazar los spots hacia el borde superior o inferior del panadapter.
- WSJT-X tiene su propio control de duración por fuente (**Spot Life:** en la pestaña WSJT-X, guardado como `WsjtxSpotLife`). El control deslizante **Spot Lifetime:** de la pestaña Display se aplica a todas las demás fuentes.

## Solución de problemas

- **Los spots están conectados pero no aparece nada en el panadapter** — Verifique que **Spots:** en la pestaña Display muestre Enabled. Si está deshabilitado, haga clic en él para activar la superposición.
- **Cambiar Levels: no tiene efecto visible** — Es probable que **Auto Mode:** esté habilitado. Haga clic en **Auto Mode:** para deshabilitarlo y luego ajuste **Levels:**.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
- [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
