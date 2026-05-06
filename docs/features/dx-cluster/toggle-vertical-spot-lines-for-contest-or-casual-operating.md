# Activar o desactivar las líneas verticales de spots para concursos u operación casual

De forma predeterminada, AetherSDR traza una línea vertical desde la base del espectro hasta cada etiqueta de spot en el panadapter. Esta página explica cómo desactivar esas líneas — útil durante concursos cuando la pantalla se satura — y cómo volver a activarlas para la operación casual.

## Antes de comenzar

- Al menos una fuente de spots (clúster DX, RBN, WSJT-X, POTA, SpotCollector o FreeDV) debe estar configurada y entregando spots; de lo contrario, el cambio no será visible.
- La superposición maestra de spots debe estar activa (`IsSpotsEnabled` configurado en Enabled). Si los spots están desactivados, las líneas de spots no tienen efecto visible.

## Pasos

Hay dos formas de acceder al control de alternancia "Spot Lines:". Use la que le resulte más conveniente.

**Mediante SpotHub:**

1. Haga clic en `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en **Spot Lines:** para alternarlo. El botón muestra **Enabled** (líneas visibles) o **Disabled** (líneas ocultas). El cambio surte efecto de inmediato.

**Mediante Spot Settings:**

1. Haga clic derecho sobre la superposición de spots del panadapter para abrir el menú contextual y seleccione la opción de configuración de spots, lo que abre la ventana **Spot Settings**.
2. Haga clic en **Spot Lines:** para alternarlo. El botón muestra **Enabled** o **Disabled**. El cambio surte efecto de inmediato.

## Qué hace cada control

| Control | Valor predeterminado | Clave de configuración | Comportamiento |
|---|---|---|---|
| **Spot Lines:** | Enabled | `IsSpotsLinesEnabled` | Cuando está en Enabled, traza una línea vertical desde la base del espectro hasta cada etiqueta de spot. Cuando está en Disabled, las etiquetas de spot aparecen sin líneas. |

## Consejos

- Desactive **Spot Lines:** antes de una sesión de concurso. Con decenas o cientos de spots en pantalla, eliminar las líneas reduce significativamente el ruido visual.
- Reactive **Spot Lines:** para DXing casual o exploración de banda, donde las líneas ayudan a identificar exactamente a qué señal corresponde cada etiqueta.
- La configuración se guarda de inmediato; no hay ningún botón Save que deba presionar.

## Relacionado

- [Activar o desactivar spots](../spot-settings/turn-spots-on-or-off.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
- [Descripción general de SpotHub](overview.md)
- [Descripción general de Spot Settings](../spot-settings/overview.md)
