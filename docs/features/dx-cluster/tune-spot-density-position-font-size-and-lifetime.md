# Referencia de la pestaña Display de SpotHub

La pestaña Display de SpotHub controla cómo aparecen las etiquetas de spots en el panadapter: cuántas se apilan verticalmente, dónde se ubican, el tamaño del texto y cuánto tiempo permanece cada spot antes de desvanecerse. También incluye controles de marcadores de Signal History y opciones de coloreado por DXCC. Ajuste estas opciones para reducir el desorden en una banda concurrida o para hacer que los spots sean más legibles en una pantalla pequeña.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión de radio para cambiar estos ajustes.
- Al menos una fuente de spots (DX cluster, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe estar activa para que pueda ver el efecto de sus cambios en tiempo real.
- La superposición principal de spots debe estar activada. En la pestaña Display, confirme que el control **Spots:** muestra Enabled.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Confirme que **Spots:** esté en Enabled. Si no lo está, haga clic en él para activar la superposición.
4. Para mostrar u ocultar las superposiciones de canales de memoria en el panadapter, haga clic en **Memories:**.
5. Para controlar cuántos spots se apilan verticalmente antes de que comiencen a superponerse, arrastre el control deslizante **Levels:**. Los valores más altos permiten más filas de etiquetas de spots.
6. Para mover las etiquetas de spots hacia arriba o hacia abajo en el panadapter, arrastre el control deslizante **Position:**.
7. Para cambiar el tamaño del texto de las etiquetas de spots, arrastre el control deslizante **Font Size:**.
8. Para establecer cuánto tiempo permanece visible un spot antes de desaparecer, arrastre el control deslizante **Spot Lifetime:**. El valor está en segundos.
9. **Auto:** está habilitado de forma predeterminada. Cuando está activado, AetherSDR cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (por ejemplo, CW, FT8, RTTY). Haga clic en **Auto:** para alternar este comportamiento.
10. Para mostrar u ocultar los marcadores de señales de voz de Signal History, haga clic en **Signals (Signal History):**.
11. Para mostrar u ocultar los marcadores de QRM, haga clic en **QRM (Signal History):**.
12. Para borrar todos los spots de DX, la alimentación de memoria, los marcadores de Signal History y los marcadores de QRM del espectro, haga clic en **Clear All**.
13. Para establecer el color de anulación para todos los spots, haga clic en **Override Colors:** para activarlo y luego haga clic en el botón selector de color junto a él para elegir un color.
14. Para habilitar colores de fondo personalizados para los spots, haga clic en **Override Background: Enabled**. Para que el color de fondo se seleccione automáticamente para obtener contraste, haga clic en **Override Background: Auto**.
15. Para establecer la opacidad del fondo, arrastre el control deslizante **Background Opacity:**.
16. Para mostrar u ocultar las líneas verticales trazadas desde el espectro hasta cada etiqueta de spot, haga clic en **Spot Lines:**. El botón muestra Enabled cuando la función está activada. Desactívelo durante concursos para reducir el desorden visual.
17. Para habilitar el coloreado por DXCC, haga clic en **DXCC Colors:** y cargue un archivo de registro ADIF usando **Log File (ADIF):**.
18. Haga clic en las muestras de color bajo la sección DXCC Coloring para elegir colores para los estados New DXCC, New Band, New Mode y Worked.
19. Ajuste el comportamiento de los marcadores de Signal History usando los controles deslizantes **Marker Lifetime:**, **QRM Gate:** y **Edge Threshold:**.
20. Haga clic en las muestras de color bajo la sección Signal History para elegir colores para los marcadores Signals y QRM.
21. Alterne **Snap to Step:** para redondear el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo.
22. Cierre el diálogo. Los cambios surten efecto de inmediato.

## Qué hace cada control

| Control | Clave de ajuste | Comportamiento |
|---------|-------------|----------|
| **Spots:** | `IsSpotsEnabled` | Interruptor principal para la superposición de spots en el panadapter. |
| **Memories:** | `IsMemorySpotsEnabled` | Alterna la superposición de canales de memoria en el panadapter. |
| **Auto:** | `SpotAutoSwitchMode` | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (por ejemplo, CW, FT8, RTTY). La clave de ajuste cambió de `SpotsAutoMode` en v26.5.1. |
| **Signals (Signal History)** | `SHistoryMarkersEnabled` | Marcadores dorados para señales detectadas con ancho de voz en el panadapter. Nuevo en v26.5.1. Mismo interruptor que View > Signal History Markers. |
| **QRM (Signal History)** | `SHistoryQrmEnabled` | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Nuevo en v26.5.1. Mismo interruptor que View > QRM History Markers. |
| **Clear All** | — | Borra todos los spots de DX, la alimentación de memoria, los marcadores de Signal History y los marcadores de QRM del espectro. |
| **Levels:** | `SpotsMaxLevel` | Número de filas de apilamiento vertical para las etiquetas de spots. |
| **Position:** | `SpotsStartingHeightPercentage` | Posición vertical de la banda de etiquetas de spots en el panadapter. |
| **Font Size:** | `SpotFontSize` | Tamaño del texto en cada etiqueta de spot. |
| **Spot Lifetime:** | `DxClusterSpotLifetimeSec` | Segundos que una etiqueta de spot permanece visible antes de desvanecerse. |
| **Spot Lines:** | `IsSpotsLinesEnabled` | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Predeterminado: Enabled. Desactívelo durante concursos para reducir el desorden visual. |
| **Override Colors:** | `IsSpotsOverrideColorsEnabled` | Fuerza un único color de texto para todos los spots. El botón siempre muestra "Enabled" independientemente del estado. Al presionarlo se activa o desactiva la función. |
| Selector de color de texto de spots | `SpotsOverrideColor` | Abre QColorDialog para elegir el color del texto de los spots. Predeterminado: `#FFFF00`. |
| **Override Background: Enabled** | `IsSpotsOverrideBackgroundColorsEnabled` | Habilita un color de fondo personalizado para los spots. |
| **Override Background: Auto** | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Selecciona automáticamente el color de fondo para obtener contraste. |
| Selector de color de fondo de spots | `SpotsOverrideBgColor` | Abre QColorDialog para el color de fondo de los spots. Predeterminado: `#000000`. |
| **Background Opacity:** | `SpotsBackgroundOpacity` | Opacidad del color de fondo de los spots. |
| **Total Spots:** | — | Conteo en vivo de los spots actualmente rastreados en todas las fuentes. |
| **DXCC Colors:** | `IsDxccColoringEnabled` | Colorea los spots según el estado de DXCC trabajado/confirmado/necesario. La clave de ajuste cambió de `DxccColoringEnabled` en v26.5.1. El botón siempre muestra "Enabled" independientemente del estado. |
| **Log File (ADIF):** | `DxccAdifFilePath` | Carga un archivo de registro ADIF para impulsar el coloreado por DXCC. Supervisa automáticamente el archivo para detectar cambios después de la selección. La clave de ajuste cambió de `DxccAdifPath` en v26.5.1. |
| **Imported: (DXCC stats)** | — | Muestra el conteo de QSO y el conteo de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`. |
| Muestras de color DXCC (New DXCC / New Band / New Mode / Worked) | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` | Abre un selector de color para cada categoría de estado DXCC. Nuevo en v26.5.1. |
| **Marker Lifetime:** | `SHistoryLifetimeS` | Cuánto tiempo persiste un marcador de Signal History inactivo antes de eliminarse. Predeterminado: 60 s. Nuevo en v26.5.1. |
| **QRM Gate:** | `SHistoryQrmGateS` | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM. Predeterminado: 6 s. Nuevo en v26.5.1. |
| **Edge Threshold:** | `SHistorySoftEdgeDb` | Umbral por encima del piso de ruido para el recorrido del borde pendiente que refina el borde lateral de la portadora de S-History. Predeterminado: 3.0 dB. Nuevo en v26.5.1. |
| Muestras de color de Signal History (Signals / QRM) | `SHistoryColorSignals`, `SHistoryColorQrm` | Abre un selector de color para los marcadores de señales de voz (dorados) y los marcadores de QRM (rojos). Nuevo en v26.5.1. |
| **Snap to Step:** | `SHistorySnapToStep` | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. Predeterminado: Disabled. Nuevo en v26.5.1. El botón siempre muestra "Enabled" independientemente del estado. |

## Doble clic en un spot para sintonizar

Al hacer doble clic en una fila de la tabla Spot List, el slice activo se sintoniza a la frecuencia del spot. AetherSDR también reenvía el modo extraído del comentario del spot (por ejemplo, CW, FT8 o SSB) para que el modo del slice cambie automáticamente para coincidir con el spot, no solo la frecuencia.

## Consejos

- Si las etiquetas de spots se superponen gravemente en una banda concurrida, aumente **Levels:** para agregar más filas de apilamiento, o reduzca **Spot Lifetime:** para que los spots antiguos se despejen antes.
- Desactive **Spot Lines:** durante concursos o en bandas muy concurridas para reducir el desorden visual sin ocultar las etiquetas de spots.
- Los spots de WSJT-X tienen su propia configuración de vida útil por fuente (**Spot Life:** en la pestaña WSJT-X, almacenada como `WsjtxSpotLife`). El control deslizante **Spot Lifetime:** de la pestaña Display se aplica a todas las demás fuentes.
- Cuando **Override Colors:** está desactivado, cada fuente de spots usa su color configurado en la pestaña de la fuente.
- Los marcadores de Signal History son independientes de los spots de DX. Use **Clear All** para eliminar ambos simultáneamente.
- El diálogo de SpotHub ahora usa colores conscientes del tema. Los indicadores de estado de conexión se diseñan con los colores de acento, etiqueta y peligro del tema actual en lugar de valores fijos. Esto garantiza una apariencia coherente con el resto de la aplicación.
- Los botones de alternancia para **Override Colors:**, **Spot Lines:**, **DXCC Colors:** y **Snap to Step:** siempre muestran "Enabled" independientemente de su estado actual. El estado presionado o no presionado del botón indica si la función está activada o desactivada.
- Las casillas de verificación de filtro de banda de la pestaña Spot List usan un diseño fluido que se ajusta a nuevas filas cuando el diálogo es estrecho, manteniendo cada casilla legible en lugar de comprimirlas horizontalmente. Esto evita el aplastamiento ilegible que podía ocurrir en versiones anteriores.

## Solución de problemas

- **Las etiquetas de spots no son visibles en absoluto** — Verifique que **Spots:** en la pestaña Display esté en Enabled (`IsSpotsEnabled`). También confirme que al menos una fuente de spots esté conectada y recibiendo spots.
- **Las líneas de spots no son visibles** — Verifique que **Spot Lines:** esté en Enabled. Si el fondo es claro, las líneas pueden ser difíciles de ver.
- **El coloreado por DXCC no funciona** — Confirme que **DXCC Colors:** esté habilitado y que haya cargado un archivo de registro ADIF usando **Log File (ADIF):**.
- **Los marcadores de Signal History no aparecen** — Verifique que **Signals (Signal History):** o **QRM (Signal History):** esté en Enabled. Estos marcadores solo aparecen cuando la radio está recibiendo señales.
- **Hacer doble clic en un spot no cambia el modo del slice** — Confirme que **Auto:** esté habilitado. También verifique que el comentario del spot contenga una cadena de modo reconocible. La extracción del modo depende del texto del comentario proporcionado por la fuente de spots; los spots sin información de modo en el comentario sintonizarán la frecuencia pero no cambiarán el modo.

## Relacionado

- [Información general de SpotHub](overview.md)
- [Elija colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
- [Iniciar el listener UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- Editar comandos de inicio para fuentes de cluster
<!-- docmesh:llm version=V26.8.4 date=2026-08-01 -->
