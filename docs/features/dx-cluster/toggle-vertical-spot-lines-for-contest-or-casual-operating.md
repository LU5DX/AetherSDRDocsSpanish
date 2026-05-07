# Alternar líneas verticales de spots para operación en concurso o casual

Por defecto, AetherSDR dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot en el panadapter. Esta página explica cómo desactivar esas líneas — útil durante concursos cuando la pantalla se vuelve desordenada — y cómo reactivarlas para operación casual.

## Antes de comenzar

- Debe tener al menos una fuente de spots configurada y activa (DX cluster, RBN, WSJT-X, POTA, SpotCollector o FreeDV), de lo contrario el efecto del cambio no será visible.
- La superposición maestra de spots debe estar activada (`IsSpotsEnabled` establecido en Enabled). Si los spots están desactivados, las líneas de spots no tienen efecto visible.

## Pasos

Hay dos formas de acceder al conmutador "Spot Lines:". Use la que le resulte más conveniente.

**Mediante SpotHub:**

1. Haga clic en `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en **Spot Lines:** para conmutarlo. El botón muestra **Enabled** (líneas dibujadas) o **Disabled** (líneas ocultas). El cambio surte efecto de inmediato.

**Mediante Spot Settings:**

1. Haga clic derecho sobre la superposición de spots del panadapter para abrir el menú contextual y seleccione la opción de configuración de spots, lo que abre la ventana **Spot Settings**.
2. Haga clic en **Spot Lines:** para conmutarlo. El botón muestra **Enabled** o **Disabled**. El cambio surte efecto de inmediato.

## Función de cada control

| Control         | Valor predeterminado | Clave de configuración |
|-----------------|---------------------|------------------------|
| **Spot Lines:** | Enabled             | `IsSpotsLinesEnabled`  |

## Consejos

- Desactive **Spot Lines:** antes de una sesión de concurso. Con docenas o cientos de spots en pantalla, eliminar las líneas reduce significativamente el ruido visual.
- Re-active **Spot Lines:** para DX casual o exploración de bandas, donde las líneas ayudan a identificar exactamente a qué señal corresponde cada etiqueta.
- La configuración se guarda de inmediato; no hay ningún botón Save que presionar.

## Relacionado

- [Turn spots on or off](../spot-settings/turn-spots-on-or-off.md)
- [Tune spot density, position, font size and lifetime](tune-spot-density-position-font-size-and-lifetime.md)
- [Clear all spots from the panadapter](clear-all-spots-from-the-panadapter.md)
- [SpotHub overview](overview.md)
- [Spot Settings overview](../spot-settings/overview.md)
