# Habilitar el coloreado por DXCC desde un archivo ADIF

El coloreado por DXCC permite que AetherSDR marque los puntos en el panadapter según si la entidad DX ha sido trabajada, confirmada o aún es necesaria, basándose en los contactos de su archivo de registro ADIF. Esto le ayuda a distinguir rápidamente las nuevas entidades de aquellas que ya ha registrado.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para configurar esta función.
- Necesita un archivo de registro ADIF exportado desde su programa de registro. El archivo debe usar el formato estándar `.adi` o `.adif`.
- Al menos una fuente de spots (DX cluster, RBN, WSJT-X, POTA, etc.) debe estar activa para que aparezcan spots en el panadapter.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en el botón de alternancia **DXCC Colors:** para habilitarlo. El botón activa el coloreado por DXCC (`IsDxccColoringEnabled`).
4. Haga clic en **Log File (ADIF):** para abrir un selector de archivos. Seleccione su archivo de registro ADIF. La ruta se almacena en `DxccAdifFilePath`.
5. Confirme que el indicador de estadísticas DXCC se actualice para mostrar la cantidad de QSOs y entidades importadas del archivo.
6. Opcionalmente, haga clic en las muestras de color para **New DXCC**, **New Band**, **New Mode** y **Worked** para personalizar el color asignado a cada categoría de estado DXCC.

## Qué hace cada control

