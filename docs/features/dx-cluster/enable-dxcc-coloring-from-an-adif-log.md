# Habilitar el coloreado de DXCC desde un archivo de registro ADIF

El coloreado de DXCC permite que AetherSDR marque los puntos en el panadapter según si la entidad DX ha sido trabajada, confirmada o aún es necesaria, basándose en los contactos de su archivo de registro ADIF. Esto le ayuda a distinguir rápidamente las nuevas entidades de aquellas que ya ha registrado.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para configurar esta función.
- Necesita un archivo de registro ADIF exportado desde su software de registro. El archivo debe usar el formato estándar `.adi` o `.adif`.
- Al menos una fuente de spots (DX cluster, RBN, WSJT-X, POTA, etc.) debe estar activa para que aparezcan spots en el panadapter.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en el botón de alternancia **DXCC Colors:** para activarlo. El botón activa el coloreado de DXCC (`IsDxccColoringEnabled`).
4. Haga clic en **Log File (ADIF):** para abrir un selector de archivos. Seleccione su archivo de registro ADIF. La ruta se almacena en `DxccAdifFilePath`.
5. Confirme que el indicador de estadísticas de DXCC se actualice para mostrar el número de QSO y entidades importados del archivo.
6. Opcionalmente, haga clic en las muestras de color para **New DXCC**, **New Band**, **New Mode** y **Worked** para personalizar el color asignado a cada categoría de estado de DXCC.

## Función de cada control

