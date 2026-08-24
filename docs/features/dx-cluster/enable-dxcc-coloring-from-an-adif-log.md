# Habilitar el coloreado DXCC desde un archivo de registro ADIF

El coloreado DXCC permite que AetherSDR marque los spots del panadapter según si la entidad DX ha sido trabajada, confirmada o aún es necesaria, basándose en los contactos de su archivo de registro ADIF. Esto le ayuda a distinguir rápidamente las entidades nuevas de las que ya ha registrado.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para configurar esta función.
- Necesita un archivo de registro ADIF exportado desde su software de registro. El archivo debe usar el formato estándar `.adi` o `.adif`.
- Al menos una fuente de spots (cluster DX, RBN, WSJT-X, POTA, etc.) debe estar activa para que los spots aparezcan en el panadapter.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en el botón de alternancia **DXCC Colors:** para habilitarlo. El botón activa el coloreado DXCC (`IsDxccColoringEnabled`).
4. Haga clic en **Log File (ADIF):** para abrir un selector de archivos. Seleccione su archivo de registro ADIF. La ruta se almacena en `DxccAdifFilePath`.
5. Confirme que el indicador de estadísticas DXCC se actualiza para mostrar el número de QSO y entidades importados del archivo.
6. Opcionalmente, haga clic en las muestras de color para **New DXCC**, **New Band**, **New Mode** y **Worked** para personalizar el color asignado a cada categoría de estado DXCC.

## Qué hace cada control

