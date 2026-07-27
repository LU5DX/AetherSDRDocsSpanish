# Habilitar el coloreado por DXCC desde un archivo de log ADIF

El coloreado por DXCC permite que AetherSDR marque los spots en el panadapter según si la entidad DX ha sido trabajada, confirmada o aún es necesaria, basándose en los contactos de su archivo de log ADIF. Esto le ayuda a distinguir rápidamente las nuevas entidades de aquellas que ya ha registrado.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para configurar esta función.
- Necesita un archivo de log ADIF exportado desde su software de logging. El archivo debe usar el formato estándar `.adi` o `.adif`.
- Al menos una fuente de spots (DX cluster, RBN, WSJT-X, POTA, etc.) debe estar activa para que aparezcan spots en el panadapter.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en el botón de alternancia **DXCC Colors:** para habilitarlo. El botón activa el coloreado por DXCC (`IsDxccColoringEnabled`).
4. Haga clic en **Log File (ADIF):** para abrir un selector de archivos. Seleccione su archivo de log ADIF. La ruta se almacena en `DxccAdifFilePath`.
5. Confirme que el indicador de estadísticas DXCC se actualiza para mostrar el número de QSOs y entidades importadas del archivo.
6. Opcionalmente, haga clic en las muestras de color para **New DXCC**, **New Band**, **New Mode** y **Worked** para personalizar el color asignado a cada categoría de estado DXCC.

## Qué hace cada control

