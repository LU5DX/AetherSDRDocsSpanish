# Alternar líneas verticales de puntos para operación en concurso o informal

Por defecto, AetherSDR dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de punto en el panadapter. Esta página explica cómo desactivar esas líneas — útil durante concursos cuando la pantalla se vuelve desordenada — y cómo reactivarlas para operación informal.

## Antes de comenzar

- Al menos una fuente de puntos (DX cluster, RBN, WSJT-X, POTA, SpotCollector o FreeDV) debe estar configurada y enviando puntos, o de lo contrario el efecto del cambio no será visible.
- La superposición maestra de puntos debe estar activada (`IsSpotsEnabled` configurado como Enabled). Si los puntos están desactivados, las líneas de puntos no tienen efecto visible.

## Pasos

Existen dos formas de llegar al conmutador "Spot Lines:". Use la que le resulte más conveniente.

**A través de SpotHub:**

1. Haga clic en `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en **Spot Lines:** para alternarlo. El botón muestra **Enabled** (líneas dibujadas) o **Disabled** (líneas ocultas). El cambio surte efecto de inmediato.

**A través de Spot Settings:**

1. Haga clic derecho en la superposición de puntos del panadapter para abrir el menú contextual y seleccione la opción de configuración de puntos, que abre la ventana **Spot Settings**.
2. Haga clic en **Spot Lines:** para alternarlo. El botón muestra **Enabled** o **Disabled**. El cambio surte efecto de inmediato.

## Función de cada control

| Control | Valor predeterminado | Clave de configuración |
|---------|----------------------|------------------------|
| **Spots:** | Enabled | `IsSpotsEnabled` |
| **Memories:** | Disabled | `IsMemorySpotsEnabled` |
| **Levels:** | 3 | `SpotsMaxLevel` |
| **Position:** | 50 | `SpotsStartingHeightPercentage` |
| **Font Size:** | 16 | `SpotFontSize` |
| **Spot Lifetime:** | Varía | `DxClusterSpotLifetimeSec` |
| **Override Colors:** | Disabled | `IsSpotsOverrideColorsEnabled` |
| **Selector de color de texto de puntos** | #FFFF00 | `SpotsOverrideColor` |
| **Override Background: Enabled** | Enabled | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Enabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| **Selector de color de fondo de puntos** | #000000 | `SpotsOverrideBgColor` |
| **Background Opacity:** | 48 | `SpotsBackgroundOpacity` |
| **Spot Lines:** | Enabled | `IsSpotsLinesEnabled` |
| **Clear All Spots** | — | (sin clave) |
| **Total Spots:** | — | (indicador) |
| Auto: | Cambia automáticamente el modo de slice al hacer clic en un punto que incluye información de modo (p. ej., CW, FT8, RTTY). | La clave de configuración cambió de SpotsAutoMode a SpotAutoSwitchMode en v26.5.1. |
| Signals (Signal History) | Marcadores dorados para señales de ancho de voz detectadas en el panadapter. | Nuevo en v26.5.1 (#2426). Mismo conmutador que View > Signal History Markers. |
| QRM (Signal History) | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. | Nuevo en v26.5.1 (#2426). Mismo conmutador que View > QRM History Markers. |
| Clear All | Borra todos los puntos DX, el feed de memoria, los marcadores de Signal History y los marcadores de QRM del espectro. | |
| Selector de color de texto de puntos | Abre QColorDialog para elegir el color del texto de los puntos. | |
| Override Background: Enabled | Habilita un color de fondo personalizado para los puntos. | |
| Override Background: Auto | Selecciona automáticamente el color de fondo para contraste. | |
| Selector de color de fondo de puntos | Abre QColorDialog para el color de fondo de los puntos. | |
| Total Spots: | Conteo en vivo de los puntos actualmente rastreados en todas las fuentes. | |
| DXCC Coloring (sección) | Encabezado de sección para los controles de coloración DXCC en la columna izquierda debajo del divisor. | |
| DXCC Colors: | Colorea los puntos según el estado DXCC trabajado/confirmado/necesario. | La clave de configuración cambió de DxccColoringEnabled a IsDxccColoringEnabled en v26.5.1. |
| Imported: (estadísticas DXCC) | Muestra el conteo de QSO y el conteo de entidades cuando se carga un registro. | Formato: '<N> QSOs / <M> entities'. |
| Muestras de color DXCC (New DXCC / New Band / New Mode / Worked) | Abre un selector de color para cada categoría de estado DXCC. | Nuevo en v26.5.1 – reemplaza el esquema de color DXCC fijo anterior. |
| Signal History (sección) | Encabezado de sección para los parámetros ajustables de Signal History en la columna derecha debajo del divisor. | Nuevo en v26.5.1 (#2506). Consolida la vida útil de los marcadores de S-History, la puerta QRM, el umbral de borde, los colores y el ajuste a paso. |
| Marker Lifetime: | Cuánto tiempo persiste un marcador inactivo de Signal History antes de ser eliminado. | Nuevo en v26.5.1. Valor predeterminado 60 s. |
| QRM Gate: | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM. | Nuevo en v26.5.1. Valor predeterminado 6 s. |
| Edge Threshold: | Umbral por encima del piso de ruido para el recorrido de borde de pendiente que refina el borde lateral de la portadora de S-History. | Nuevo en v26.5.1. Más bajo = más cercano a la portadora pero más sensible al ruido. Valor predeterminado 3.0 dB. |
| Muestras de color de Signal History (Signals / QRM) | Abre un selector de color para los marcadores de señal de voz (dorados) y los marcadores de QRM (rojos). | Nuevo en v26.5.1. |
| Snap to Step: | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. | Nuevo en v26.5.1. Valor predeterminado Disabled. |

## Consejos

- Desactive **Spot Lines:** antes de una sesión de concurso. Con decenas o cientos de puntos en pantalla, eliminar las líneas reduce significativamente el ruido visual.
- Vuelva a activar **Spot Lines:** para DX informal o exploración de bandas, donde las líneas ayudan a identificar exactamente a qué señal corresponde cada etiqueta.
- La configuración se guarda de inmediato; no hay ningún botón Guardar para hacer clic.

## Relacionado

- [Turn spots on or off](../spot-settings/turn-spots-on-or-off.md)
- [Tune spot density, position, font size and lifetime](tune-spot-density-position-font-size-and-lifetime.md)
- [Clear all spots from the panadapter](clear-all-spots-from-the-panadapter.md)
- [SpotHub overview](overview.md)
- [Spot Settings overview](../spot-settings/overview.md)