| Control                                                       | Comportamiento                                                                                                                                                                                                       | Clave de configuración                                                                      |
|---------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| **DXCC Colors:**                                              | Alternancia principal. Colorea los spots del panadapter según el estado DXCC trabajado/confirmado/necesario.                                                                                                         | `IsDxccColoringEnabled` (cambiado desde `DxccColoringEnabled` en v26.5.1)                  |
| **Log File (ADIF):**                                          | Abre un selector de archivos. El archivo ADIF elegido se lee para completar el estado DXCC. Supervisa automáticamente el archivo en busca de cambios después de la selección.                                        | `DxccAdifFilePath` (cambiado desde `DxccAdifPath` en v26.5.1)                             |
| **Imported:**                                                 | Muestra el recuento de QSO y de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`.                                                                                                           | —                                                                                          |
| Muestra de color **New DXCC**                                 | Abre un selector de color para el color asignado a entidades DXCC nunca trabajadas.                                                                                                                                  | `DxccColorNewEntity` (nuevo en v26.5.1)                                                    |
| Muestra de color **New Band**                                 | Abre un selector de color para el color asignado a entidades DXCC trabajadas en otras bandas pero necesarias en la banda actual.                                                                                     | `DxccColorNewBand` (nuevo en v26.5.1)                                                      |
| Muestra de color **New Mode**                                 | Abre un selector de color para el color asignado a entidades DXCC trabajadas en otros modos pero necesarias en el modo actual.                                                                                       | `DxccColorNewMode` (nuevo en v26.5.1)                                                      |
| Muestra de color **Worked**                                   | Abre un selector de color para el color asignado a entidades DXCC completamente trabajadas y confirmadas.                                                                                                            | `DxccColorWorked` (nuevo en v26.5.1)                                                       |
| **Spots:**                                                    | Alternancia principal para la superposición de spots DX en el panadapter.                                                                                                                                            | `IsSpotsEnabled`                                                                           |
| **Memories:**                                                 | Alterna la superposición de canales de memoria en el panadapter.                                                                                                                                                     | `IsMemorySpotsEnabled`                                                                     |
| **Auto:**                                                     | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (p. ej., CW, FT8, RTTY).                                                                                           | `SpotAutoSwitchMode` (cambiado desde `SpotsAutoMode` en v26.5.1)                           |
| **Signals (Signal History)**                                  | Marcadores dorados para señales detectadas de ancho de voz en el panadapter. Nuevo en v26.5.1 (#2426). Misma alternancia que View > Signal History Markers.                                                          | `SHistoryMarkersEnabled` (nuevo en v26.5.1)                                                |
| **QRM (Signal History)**                                      | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Nuevo en v26.5.1 (#2426). Misma alternancia que View > QRM History Markers.                                                           | `SHistoryQrmEnabled` (nuevo en v26.5.1)                                                    |
| **Clear All**                                                 | Borra todos los spots DX, la alimentación de memoria, los marcadores de Signal History y los marcadores QRM del espectro.                                                                                            | —                                                                                          |
| **Levels:**                                                   | Número de filas de apilamiento vertical para spots (1–10).                                                                                                                                                           | `SpotsMaxLevel`                                                                            |
| **Position:**                                                 | Posición vertical en el panadapter (0–100%).                                                                                                                                                                         | `SpotsStartingHeightPercentage`                                                            |
| **Font Size:**                                                | Tamaño del texto del spot (8–32).                                                                                                                                                                                    | `SpotFontSize`                                                                             |
| **Spot Lifetime:**                                            | Segundos antes de que un spot se desvanezca (10 seg – 24 horas, pasos no lineales).                                                                                                                                  | `DxClusterSpotLifetimeSec`                                                                 |
| **Override Colors:**                                          | Fuerza un solo color de texto para todos los spots.                                                                                                                                                                  | `IsSpotsOverrideColorsEnabled`                                                             |
| Selector de color de texto del spot                           | Abre QColorDialog para elegir el color del texto del spot cuando Override Colors está activado. Valor predeterminado #FFFF00.                                                                                        | `SpotsOverrideColor`                                                                       |
| **Override Background: Enabled**                              | Activa el color de fondo personalizado del spot.                                                                                                                                                                     | `IsSpotsOverrideBackgroundColorsEnabled`                                                   |
| **Override Background: Auto**                                 | Elige automáticamente el color de fondo para contraste cuando el fondo personalizado está activado.                                                                                                                  | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                              |
| Selector de color de fondo del spot                           | Abre QColorDialog para el color de fondo del spot. Valor predeterminado #000000.                                                                                                                                     | `SpotsOverrideBgColor`                                                                     |
| **Background Opacity:**                                       | Opacidad del color de fondo del spot (0–100%). Valor predeterminado 48.                                                                                                                                              | `SpotsBackgroundOpacity`                                                                   |
| **Spot Lines:**                                               | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactive durante concursos para reducir el desorden visual. Activado por defecto.                                                           | `IsSpotsLinesEnabled`                                                                      |
| **DXCC Coloring (sección)**                                   | Encabezado de sección para los controles de coloreado DXCC en la columna izquierda debajo del divisor.                                                                                                               | —                                                                                          |
| **Signal History (sección)**                                  | Encabezado de sección para los ajustes de Signal History en la columna derecha debajo del divisor. Nuevo en v26.5.1 (#2506).                                                                                         | —                                                                                          |
| **Marker Lifetime:**                                          | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado (15–300 seg). Valor predeterminado 60 s. Nuevo en v26.5.1.                                                                      | `SHistoryLifetimeS` (nuevo en v26.5.1)                                                     |
| **QRM Gate:**                                                 | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM (3–30 seg). Valor predeterminado 6 s. Nuevo en v26.5.1.                                                 | `SHistoryQrmGateS` (nuevo en v26.5.1)                                                      |
| **Edge Threshold:**                                           | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde del lado de la portadora de S-History (1.0–10.0 dB). Valor predeterminado 3.0 dB. Más bajo = más cercano a la portadora pero más sensible al ruido. Nuevo en v26.5.1. | `SHistorySoftEdgeDb` (nuevo en v26.5.1)                                                    |
| Muestra de color **Signals**                                  | Abre un selector de color para los marcadores de señal de voz (dorado). Valor predeterminado #FFC800. Nuevo en v26.5.1.                                                                                             | `SHistoryColorSignals` (nuevo en v26.5.1)                                                  |
| Muestra de color **QRM**                                      | Abre un selector de color para los marcadores QRM (rojo). Valor predeterminado #FF0000. Nuevo en v26.5.1.                                                                                                           | `SHistoryColorQrm` (nuevo en v26.5.1)                                                      |
| **Snap to Step:**                                             | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. Desactivado por defecto. Nuevo en v26.5.1.           | `SHistorySnapToStep` (nuevo en v26.5.1)                                                    |
| Total Spots:                                                  | Lectura en vivo de cuántos spots se rastrean actualmente en todas las fuentes. Se actualiza cuando se añaden o borran spots.                                                                                         | —                                                                                          |

## Sintonización desde la lista de spots

Al hacer doble clic en una fila de la pestaña **Spot List** se sintoniza el receptor activo en la frecuencia de ese spot. A partir de v0.9.7, AetherSDR también reenvía el modo derivado del comentario del spot, por lo que el receptor cambia al modo apropiado (por ejemplo, CW o SSB) para coincidir con el spot, en lugar de solo cambiar la frecuencia.

## Comandos de inicio de Cluster y RBN

Las pestañas **Cluster** y **RBN** tienen cada una un botón **Startup Commands…** que abre un editor para comandos enviados automáticamente después de cada inicio de sesión en esa fuente. Nuevo en v26.5.2.1 (#2683).

### Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Cluster** o **RBN**.
3. Haga clic en **Startup Commands…**.
4. Escriba un comando por línea (por ejemplo, `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`).
5. Haga clic en **Save**. Los comandos se almacenan por separado para cada fuente:
   - La pestaña Cluster usa la clave de configuración `DxClusterStartupCommands`.
   - La pestaña RBN usa la clave de configuración `RbnStartupCommands`.

Los comandos se reproducen después de cada conexión, incluyendo reconexiones.

## Reporte a FreeDV Reporter

El grupo **Station Reporting** en la pestaña **FreeDV** permite que AetherSDR transmita la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org siempre que el módem RADE esté activo.

### Requisitos antes de activar

- Debe estar disponible un indicativo no vacío, ya sea desde la radio (cuando **Use radio (callsign)** está marcado) o ingresado manualmente en el campo **Callsign:**.
- Debe estar disponible un cuadrado de cuadrícula Maidenhead no vacío, ya sea desde el GPS de la radio (cuando **Use GPS (grid)** está marcado, en hardware compatible) o ingresado manualmente en el campo **Grid Square:**.
- Si falta alguno de los valores al marcar **Enable FreeDV Reporter reporting when RADE is active**, aparece un diálogo de advertencia y la casilla de verificación se desmarca.

### Pasos

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme que **Use radio (callsign)** esté marcado si desea que AetherSDR obtenga el indicativo de la radio automáticamente. Desmárquelo y escriba un indicativo en **Callsign:** para ingresarlo manualmente.
3. Si su radio tiene hardware GPS, confirme que **Use GPS (grid)** esté marcado para completar **Grid Square:** automáticamente. De lo contrario, desmárquelo y escriba su cuadrado de cuadrícula Maidenhead (hasta seis caracteres) en **Grid Square:**.
4. Opcionalmente, escriba un mensaje corto en **Station Msg:** para mostrarlo junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active** (`FreeDvAutoReport`). Si faltan el indicativo o la cuadrícula, aparece una advertencia: complete el campo faltante e intente de nuevo.
6. Para que el reporte comience automáticamente cada vez que se inicie AetherSDR, active **Auto-start on startup (FreeDV)** (`FreeDvAutoStart`).

## Consejos

- El indicador de estadísticas DXCC en el diálogo muestra cuántos QSO y entidades se importaron del archivo ADIF. Si muestra cero después de cargar, verifique que el archivo sea ADIF válido.
- El botón **Log File (ADIF):** almacena la ruta de forma persistente. No necesita volver a seleccionar el archivo después de reiniciar AetherSDR.
- AetherSDR supervisa automáticamente el archivo ADIF en busca de cambios después de la selección. Cuando su registrador escribe en el archivo, los colores de los spots en el panadapter se actualizan automáticamente — no se necesita una alternancia de recarga separada.
- El coloreado DXCC es independiente de los colores de spots por fuente. Si **Override Colors:** también está activo, consulte [Pick colors for each spot source](pick-colors-for-each-spot-source.md) para saber cómo interactúan esas configuraciones.
- **Spot Lines:** (`IsSpotsLinesEnabled`) está activado por defecto. Durante concursos o cuando el panadapter se siente visualmente recargado, desactive esta alternancia en la pestaña **Display** para eliminar las líneas verticales mientras mantiene visibles las etiquetas de los spots.
- Las cuatro muestras de color DXCC (**New DXCC**, **New Band**, **New Mode**, **Worked**) reemplazan el esquema de color fijo anterior. Personalice cada una según su preferencia.
- Cuando **Use radio (callsign)** está marcado, el campo de indicativo se actualiza automáticamente si cambia el indicativo en Radio Setup sin volver a abrir SpotHub.
- La transmisión del reportero está limitada por compilación mediante `HAVE_WEBSOCKETS`. En Windows, requiere adicionalmente `HAVE_RADE`. Si el grupo **Station Reporting** o la casilla de verificación de activación están ausentes, su compilación no incluye los componentes necesarios.
- Los comandos de inicio se almacenan por separado para la pestaña **Cluster** (`DxClusterStartupCommands`) y la pestaña **RBN** (`RbnStartupCommands`). Puede configurar comandos diferentes para cada fuente.

## Solución de problemas

- **Las estadísticas DXCC muestran 0 QSO después de seleccionar un archivo** — El archivo