| Control                                                       | Comportamiento                                                                                                                                                                                                                     | Clave de configuración                                                                        |
|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| **DXCC Colors:**                                              | Activación general. Colorea los spots del panadapter según el estado DXCC trabajado/confirmado/necesario.                                                                                                                            | `IsDxccColoringEnabled` (cambiado desde `DxccColoringEnabled` en v26.5.1)                    |
| **Log File (ADIF):**                                          | Abre un selector de archivos. El archivo ADIF elegido se lee para poblar el estado DXCC. Vigila automáticamente el archivo en busca de cambios después de la selección.                                                             | `DxccAdifFilePath` (cambiado desde `DxccAdifPath` en v26.5.1)                               |
| **Imported:**                                                 | Muestra el recuento de QSOs y entidades cuando se carga un log. Formato: `<N> QSOs / <M> entities`.                                                                                                                                | —                                                                                             |
| **New DXCC** muestra de color                                 | Abre un selector de color para el color asignado a entidades DXCC nunca trabajadas.                                                                                                                                               | `DxccColorNewEntity` (nuevo en v26.5.1)                                                      |
| **New Band** muestra de color                                 | Abre un selector de color para el color asignado a entidades DXCC trabajadas en otras bandas pero necesarias en la banda actual.                                                                                                  | `DxccColorNewBand` (nuevo en v26.5.1)                                                        |
| **New Mode** muestra de color                                 | Abre un selector de color para el color asignado a entidades DXCC trabajadas en otros modos pero necesarias en el modo actual.                                                                                                    | `DxccColorNewMode` (nuevo en v26.5.1)                                                        |
| **Worked** muestra de color                                   | Abre un selector de color para el color asignado a entidades DXCC completamente trabajadas y confirmadas.                                                                                                                         | `DxccColorWorked` (nuevo en v26.5.1)                                                         |
| **Spots:**                                                    | Activación general de la superposición de spots DX en el panadapter.                                                                                                                                                               | `IsSpotsEnabled`                                                                              |
| **Memories:**                                                 | Activa/desactiva la superposición de canales de memoria en el panadapter.                                                                                                                                                          | `IsMemorySpotsEnabled`                                                                        |
| **Auto:**                                                     | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (p. ej., CW, FT8, RTTY).                                                                                                         | `SpotAutoSwitchMode` (cambiado desde `SpotsAutoMode` en v26.5.1)                             |
| **Signals (Signal History)**                                  | Marcadores dorados para señales de ancho de voz detectadas en el panadapter. Nuevo en v26.5.1 (#2426). Misma activación que View > Signal History Markers.                                                                        | `SHistoryMarkersEnabled` (nuevo en v26.5.1)                                                  |
| **QRM (Signal History)**                                      | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Nuevo en v26.5.1 (#2426). Misma activación que View > QRM History Markers.                                                                           | `SHistoryQrmEnabled` (nuevo en v26.5.1)                                                      |
| **Clear All**                                                 | Limpia todos los spots DX, la alimentación de memoria, los marcadores Signal History y QRM del espectro.                                                                                                                           | —                                                                                             |
| **Levels:**                                                   | Número de filas de apilamiento vertical para spots (1–10).                                                                                                                                                                         | `SpotsMaxLevel`                                                                               |
| **Position:**                                                 | Posición vertical en el panadapter (0–100%).                                                                                                                                                                                       | `SpotsStartingHeightPercentage`                                                               |
| **Font Size:**                                                | Tamaño del texto del spot (8–32).                                                                                                                                                                                                  | `SpotFontSize`                                                                                |
| **Spot Lifetime:**                                            | Segundos antes de que un spot se desvanezca (10 seg – 24 horas, pasos no lineales).                                                                                                                                               | `DxClusterSpotLifetimeSec`                                                                    |
| **Override Colors:**                                          | Fuerza un color de texto único para todos los spots.                                                                                                                                                                               | `IsSpotsOverrideColorsEnabled`                                                                |
| **Selector de color de texto del spot**                       | Abre QColorDialog para elegir el color del texto del spot cuando Override Colors está habilitado. Valor predeterminado #FFFF00.                                                                                                    | `SpotsOverrideColor`                                                                          |
| **Override Background: Enabled**                              | Habilita un color de fondo personalizado para los spots.                                                                                                                                                                           | `IsSpotsOverrideBackgroundColorsEnabled`                                                      |
| **Override Background: Auto**                                 | Elige automáticamente el color de fondo para contraste cuando el fondo personalizado está habilitado.                                                                                                                              | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                 |
| **Selector de color de fondo del spot**                       | Abre QColorDialog para el color de fondo del spot. Valor predeterminado #000000.                                                                                                                                                   | `SpotsOverrideBgColor`                                                                        |
| **Background Opacity:**                                       | Opacidad del color de fondo del spot (0–100%). Valor predeterminado 48.                                                                                                                                                           | `SpotsBackgroundOpacity`                                                                      |
| **Spot Lines:**                                               | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Deshabilitar durante concursos para reducir el desorden visual. Habilitado por defecto. El botón de alternancia siempre muestra "Enabled".                | `IsSpotsLinesEnabled`                                                                         |
| **DXCC Coloring (sección)**                                   | Encabezado de sección para los controles de coloreado DXCC en la columna izquierda debajo del divisor.                                                                                                                            | —                                                                                             |
| **Signal History (sección)**                                  | Encabezado de sección para los ajustes de Signal History en la columna derecha debajo del divisor. Nuevo en v26.5.1 (#2506).                                                                                                      | —                                                                                             |
| **Marker Lifetime:**                                          | Cuánto tiempo persiste un marcador inactivo de Signal History antes de ser eliminado (15–300 seg). Valor predeterminado 60 s. Nuevo en v26.5.1.                                                                                  | `SHistoryLifetimeS` (nuevo en v26.5.1)                                                        |
| **QRM Gate:**                                                 | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM (3–30 seg). Valor predeterminado 6 s. Nuevo en v26.5.1.                                                                | `SHistoryQrmGateS` (nuevo en v26.5.1)                                                         |
| **Edge Threshold:**                                           | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde del lado de la portadora de S-History (1.0–10.0 dB). Valor predeterminado 3.0 dB. Más bajo = más cercano a la portadora pero más sensible al ruido. Nuevo en v26.5.1. | `SHistorySoftEdgeDb` (nuevo en v26.5.1)                                                      |
| **Signals** muestra de color                                  | Abre un selector de color para los marcadores de señal de voz (dorados). Valor predeterminado #FFC800. Nuevo en v26.5.1.                                                                                                           | `SHistoryColorSignals` (nuevo en v26.5.1)                                                    |
| **QRM** muestra de color                                      | Abre un selector de color para los marcadores QRM (rojos). Valor predeterminado #FF0000. Nuevo en v26.5.1.                                                                                                                         | `SHistoryColorQrm` (nuevo en v26.5.1)                                                        |
| **Snap to Step:**                                             | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. Deshabilitado por defecto. El botón de alternancia siempre muestra "Enabled". Nuevo en v26.5.1. | `SHistorySnapToStep` (nuevo en v26.5.1)                                                      |
| Total Spots:                                                  | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se actualiza cuando se añaden o eliminan spots.                                                                                              | —                                                                                             |

## Casillas de verificación por banda en la pestaña Spot List

La pestaña **Spot List** contiene casillas de verificación por banda que filtran qué bandas aparecen en la tabla de spots. A partir de v26.7.4, estas casillas usan un diseño de flujo para que, cuando el diálogo SpotHub sea estrecho, las casillas pasen a una nueva fila en lugar de comprimirse a un tamaño ilegible. El ancho mínimo del diálogo se ha reducido de 680 a 360 píxeles para permitir que la ventana se reduzca una vez que se oculten las columnas de la tabla de spots.

Para usar las casillas de verificación por banda:
1. Haga clic en la pestaña **Spot List**.
2. Marque o desmarque cualquier nombre de banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.) para mostrar u ocultar los spots de esa banda en la tabla.
3. Haga clic en **Clear** para vaciar la lista actual de spots.

## Sintonización desde la lista de spots

Al hacer doble clic en una fila de la pestaña **Spot List** se sintoniza el receptor activo a la frecuencia de ese spot. A partir de v0.9.7, AetherSDR también reenvía el modo derivado del comentario del spot, por lo que el receptor cambia al modo apropiado (por ejemplo, CW o SSB) para coincidir con el spot, en lugar de solo cambiar la frecuencia.

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

### Requisitos antes de habilitar

- Debe estar disponible un indicativo no vacío, ya sea desde la radio (cuando **Use radio (callsign)** está marcado) o ingresado manualmente en el campo **Callsign:**.
- Debe estar disponible un cuadrado de cuadrícula Maidenhead no vacío, ya sea desde el GPS de la radio (cuando **Use GPS (grid)** está marcado, en hardware compatible) o ingresado manualmente en el campo **Grid Square:**.
- Si falta alguno de los valores cuando marca **Enable FreeDV Reporter reporting when RADE is active**, aparece un diálogo de advertencia y la casilla de verificación vuelve a un estado desmarcado.

### Pasos

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme que **Use radio (callsign)** esté marcado si desea que AetherSDR obtenga el indicativo automáticamente desde la radio. Desmárquelo y escriba un indicativo en **Callsign:** para ingresarlo manualmente.
3. Si su radio tiene hardware GPS, confirme que **Use GPS (grid)** esté marcado para completar **Grid Square:** automáticamente. De lo contrario, desmárquelo y escriba su cuadrado de cuadrícula Maidenhead (hasta seis caracteres) en **Grid Square:**.
4. Opcionalmente, escriba un mensaje corto en **Station Msg:** para mostrarlo junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active** (`FreeDvAutoReport`). Si falta el indicativo o la cuadrícula, aparece una advertencia — complete el campo faltante e intente nuevamente.
6. Para que el reporte se inicie automáticamente cada vez que se lance AetherSDR, habilite **Auto-start on startup (FreeDV)** (`FreeDvAutoStart`).

## Soporte de temas

A partir de v26.6.1, el diálogo SpotHub y todas sus etiquetas de estado usan colores conscientes del tema en lugar de valores codificados. El contenedor del diálogo aplica el estilo de tema `dialog/dxCluster`, y los widgets de pestañas, las etiquetas de estado y los estados de conexión resuelven los colores del tema activo. Esto significa que el diálogo se adapta automáticamente a temas claros, oscuros o personalizados sin necesidad de ajustes manuales de color.

## Consejos

- El indicador de estadísticas DXCC en el diálogo muestra cuántos QSOs y entidades se importaron del archivo ADIF. Si muestra cero después de cargar, verifique que el archivo sea un ADIF válido.
- El botón **Log File (ADIF):** almacena la ruta de forma persistente. No necesita volver a seleccionar el archivo después de reiniciar AetherSDR.
- AetherSDR vigila automáticamente el archivo ADIF en busca de cambios después de la selección. Cuando su logger escribe en el archivo
