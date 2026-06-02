# Sintonizar un Spot Haciendo Doble Clic en la Lista de Spots

La pestaña Lista de Spots en SpotHub muestra todos los spots en vivo de todas las fuentes activas en una única tabla ordenable. Al hacer doble clic en una fila, se sintoniza el VFO activo en la frecuencia de ese spot. A partir de la versión v0.9.7, al hacer doble clic también se reenvía la sugerencia de modo extraída del comentario del spot, de modo que el receptor cambie al modo correcto (por ejemplo, CW o FT8) y no solo cambie la frecuencia.

## Antes de comenzar

- Al menos una fuente de spots (DX Cluster, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe estar conectada y recibiendo spots.
- La radio debe estar conectada a AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña "Spot List".
3. Opcionalmente, use las casillas de verificación "Bands:" para filtrar la tabla por banda. Desmarque cualquier banda que no desee ver.
4. Haga clic en un encabezado de columna para ordenar la tabla por esa columna. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source.
5. Haga doble clic en cualquier fila de la tabla de spots. AetherSDR sintoniza el VFO activo en la frecuencia mostrada en esa fila. Si el spot contiene un modo reconocible en su campo de comentario, AetherSDR también cambia el slice a ese modo.

## Qué hace cada control

### Pestaña Cluster

| Control                    | Comportamiento                                                                                                                                               | Clave de configuración |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| Server:                    | Nombre de host del cluster DX al que conectarse.                                                                                                                 | `ClusterHost`           |
| Port:                      | Puerto Telnet del cluster DX. Rango: 1–65535.                                                                                                                 | `ClusterPort`           |
| Callsign:                  | Indicativo de inicio de sesión enviado al cluster.                                                                                                                           | `ClusterCallsign`       |
| Connect / Disconnect       | Activa o desactiva la conexión Telnet al cluster.                                                                                                                  | —                       |
| Auto-connect on startup    | Conecta automáticamente el cluster al iniciar.                                                                                                                          | `ClusterAutoConnect`    |
| Cluster Console            | Consola Telnet de solo lectura del tráfico bruto del cluster.                                                                                                           | —                       |
| Send                       | Envía un comando escrito al cluster.                                                                                                                     | —                       |
| Spot Color:                | Abre un selector de color para los spots del cluster.                                                                                                                   | `ClusterSpotColor`      |
| Startup Commands…          | Abre el editor de comandos de inicio. Los comandos se envían automáticamente después de cada inicio de sesión. Un comando por línea (p. ej. SET/NAME, SET/QTH, ACCEPT/SPOT).          | `DxClusterStartupCommands` |

### Pestaña RBN

| Control                       | Comportamiento                                                                                                       | Clave de configuración |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------|-----------------------|
| Server:                       | Nombre de host Telnet de RBN.                                                                                              | `RbnHost`             |
| Port:                         | Puerto Telnet de RBN. Rango: 1–65535.                                                                                  | `RbnPort`             |
| Callsign:                     | Indicativo de inicio de sesión para RBN.                                                                                            | `RbnCallsign`         |
| Rate Limit:                   | Limita los spots de RBN por segundo.                                                                                        | `RbnRateLimit`        |
| Connect / Disconnect (RBN)    | Activa o desactiva la conexión RBN.                                                                                           | —                     |
| Auto-connect on startup (RBN) | Inicia RBN automáticamente.                                                                                         | `RbnAutoConnect`      |
| RBN Console                   | Consola de solo lectura del tráfico de RBN.                                                                                 | —                     |
| Send (RBN)                    | Envía un comando a RBN.                                                                                             | —                     |
| Spot Color: (RBN)             | Selector de color para spots de RBN.                                                                                       | `RbnSpotColor`        |
| Startup Commands…             | Abre el editor de comandos de inicio para RBN. Los comandos se envían automáticamente después de cada inicio de sesión. Un comando por línea. | `RbnStartupCommands`  |

### Pestaña WSJT-X

| Control                              | Comportamiento                                                                                | Clave de configuración     |
|--------------------------------------|-----------------------------------------------------------------------------------------------|-----------------------------|
| Address:                             | Dirección de enlace UDP para mensajes de WSJT-X.                                                      | `WsjtxAddress`             |
| Port:                                | Puerto UDP para WSJT-X. Rango: 1–65535.                                                       | `WsjtxPort`                |
| Start / Stop                         | Inicia o detiene el listener UDP.                                                              | —                           |
| Auto-start on startup (WSJT-X)       | Inicia automáticamente el listener al iniciar.                                                            | `WsjtxAutoStart`           |
| CQ                                   | Muestra solo llamadas CQ de WSJT-X.                                                            | `WsjtxFilterCQ`            |
| CQ POTA                              | Muestra llamadas CQ POTA.                                                                        | `WsjtxFilterPOTA`          |
| Calling Me                           | Muestra solo decodificaciones dirigidas a su indicativo.                                              | `WsjtxFilterCallingMe`     |
| CQ color / POTA color / Calling Me color / Default color | Selectores de color para cada categoría de spot de WSJT-X.                     | `WsjtxColorCQ`, `WsjtxColorPOTA`, `WsjtxColorCallingMe`, `WsjtxColorDefault` |
| WSJT-X Decodes                       | Consola de transmisiones decodificadas.                                                         | —                           |
| Spot Life:                           | Segundos que los spots de WSJT-X permanecen en el panadapter.                                                 | `WsjtxSpotLife`            |

### Pestaña SpotCollector

| Control                              | Comportamiento                                                    | Clave de configuración     |
|--------------------------------------|-------------------------------------------------------------------|-----------------------------|
| UDP Port:                            | Puerto UDP en el que transmite SpotCollector. Rango: 1–65535.       | `SpotCollectorPort`         |
| Start / Stop (SpotCollector)         | Inicia o detiene el listener UDP.                               | —                           |
| Auto-start on startup (SpotCollector)| Inicia automáticamente el listener al iniciar.                             | `SpotCollectorAutoStart`    |
| SpotCollector Spots                  | Consola de spots de SpotCollector recibidos.                    | —                           |

### Pestaña POTA

| Control                        | Comportamiento                                              | Clave de configuración |
|--------------------------------|-------------------------------------------------------------|-----------------------|
| Server:                        | Muestra el endpoint fijo de POTA: api.pota.app (sondeo HTTP).| —                     |
| Poll Interval:                 | Segundos entre sondeos de POTA.                            | `PotaPollInterval`    |
| Start / Stop (POTA)            | Inicia o detiene el sondeo de POTA.                          | —                     |
| Auto-start on startup (POTA)   | Inicia POTA automáticamente al iniciar.                            | `PotaAutoStart`       |
| POTA Activations               | Consola del feed de activaciones.                            | —                     |
| Spot Color: (POTA)             | Selector de color para spots de POTA.                           | `PotaSpotColor`       |

### Pestaña FreeDV

| Control                          | Comportamiento                                                    | Clave de configuración |
|----------------------------------|-------------------------------------------------------------------|-------------------------|
| Server:                          | Muestra el endpoint fijo de FreeDV: qso.freedv.org (WebSocket).     | —                       |
| Start / Stop (FreeDV)            | Conecta o desconecta el WebSocket de FreeDV.                | —                       |
| Auto-start on startup (FreeDV)   | Inicia FreeDV automáticamente al iniciar.                                | `FreeDvAutoStart`       |
| FreeDV Spots                     | Consola de actividad de FreeDV.                                  | —                       |
| Spot Color: (FreeDV)             | Selector de color para spots de FreeDV.                               | `FreeDvSpotColor`       |

### Pestaña Spot List

| Control          | Comportamiento                                                                                                                | Clave de configuración |
|------------------|-------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| Bands:           | Las casillas de verificación por banda alternan la visibilidad de los spots en la tabla para cada banda de aficionados.       | Una casilla de verificación por banda: 160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m. Cada una se conserva como `SpotBandFilter_160m`, `SpotBandFilter_80m`, etc. Se almacena como una cadena `True`/`False`. La banda de 2m es reconocida por el modelo subyacente (para spots de FreeDV) pero no tiene una casilla de verificación correspondiente: los spots de 2m omiten el filtro y siempre son visibles. |
| Clear            | Elimina todos los spots mostrados actualmente en la tabla.                                                                          | —               |
| Spot table       | Tabla ordenable de spots; los spots se agrupan y vacían en la tabla una vez por segundo. Haga doble clic en una fila para sintonizar esa frecuencia y cambiar al modo del spot si se puede identificar. | Columnas (orden visual por índice de enumeración): Time, Freq (kHz), DX Call, Comment, Spotter, Band, Mode, Source. Mode (índice 6) se extrae automáticamente del campo Comment. El spot más nuevo siempre aparece en la parte superior. La tabla contiene un máximo de 500 spots. El modelo reconoce internamente la banda de 2m (144–148 MHz) para spots de FreeDV, pero no se muestra ninguna casilla de verificación de filtro para 2m en la interfaz de usuario; los spots de 2m siempre aparecen en la tabla independientemente del estado del filtro de banda. |

### Pestaña Display

| Control                                                  | Comportamiento                                                                                                                                                                                                                                           | Clave de configuración                                                                                                                                                           |
|----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Spots:                                                   | Activación general para la superposición de spots DX en el panadapter.                                                                                                                                                                                    | `IsSpotsEnabled`                                                                                                                                                                  |
| Memories:                                                | Activa o desactiva la superposición de canales de memoria en el panadapter.                                                                                                                                                                                                       | `IsMemorySpotsEnabled`                                                                                                                                                        |
| Auto:                                                    | Cambiar automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (p. ej. CW, FT8, RTTY).                                                                                                                                                      | La clave de configuración cambió de `SpotsAutoMode` a `SpotAutoSwitchMode` en v26.5.1.                                                                                                  |
| Signals (Signal History)                                 | Marcadores dorados para señales detectadas de ancho de voz en el panadapter.                                                                                                                                                                                        | Nuevo en v26.5.1 (#2426). Clave de configuración: `SHistoryMarkersEnabled`. Misma activación que View > Signal History Markers.                                                                  |
| QRM (Signal History)                                     | Marcadores rojos para portadoras persistentes e interferencia de banda ancha.                                                                                                                                                                                          | Nuevo en v26.5.1 (#2426). Clave de configuración: `SHistoryQrmEnabled`. Misma activación que View > QRM History Markers.                                                                         |
| Clear All                                                | Borra todos los spots DX, el feed de memoria, los marcadores de Signal History y los marcadores de QRM del espectro.                                                                                                                                                             | —                                                                                                                                                                             |
| Levels:                                                  | Número de filas de apilamiento vertical para los spots.                                                                                                                                                                                                             | La clave de configuración se migró de `SpotsStackLevels` en v0.9.7 a `SpotsMaxLevel`.                                                                                                    |
| Position:                                                | Posición vertical en el panadapter.                                                                                                                                                                                                                        | La clave de configuración se migró de `SpotsPosition` en v0.9.7 a `SpotsStartingHeightPercentage`.                                                                                       |
| Font Size:                                               | Tamaño del texto del spot.                                                                                                                                                                                                                                         | La clave de configuración se migró de `SpotsFontSize` en v0.9.7 a `SpotFontSize`.                                                                                                        |
| Spot Lifetime:                                           | Segundos antes de que un spot se desvanezca.                                                                                                                                                                                                                       | La clave de configuración se migró de `SpotsLifetime` en v0.9.7 a `DxClusterSpotLifetimeSec`. Migra la clave anterior basada en minutos `DxClusterSpotLifetime` en la primera lectura.                      |
| Override Colors:                                         | Fuerza un único color de texto para todos los spots.                                                                                                                                                                                                               | `IsSpotsOverrideColorsEnabled`                                                                                                                                                |
| Spot text color picker                                   | Abre QColorDialog para elegir el color del texto del spot.                                                                                                                                                                                                             | `SpotsOverrideColor`                                                                                                                                                          |
| Override Background: Enabled                             | Activa el color de fondo personalizado del spot.                                                                                                                                                                                                                   | `IsSpotsOverrideBackgroundColorsEnabled`                                                                                                                                      |
| Override Background: Auto                                | Selecciona automáticamente el color de fondo para el contraste.                                                                                                                                                                                                               | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                                                                                                 |
| Spot background color picker                             | Abre QColorDialog para el color de fondo del spot.                                                                                                                                                                                                           | `SpotsOverrideBgColor`                                                                                                                                                        |
| Background Opacity:                                      | Opacidad del color de fondo del spot.                                                                                                                                                                                                                       | La clave de configuración se migró de `SpotsOverrideBgOpacity` en v0.9.7 a `SpotsBackgroundOpacity`.                                                                                     |
| Spot Lines:                                              | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Activado por defecto. Desactívelo durante concursos para reducir el desorden visual.                                                                                                                     | `IsSpotsLinesEnabled`                                                                                                                                                         |
| Total Spots:                                             | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se actualiza cuando se añaden o borran spots. Se reinicia a 0 cuando se presiona "Clear All Spots".                                                                                    | —                                                                                                                                                                             |
| DXCC Colors:                                             | Colorea los spots según el estado de DXCC trabajado/confirmado/necesitado.                                                                                                                                                                                                    | La clave de configuración cambió de `DxccColoringEnabled` a `IsDxccColoringEnabled` en v26.5.1.                                                                                         |
| Log File (ADIF):                                         | Carga un archivo de registro ADIF para impulsar la coloración de DXCC. Vigila automáticamente el archivo en busca de cambios después de la selección.                                                                                                                                                       | La clave de configuración cambió de `DxccAdifPath` a `DxccAdifFilePath` en v26.5.1. La recarga automática siempre está activada cuando se selecciona un archivo (no hay una activación separada).                         |
| Imported: (DXCC stats)                                   | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro.                                                                                                                                                                                                  | Formato: '<N> QSOs / <M> entities'.                                                                                                                                            |
| DXCC Color swatches (New DXCC / New Band / New Mode / Worked) | Abre un selector de color para cada categoría de estado DXCC.