| Control                                                       | Comportamiento                                                                                                                                                                                                            | Clave de configuración                                                                                |
|---------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| **DXCC Colors:**                                              | Alternancia maestra. Colorea los spots del panadapter según el estado DXCC trabajado/confirmado/necesario.                                                                                                                   | `IsDxccColoringEnabled` (cambiado desde `DxccColoringEnabled` en v26.5.1)                              |
| **Log File (ADIF):**                                          | Abre un selector de archivos. El archivo ADIF elegido se lee para poblar el estado DXCC. Vigila automáticamente el archivo para detectar cambios después de la selección.                                                    | `DxccAdifFilePath` (cambiado desde `DxccAdifPath` en v26.5.1)                                           |
| **Imported:**                                                 | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`.                                                                                                      | —                                                                                                      |
| **New DXCC** muestra de color                                 | Abre un selector de color para el color asignado a entidades DXCC nunca trabajadas.                                                                                                                                           | `DxccColorNewEntity` (nuevo en v26.5.1)                                                                |
| **New Band** muestra de color                                 | Abre un selector de color para el color asignado a entidades DXCC trabajadas en otras bandas pero necesarias en la banda actual.                                                                                              | `DxccColorNewBand` (nuevo en v26.5.1)                                                                  |
| **New Mode** muestra de color                                 | Abre un selector de color para el color asignado a entidades DXCC trabajadas en otros modos pero necesarias en el modo actual.                                                                                                | `DxccColorNewMode` (nuevo en v26.5.1)                                                                  |
| **Worked** muestra de color                                   | Abre un selector de color para el color asignado a entidades DXCC totalmente trabajadas y confirmadas.                                                                                                                       | `DxccColorWorked` (nuevo en v26.5.1)                                                                   |
| **Spots:**                                                    | Alternancia maestra para la superposición de spots DX en el panadapter.                                                                                                                                                     | `IsSpotsEnabled`                                                                                       |
| **Memories:**                                                 | Alterna la superposición de canales de memoria en el panadapter.                                                                                                                                                            | `IsMemorySpotsEnabled`                                                                                 |
| **Auto:**                                                     | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (p. ej., CW, FT8, RTTY).                                                                                                    | `SpotAutoSwitchMode` (cambiado desde `SpotsAutoMode` en v26.5.1)                                       |
| **Signals (Signal History)**                                  | Marcadores dorados para señales detectadas de ancho de voz en el panadapter. Nuevo en v26.5.1 (#2426). Misma alternancia que View > Signal History Markers.                                                                  | `SHistoryMarkersEnabled` (nuevo en v26.5.1)                                                            |
| **QRM (Signal History)**                                      | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Nuevo en v26.5.1 (#2426). Misma alternancia que View > QRM History Markers.                                                                   | `SHistoryQrmEnabled` (nuevo en v26.5.1)                                                                |
| **Clear All**                                                 | Borra todos los spots DX, la alimentación de memorias, los marcadores de Signal History y los marcadores QRM del espectro.                                                                                                    | —                                                                                                      |
| **Levels:**                                                   | Número de filas de apilamiento vertical para spots (1–10).                                                                                                                                                                   | `SpotsMaxLevel`                                                                                        |
| **Position:**                                                 | Posición vertical en el panadapter (0–100%).                                                                                                                                                                                | `SpotsStartingHeightPercentage`                                                                        |
| **Font Size:**                                                | Tamaño del texto del spot (8–32).                                                                                                                                                                                           | `SpotFontSize`                                                                                         |
| **Spot Lifetime:**                                            | Segundos antes de que un spot se desvanezca (10 s – 24 h, pasos no lineales).                                                                                                                                                | `DxClusterSpotLifetimeSec`                                                                             |
| **Override Colors:**                                          | Fuerza un único color de texto para todos los spots.                                                                                                                                                                          | `IsSpotsOverrideColorsEnabled`                                                                         |
| **Selector de color de texto del spot**                       | Abre QColorDialog para elegir el color del texto del spot cuando Override Colors está habilitado. Predeterminado #FFFF00.                                                                                                     | `SpotsOverrideColor`                                                                                   |
| **Override Background: Enabled**                              | Habilita un color de fondo personalizado para los spots.                                                                                                                                                                      | `IsSpotsOverrideBackgroundColorsEnabled`                                                               |
| **Override Background: Auto**                                 | Elige automáticamente el color de fondo para contraste cuando el fondo personalizado está habilitado.                                                                                                                         | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                          |
| **Selector de color de fondo del spot**                       | Abre QColorDialog para el color de fondo del spot. Predeterminado #000000.                                                                                                                                                   | `SpotsOverrideBgColor`                                                                                 |
| **Background Opacity:**                                       | Opacidad del color de fondo del spot (0–100%). Predeterminado 48.                                                                                                                                                            | `SpotsBackgroundOpacity`                                                                               |
| **Spot Lines:**                                               | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactive durante concursos para reducir el desorden visual. Predeterminado habilitado. El botón de alternancia siempre muestra "Enabled".            | `IsSpotsLinesEnabled`                                                                                  |
| **DXCC Coloring (sección)**                                   | Encabezado de sección para los controles de coloreado DXCC en la columna izquierda debajo del divisor.                                                                                                                        | —                                                                                                      |
| **Signal History (sección)**                                  | Encabezado de sección para los ajustes de Signal History en la columna derecha debajo del divisor. Nuevo en v26.5.1 (#2506).                                                                                                  | —                                                                                                      |
| **Marker Lifetime:**                                          | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado (15–300 s). Predeterminado 60 s. Nuevo en v26.5.1.                                                                                       | `SHistoryLifetimeS` (nuevo en v26.5.1)                                                                 |
| **QRM Gate:**                                                 | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de ser clasificada como QRM (3–30 s). Predeterminado 6 s. Nuevo en v26.5.1.                                                               | `SHistoryQrmGateS` (nuevo en v26.5.1)                                                                  |
| **Edge Threshold:**                                           | Umbral por encima del piso de ruido para el recorrido de borde de pendiente que refina el borde del lado de la portadora del S-History (1,0–10,0 dB). Predeterminado 3,0 dB. Más bajo = más cerca de la portadora pero más sensible al ruido. Nuevo en v26.5.1. | `SHistorySoftEdgeDb` (nuevo en v26.5.1)                                                                |
| **Signals** muestra de color                                  | Abre un selector de color para los marcadores de señal de voz (dorado). Predeterminado #FFC800. Nuevo en v26.5.1.                                                                                                             | `SHistoryColorSignals` (nuevo en v26.5.1)                                                              |
| **QRM** muestra de color                                      | Abre un selector de color para los marcadores QRM (rojo). Predeterminado #FF0000. Nuevo en v26.5.1.                                                                                                                          | `SHistoryColorQrm` (nuevo en v26.5.1)                                                                  |
| **Snap to Step:**                                             | Redondea el clic-para-sintonizar del S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. Predeterminado deshabilitado. El botón de alternancia siempre muestra "Enabled". Nuevo en v26.5.1. | `SHistorySnapToStep` (nuevo en v26.5.1)                                                                |
| Total Spots:                                                  | Lectura en vivo de cuántos spots se rastrean actualmente en todas las fuentes. Se actualiza siempre que se agregan o borran spots.                                                                                             | —                                                                                                      |

## Casillas de verificación de banda de la pestaña Spot List

La pestaña **Spot List** contiene casillas de verificación por banda que filtran qué bandas aparecen en la tabla de spots. A partir de v26.7.4, estas casillas usan un diseño de flujo, de modo que cuando el diálogo SpotHub es estrecho, las casillas se ajustan a una nueva fila en lugar de comprimirse a un tamaño ilegible. El ancho mínimo del diálogo se ha reducido de 680 a 360 píxeles para permitir que la ventana se reduzca una vez que se ocultan las columnas de la tabla de spots.

Para usar las casillas de verificación de banda:
1. Haga clic en la pestaña **Spot List**.
2. Marque o desmarque cualquier nombre de banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.) para mostrar u ocultar los spots en esa banda en la tabla.
3. Haga clic en **Clear** para vaciar la lista de spots actual.

## Sintonización desde la lista de spots

Hacer doble clic en una fila de la pestaña **Spot List** sintoniza el receptor activo a la frecuencia de ese spot. A partir de v0.9.7, AetherSDR también reenvía el modo derivado del comentario del spot, por lo que el receptor cambia al modo apropiado (por ejemplo, CW o SSB) para coincidir con el spot en lugar de solo cambiar la frecuencia.

## Columnas de la tabla de la lista de spots

La pestaña **Spot List** muestra una tabla ordenable de todos los spots en vivo con las siguientes columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode y Source.

A partir de v26.8.4, la columna **Time** ahora es ordenable, igual que la columna **Freq**. Anteriormente, Time era la única columna siempre visible que no se podía ordenar, por lo que hacer clic en su encabezado no hacía nada y no había forma de volver al orden predeterminado de más reciente primero una vez que se había ordenado la columna **Freq**. Ahora puede hacer clic en el encabezado **Time** para restaurar o alternar el orden de más reciente primero.

Para sintonizar un spot desde la tabla:
1. Abra `Settings > SpotHub...` y haga clic en la pestaña **Spot List**.
2. Opcionalmente, haga clic en los encabezados de columna **Time** o **Freq** para ordenar la tabla.
3. Haga doble clic en cualquier fila para sintonizar el receptor activo a la frecuencia y modo de ese spot.

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

Los comandos se reproducen después de cada conexión, incluidas las reconexiones.

## Pestañas de fuentes de spots

El diálogo SpotHub contiene una pestaña para cada fuente de spots, más las pestañas unificadas **Spot List** y **Display**:

| Pestaña            | Propósito                                                                                                                                                            |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Cluster**        | Conexión telnet a cluster DX con consola, comandos de inicio y selector de color de spots.                                                                              |
| **RBN**            | Fuente telnet de Reverse Beacon Network con limitación de velocidad, consola, comandos de inicio y selector de color de spots.                                           |
| **WSJT-X**         | Listener UDP de WSJT-X con filtros CQ/POTA/Calling Me, selectores de color por categoría y consola de decodificaciones.                                                  |
| **SpotCollector**  | Listener UDP para transmisiones de Ham Radio Deluxe SpotCollector.                                                                                                    |
| **POTA**           | Consulta api.pota.app para activaciones actuales.                                                                                                                      |
| **FreeDV**         | Fuente WebSocket de spots del reporter de QSO FreeDV. Limitado por compilación con HAVE_WEBSOCKETS.                                                                     |
| **Spot List**      | Tabla unificada y buscable de todos los spots en vivo con filtros por banda.                                                                                            |
| **Display**        | Visualización de spots en el panadapter, ajustes de Signal History y coloreado DXCC. Reorganizado en v26.5.1 (#2506).                                                  |

## Informes del FreeDV Reporter

El grupo **Station Reporting** en la pestaña **FreeDV** permite que AetherSDR transmita la actividad de su estación al mapa público del FreeDV Reporter en qso.freedv.org siempre que el módem RADE esté activo.

### Requisitos antes de habilitar

- Debe estar disponible un indicativo no vacío, ya sea desde la radio (cuando **Use radio (callsign)** está marcado) o ingresado manualmente en el campo **Callsign:**.
- Debe estar disponible un cuadrado de cuadrícula Maidenhead no vacío (
