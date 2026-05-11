# Alternar líneas verticales de spots para operación en concurso o casual

Por defecto, AetherSDR dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot en el panadapter. Esta página explica cómo desactivar esas líneas — útil durante concursos cuando la pantalla se vuelve desordenada — y cómo volver a activarlas para operación casual.

## Antes de comenzar

- Al menos una fuente de spots (DX cluster, RBN, WSJT-X, POTA, SpotCollector o FreeDV) debe estar configurada y entregando spots, o el efecto del cambio no será visible.
- La superposición maestra de spots debe estar activada (`IsSpotsEnabled` configurado en Enabled). Si los spots están desactivados, las líneas de spots no tienen efecto visible.

## Pasos

Hay dos formas de acceder al conmutador "Spot Lines:". Use la que le resulte más conveniente.

**A través de SpotHub:**

1. Haga clic en `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en **Spot Lines:** para conmutarlo. El botón muestra **Enabled** (líneas dibujadas) o **Disabled** (líneas ocultas). El cambio tiene efecto inmediato.

**A través de Spot Settings:**

1. Haga clic derecho en la superposición de spots del panadapter para abrir el menú contextual y seleccione la opción de configuración de spots, que abre la ventana **Spot Settings**.
2. Haga clic en **Spot Lines:** para conmutarlo. El botón muestra **Enabled** o **Disabled**. El cambio tiene efecto inmediato.

## Qué hace cada control

| Control                                                       | Valor predeterminado                                                                                                     | Clave de configuración                                                                                               |
|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| **Spot Lines:**                                               | Enabled                                                                                                                  | `IsSpotsLinesEnabled`                                                                                                |
| Auto:                                                         | Cambia automáticamente el modo de slice al hacer clic en un spot que incluye información de modo (p. ej., CW, FT8, RTTY). | La clave de configuración cambió de SpotsAutoMode a SpotAutoSwitchMode en v26.5.1.                                   |
| Signals (Signal History)                                      | Marcadores dorados para señales de ancho de voz detectadas en el panadapter.                                             | Nuevo en v26.5.1 (#2426). Mismo conmutador que View > Signal History Markers.                                        |
| QRM (Signal History)                                          | Marcadores rojos para portadoras persistentes e interferencia de banda ancha.                                            | Nuevo en v26.5.1 (#2426). Mismo conmutador que View > QRM History Markers.                                           |
| Clear All                                                     | Limpia todos los spots DX, la fuente de memoria, los marcadores de Signal History y los marcadores QRM del espectro.     |                                                                                                                      |
| Selector de color de texto de spot                            | Abre QColorDialog para elegir el color del texto del spot.                                                               |                                                                                                                      |
| Override Background: Enabled                                  | Habilita un color de fondo personalizado para los spots.                                                                 |                                                                                                                      |
| Override Background: Auto                                     | Selecciona automáticamente el color de fondo para obtener contraste.                                                     |                                                                                                                      |
| Selector de color de fondo de spot                            | Abre QColorDialog para el color de fondo del spot.                                                                       |                                                                                                                      |
| Total Spots:                                                  | Conteo en vivo de spots actualmente rastreados en todas las fuentes.                                                     |                                                                                                                      |
| DXCC Coloring (sección)                                       | Encabezado de sección para controles de coloración DXCC en la columna izquierda debajo del divisor.                      |                                                                                                                      |
| DXCC Colors:                                                  | Colorea los spots según el estado de DXCC trabajado/confirmado/necesario.                                                | La clave de configuración cambió de DxccColoringEnabled a IsDxccColoringEnabled en v26.5.1.                          |
| Imported: (estadísticas DXCC)                                  | Muestra el conteo de QSO y el conteo de entidades cuando se carga un registro.                                           | Formato: '<N> QSOs / <M> entities'.                                                                                  |
| Muestras de color DXCC (New DXCC / New Band / New Mode / Worked) | Abre un selector de color para cada categoría de estado DXCC.                                                          | Nuevo en v26.5.1 — reemplaza el esquema de color DXCC fijo anterior.                                                 |
| Signal History (sección)                                      | Encabezado de sección para parámetros ajustables de Signal History en la columna derecha debajo del divisor.             | Nuevo en v26.5.1 (#2506). Consolida la vida útil del marcador S-History, la puerta QRM, el umbral de borde, los colores y snap-to-step. |
| Marker Lifetime:                                              | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado.                                    | Nuevo en v26.5.1. Valor predeterminado 60 s.                                                                         |
| QRM Gate:                                                     | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM.               | Nuevo en v26.5.1. Valor predeterminado 6 s.                                                                          |
| Edge Threshold:                                               | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde del lado de la portadora de S-History. | Nuevo en v26.5.1. Más bajo = más cercano a la portadora pero más sensible al ruido. Valor predeterminado 3.0 dB.     |
| Muestras de color de Signal History (Signals / QRM)           | Abre un selector de color para los marcadores de señal de voz (dorados) y los marcadores QRM (rojos).                    | Nuevo en v26.5.1.                                                                                                    |
| Snap to Step:                                                 | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. | Nuevo en v26.5.1. Valor predeterminado Disabled.                                                                     |

## Consejos

- Desactive **Spot Lines:** antes de una sesión de concurso. Con docenas o cientos de spots en pantalla, eliminar las líneas reduce significativamente el ruido visual.
- Vuelva a activar **Spot Lines:** para DXing casual o exploración de bandas, donde las líneas ayudan a identificar exactamente a qué señal corresponde cada etiqueta.
- La configuración se guarda inmediatamente; no hay ningún botón Save que presionar.

## Relacionado

- [Activar o desactivar spots](../spot-settings/turn-spots-on-or-off.md)
- [Ajustar densidad, posición, tamaño de fuente y vida útil de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Limpiar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
- [Descripción general de SpotHub](overview.md)
- [Descripción general de Spot Settings](../spot-settings/overview.md)