| Control                                                      | Comportamiento                                                                                                                                                                                                                     | Clave de configuración                                                                            |
|--------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| **DXCC Colors:**                                             | Activación general. Colorea los spots del panadapter según el estado DXCC trabajado/confirmado/necesario.                                                                                                                          | `IsDxccColoringEnabled` (cambiado desde `DxccColoringEnabled` en v26.5.1)                        |
| **Log File (ADIF):**                                         | Abre un selector de archivos. El archivo ADIF elegido se lee para completar el estado DXCC. Vigila automáticamente el archivo en busca de cambios después de la selección.                                                         | `DxccAdifFilePath` (cambiado desde `DxccAdifPath` en v26.5.1)                                   |
| **Imported:**                                                | Muestra el recuento de QSOs y entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`.                                                                                                                           | —                                                                                                |
| Muestra de color **New DXCC**                                | Abre un selector de color para el color asignado a entidades DXCC nunca trabajadas.                                                                                                                                                | `DxccColorNewEntity` (nuevo en v26.5.1)                                                          |
| Muestra de color **New Band**                                | Abre un selector de color para el color asignado a entidades DXCC trabajadas en otras bandas pero necesarias en la banda actual.                                                                                                   | `DxccColorNewBand` (nuevo en v26.5.1)                                                            |
| Muestra de color **New Mode**                                | Abre un selector de color para el color asignado a entidades DXCC trabajadas en otros modos pero necesarias en el modo actual.                                                                                                     | `DxccColorNewMode` (nuevo en v26.5.1)                                                            |
| Muestra de color **Worked**                                  | Abre un selector de color para el color asignado a entidades DXCC completamente trabajadas y confirmadas.                                                                                                                          | `DxccColorWorked` (nuevo en v26.5.1)                                                             |
| **Spots:**                                                   | Activación general para la superposición de spots DX en el panadapter.                                                                                                                                                             | `IsSpotsEnabled`                                                                                  |
| **Memories:**                                                | Activa/desactiva la superposición de canales de memoria en el panadapter.                                                                                                                                                          | `IsMemorySpotsEnabled`                                                                           |
| **Auto:**                                                    | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (p. ej., CW, FT8, RTTY).                                                                                                          | `SpotAutoSwitchMode` (cambiado desde `SpotsAutoMode` en v26.5.1)                                 |
| **Signals (Signal History)**                                 | Marcadores dorados para señales detectadas de ancho de voz en el panadapter. Nuevo en v26.5.1 (#2426). Misma activación que View > Signal History Markers.                                                                         | `SHistoryMarkersEnabled` (nuevo en v26.5.1)                                                      |
| **QRM (Signal History)**                                     | Marcadores rojos para portadoras persistentes e interferencias de banda ancha. Nuevo en v26.5.1 (#2426). Misma activación que View > QRM History Markers.                                                                          | `SHistoryQrmEnabled` (nuevo en v26.5.1)                                                          |
| **Clear All**                                                | Borra todos los spots DX, la fuente de memorias, los marcadores de Signal History y los marcadores QRM del espectro.                                                                                                                | —                                                                                                |
| **Levels:**                                                  | Número de filas de apilamiento vertical para spots (1–10).                                                                                                                                                                         | `SpotsMaxLevel`                                                                                  |
| **Position:**                                                | Posición vertical en el panadapter (0–100%).                                                                                                                                                                                       | `SpotsStartingHeightPercentage`                                                                  |
| **Font Size:**                                               | Tamaño del texto del spot (8–32).                                                                                                                                                                                                 | `SpotFontSize`                                                                                   |
| **Spot Lifetime:**                                           | Segundos antes de que un spot se desvanezca (10 seg – 24 horas, pasos no lineales).                                                                                                                                               | `DxClusterSpotLifetimeSec`                                                                       |
| **Override Colors:**                                         | Fuerza un solo color de texto para todos los spots.                                                                                                                                                                                | `IsSpotsOverrideColorsEnabled`                                                                   |
| Selector de color de texto del spot                          | Abre QColorDialog para elegir el color del texto del spot cuando Override Colors está habilitado. Por defecto #FFFF00.                                                                                                             | `SpotsOverrideColor`                                                                             |
| **Override Background: Enabled**                             | Habilita un color de fondo personalizado para los spots.                                                                                                                                                                           | `IsSpotsOverrideBackgroundColorsEnabled`                                                         |
| **Override Background: Auto**                                | Selecciona automáticamente el color de fondo para contraste cuando el fondo personalizado está habilitado.                                                                                                                         | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                    |
| Selector de color de fondo del spot                          | Abre QColorDialog para el color de fondo del spot. Por defecto #000000.                                                                                                                                                           | `SpotsOverrideBgColor`                                                                           |
| **Background Opacity:**                                      | Opacidad del color de fondo del spot (0–100%). Por defecto 48.                                                                                                                                                                    | `SpotsBackgroundOpacity`                                                                         |
| **Spot Lines:**                                              | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactive durante concursos para reducir el desorden visual. Habilitado por defecto. El botón de alternancia siempre muestra "Enabled".                    | `IsSpotsLinesEnabled`                                                                            |
| **DXCC Coloring (sección)**                                  | Encabezado de sección para los controles de coloreado por DXCC en la columna izquierda debajo del divisor.                                                                                                                         | —                                                                                                |
| **Signal History (sección)**                                 | Encabezado de sección para los ajustes de Signal History en la columna derecha debajo del divisor. Nuevo en v26.5.1 (#2506).                                                                                                       | —                                                                                                |
| **Marker Lifetime:**                                         | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado (15–300 seg). Por defecto 60 s. Nuevo en v26.5.1.                                                                                             | `SHistoryLifetimeS` (nuevo en v26.5.1)                                                           |
| **QRM Gate:**                                                | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM (3–30 seg). Por defecto 6 s. Nuevo en v26.5.1.                                                                      | `SHistoryQrmGateS` (nuevo en v26.5.1)                                                            |
| **Edge Threshold:**                                          | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde del lado de la portadora de S-History (1.0–10.0 dB). Por defecto 3.0 dB. Valores más bajos = más cerca de la portadora pero más sensible al ruido. Nuevo en v26.5.1. | `SHistorySoftEdgeDb` (nuevo en v26.5.1)                                                          |
| Muestra de color **Signals**                                 | Abre un selector de color para los marcadores de señal de voz (dorado). Por defecto #FFC800. Nuevo en v26.5.1.                                                                                                                     | `SHistoryColorSignals` (nuevo en v26.5.1)                                                        |
| Muestra de color **QRM**                                     | Abre un selector de color para los marcadores QRM (rojo). Por defecto #FF0000. Nuevo en v26.5.1.                                                                                                                                 | `SHistoryColorQrm` (nuevo en v26.5.1)                                                            |
| **Snap to Step:**                                            | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. Deshabilitado por defecto. El botón de alternancia siempre muestra "Enabled". Nuevo en v26.5.1. | `SHistorySnapToStep` (nuevo en v26.5.1)                                                          |
| Total Spots:                                                 | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se actualiza cuando se añaden o borran spots.                                                                                               | —                                                                                                |

## Sintonización desde la lista de spots

Hacer doble clic en una fila de la pestaña **Spot List** sintoniza el receptor activo a la frecuencia de ese spot. A partir de v0.9.7, AetherSDR también reenvía el modo derivado del comentario del spot, por lo que el receptor cambia al modo apropiado (por ejemplo, CW o SSB) para coincidir con el spot, en lugar de solo cambiar la frecuencia.

## Comandos de inicio del cluster y RBN

Las pestañas **Cluster** y **RBN** tienen cada una un botón **Startup Commands…** que abre un editor para comandos enviados automáticamente después de cada inicio de sesión en esa fuente. Nuevo en v26.5.2.1 (#2683).

### Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Cluster** o **RBN**.
3. Haga clic en **Startup Commands…**.
4. Escriba un comando por línea (por ejemplo, `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`).
5. Haga clic en **Save**. Los comandos se almacenan por separado para cada fuente:
   - La pestaña Cluster usa la clave de configuración `DxClusterStartupCommands`.
   - La pestaña RBN usa la clave de configuración `RbnStartupCommands`.

Los comandos se reejecutan después de cada conexión, incluyendo reconexiones.

## Reporte a FreeDV Reporter

El grupo **Station Reporting** en la pestaña **FreeDV** permite que AetherSDR transmita la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org siempre que el módem RADE esté activo.

### Requisitos antes de habilitar

- Debe estar disponible un indicativo no vacío, ya sea desde la radio (cuando **Use radio (callsign)** está marcado) o ingresado manualmente en el campo **Callsign:**.
- Debe estar disponible un cuadrado Maidenhead no vacío, ya sea desde el GPS de la radio (cuando **Use GPS (grid)** está marcado, en hardware compatible) o ingresado manualmente en el campo **Grid Square:**.
- Si falta alguno de los valores al marcar **Enable FreeDV Reporter reporting when RADE is active**, aparece un cuadro de diálogo de advertencia y la casilla de verificación vuelve a su estado desmarcado.

### Pasos

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme que **Use radio (callsign)** esté marcado si desea que AetherSDR obtenga el indicativo de la radio automáticamente. Desmárquelo y escriba un indicativo en **Callsign:** para ingresarlo manualmente.
3. Si su radio tiene hardware GPS, confirme que **Use GPS (grid)** esté marcado para completar **Grid Square:** automáticamente. De lo contrario, desmárquelo y escriba su cuadrado Maidenhead (hasta seis caracteres) en **Grid Square:**.
4. Opcionalmente, escriba un mensaje corto en **Station Msg:** para mostrarlo junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active** (`FreeDvAutoReport`). Si falta el indicativo o el cuadrado, aparece una advertencia: complete el campo faltante e intente nuevamente.
6. Para que el reporte comience automáticamente cada vez que se inicie AetherSDR, active **Auto-start on startup (FreeDV)** (`FreeDvAutoStart`).

## Soporte de temas

A partir de v26.6.1, el diálogo SpotHub y todas sus etiquetas de estado utilizan colores conscientes del tema en lugar de valores codificados. El contenedor del diálogo aplica el estilo de tema `dialog/dxCluster`, y los widgets de pestaña, las etiquetas de estado y los estados de conexión resuelven todos los colores del tema activo. Esto significa que el diálogo se adapta automáticamente a temas claros, oscuros o personalizados sin necesidad de ajustes manuales de color.

## Consejos

- El indicador de estadísticas DXCC en el diálogo muestra cuántos QSOs y entidades se importaron del archivo ADIF. Si muestra cero después de cargar, verifique que el archivo sea ADIF válido.
- El botón **Log File (ADIF):** almacena la ruta de forma persistente. No necesita volver a seleccionar el archivo después de reiniciar AetherSDR.
- AetherSDR vigila automáticamente el archivo ADIF en busca de cambios después de la selección. Cuando su programa de registro escribe en el archivo, los colores de los spots en el panadapter se actualizan automáticamente; no se necesita un botón de recarga independiente.
- El coloreado por DXCC es independiente de los colores de spots por fuente. Si **Override Colors:** también está activo, consulte [Pick colors for each spot source](pick-colors-for-each-spot-source.md) para saber cómo interactúan esas configuraciones.
- **Spot Lines:** (`IsSpotsLinesEnabled`) a partir de v26.6.3, el botón de alternancia siempre muestra el texto "Enabled" independientemente de su estado real. Haga clic en el botón para activar o desactivar las líneas; la apariencia del botón (marcado/desmarcado) muestra el estado actual.
- Las cuatro muestras de color DXCC (**New DXCC**, **New Band**, **New Mode**, **Worked**) reemplazan el esquema de color fijo anterior. Personalice cada una según su preferencia.
- Cuando **Use radio (callsign)** está marcado, el campo de indicativo se actualiza automáticamente si cambia el indicativo en Radio Setup sin necesidad de reabrir SpotHub.
- La transmisión al reportero depende de la compilación.
