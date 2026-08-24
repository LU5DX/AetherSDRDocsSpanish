# Sintonizar un Punto de Observación con Doble Clic en la Lista de Puntos

La pestaña "Spot List" de SpotHub muestra todos los puntos (spots) en vivo de todas las fuentes activas en una única tabla ordenable. Al hacer doble clic en una fila, se sintoniza el VFO activo a la frecuencia de ese punto. A partir de la versión v0.9.7, el doble clic también transmite la sugerencia de modo extraída del comentario del punto, de modo que el receptor cambia al modo correcto (por ejemplo, CW o FT8) y no solo cambia la frecuencia.

## Antes de comenzar

- Al menos una fuente de puntos (DX Cluster, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe estar conectada y recibiendo puntos.
- La radio debe estar conectada a AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña "Spot List".
3. Opcionalmente, use las casillas de verificación "Bands:" para filtrar la tabla por banda. Desmarque las bandas que no desee ver. Las casillas de banda usan un diseño de flujo que se ajusta a una nueva fila cuando el espacio horizontal es limitado, manteniendo las etiquetas legibles.
4. Haga clic en un encabezado de columna para ordenar la tabla por esa columna. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source. Al hacer clic en el encabezado Time se ordena por tiempo.
5. Haga clic derecho en cualquier encabezado de columna para abrir el menú de visibilidad de columnas. Alterne las acciones marcables en el menú para mostrar u ocultar columnas. El menú permanece abierto mientras alterna, de modo que puede ajustar varias columnas de una sola vez.
6. Haga doble clic en cualquier fila de la tabla de puntos. AetherSDR sintoniza el VFO activo a la frecuencia mostrada en esa fila. Si el punto contiene un modo reconocible en su campo de comentario, AetherSDR también cambia el slice a ese modo.

## Qué hace cada control

### Pestaña Cluster

| Control                    | Comportamiento                                                                                                                                              | Clave de ajuste         |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| Server:                    | Nombre de host del DX cluster al que conectarse.                                                                                                             | `ClusterHost`           |
| Port:                      | Puerto telnet del DX cluster. Rango: 1–65535.                                                                                                                 | `ClusterPort`           |
| Callsign:                  | Indicativo de inicio de sesión enviado al cluster.                                                                                                           | `ClusterCallsign`       |
| Connect / Disconnect       | Alterna la conexión telnet al cluster.                                                                                                                       | —                       |
| Auto-connect on startup    | Conecta el cluster automáticamente al inicio.                                                                                                                | `ClusterAutoConnect`    |
| Cluster Console            | Consola telnet de solo lectura del tráfico crudo del cluster.                                                                                                | —                       |
| Send                       | Envía un comando escrito al cluster.                                                                                                                         | —                       |
| Spot Color:                | Abre un selector de color para los puntos del cluster.                                                                                                       | `ClusterSpotColor`      |
| Startup Commands…          | Abre el editor de comandos de inicio. Los comandos se envían automáticamente después de cada inicio de sesión. Un comando por línea (p. ej. SET/NAME, SET/QTH, ACCEPT/SPOT). | `DxClusterStartupCommands` |

### Pestaña RBN

| Control                       | Comportamiento                                                                                                       | Clave de ajuste           |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------|---------------------------|
| Server:                       | Nombre de host telnet de RBN.                                                                                         | `RbnHost`                 |
| Port:                         | Puerto telnet de RBN. Rango: 1–65535.                                                                                 | `RbnPort`                 |
| Callsign:                     | Indicativo de inicio de sesión para RBN.                                                                              | `RbnCallsign`             |
| Rate Limit:                   | Limita los puntos RBN por segundo.                                                                                    | `RbnRateLimit`            |
| Connect / Disconnect (RBN)    | Alterna la conexión RBN.                                                                                              | —                         |
| Auto-connect on startup (RBN) | Inicia RBN automáticamente.                                                                                           | `RbnAutoConnect`          |
| RBN Console                   | Consola de solo lectura del tráfico RBN.                                                                              | —                         |
| Send (RBN)                    | Envía un comando a RBN.                                                                                               | —                         |
| Spot Color: (RBN)             | Selector de color para puntos RBN.                                                                                    | `RbnSpotColor`            |
| Startup Commands…             | Abre el editor de comandos de inicio para RBN. Los comandos se envían automáticamente después de cada inicio de sesión. Un comando por línea. | `RbnStartupCommands`      |

### Pestaña WSJT-X

| Control                              | Comportamiento                                                                                | Clave de ajuste                 |
|--------------------------------------|-----------------------------------------------------------------------------------------------|---------------------------------|
| Address:                             | Dirección de enlace UDP para mensajes WSJT-X.                                                 | `WsjtxAddress`                 |
| Port:                                | Puerto UDP para WSJT-X. Rango: 1–65535.                                                       | `WsjtxPort`                    |
| Start / Stop                         | Inicia o detiene el listener UDP.                                                             | —                               |
| Auto-start on startup (WSJT-X)       | Inicia el listener automáticamente al inicio.                                                 | `WsjtxAutoStart`               |
| CQ                                   | Mostrar solo llamadas CQ de WSJT-X.                                                           | `WsjtxFilterCQ`                |
| CQ POTA                              | Mostrar llamadas CQ POTA.                                                                     | `WsjtxFilterPOTA`              |
| Calling Me                           | Mostrar solo decodificaciones dirigidas a su indicativo.                                      | `WsjtxFilterCallingMe`         |
| CQ color / POTA color / Calling Me color / Default color | Selectores de color para cada categoría de punto WSJT-X.                    | `WsjtxColorCQ`, `WsjtxColorPOTA`, `WsjtxColorCallingMe`, `WsjtxColorDefault` |
| WSJT-X Decodes                       | Consola de transmisiones decodificadas.                                                       | —                               |
| Spot Life:                           | Segundos que los puntos WSJT-X permanecen en el panadapter.                                   | `WsjtxSpotLife`                |

### Pestaña SpotCollector

| Control                              | Comportamiento                                                  | Clave de ajuste                 |
|--------------------------------------|-----------------------------------------------------------------|---------------------------------|
| UDP Port:                            | Puerto UDP en el que SpotCollector transmite. Rango: 1–65535.   | `SpotCollectorPort`             |
| Start / Stop (SpotCollector)         | Inicia o detiene el listener UDP.                               | —                               |
| Auto-start on startup (SpotCollector)| Inicia el listener automáticamente al inicio.                   | `SpotCollectorAutoStart`        |
| SpotCollector Spots                  | Consola de puntos SpotCollector recibidos.                      | —                               |

### Pestaña POTA

| Control                        | Comportamiento                                             | Clave de ajuste           |
|--------------------------------|------------------------------------------------------------|---------------------------|
| Server:                        | Muestra el endpoint fijo de POTA: api.pota.app (sondeo HTTP). | —                         |
| Poll Interval:                 | Segundos entre sondeos de POTA.                             | `PotaPollInterval`        |
| Start / Stop (POTA)            | Inicia o detiene el sondeo de POTA.                         | —                         |
| Auto-start on startup (POTA)   | Inicia POTA automáticamente al inicio.                      | `PotaAutoStart`           |
| POTA Activations               | Consola del flujo de activaciones.                          | —                         |
| Spot Color: (POTA)             | Selector de color para puntos POTA.                         | `PotaSpotColor`           |

### Pestaña FreeDV

| Control                          | Comportamiento                                                  | Clave de ajuste             |
|----------------------------------|-----------------------------------------------------------------|-----------------------------|
| Server:                          | Muestra el endpoint fijo de FreeDV: qso.freedv.org (WebSocket).  | —                           |
| Start / Stop (FreeDV)            | Conecta o desconecta el WebSocket de FreeDV.                    | —                           |
| Auto-start on startup (FreeDV)   | Inicia FreeDV automáticamente al inicio.                         | `FreeDvAutoStart`           |
| FreeDV Spots                     | Consola de actividad de FreeDV.                                  | —                           |
| Spot Color: (FreeDV)             | Selector de color para puntos FreeDV.                            | `FreeDvSpotColor`           |

### Pestaña Spot List

| Control          | Comportamiento                                                                                                                                                                                                                                                                                             | Clave de ajuste     |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|
| Bands:           | Casillas de verificación por banda que alternan la visibilidad de los puntos en la tabla para cada banda de aficionados. Las casillas usan un diseño de flujo que se ajusta a una nueva fila cuando el espacio horizontal es limitado (#4157).                                                                                                                            | Una casilla por banda: 160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m. Cada una se guarda como `SpotBandFilter_160m`, `SpotBandFilter_80m`, etc. Almacenada como cadena `True`/`False`. La banda de 2m es reconocida por el modelo subyacente (para puntos FreeDV) pero no tiene casilla correspondiente — los puntos de 2m omiten el filtro y siempre son visibles. |
| Clear            | Elimina todos los puntos mostrados actualmente en la tabla.                                                                                                                                                                                                                                                  | —                   |
| Spot table       | Tabla ordenable de puntos; los puntos se agrupan y se descargan a la tabla una vez por segundo. Haga doble clic en una fila para sintonizar esa frecuencia y cambiar al modo del punto si se puede identificar. Haga clic derecho en cualquier encabezado de columna para abrir el menú de visibilidad de columnas — el menú permanece abierto mientras alterna, de modo que puede mostrar u ocultar varias columnas de una sola vez (#4157). | Columnas (orden visual por índice de enumeración): Time, Freq (kHz), DX Call, Comment, Spotter, Band, Mode, Source. Mode (índice 6) se extrae automáticamente del campo Comment. El punto más nuevo siempre aparece arriba. La tabla contiene como máximo 500 puntos. El modelo reconoce internamente la banda de 2m (144–148 MHz) para puntos FreeDV, pero no se muestra ninguna casilla de filtro para 2m en la interfaz — los puntos de 2m siempre aparecen en la tabla independientemente del estado del filtro de banda. |

### Pestaña Display

| Control                                                  | Comportamiento                                                                                                                                                                                                                                                | Clave de ajuste                                                                                                                                                                   |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Spots:                                                   | Interruptor principal para la superposición de puntos DX en el panadapter.                                                                                                                                                                                      | `IsSpotsEnabled`                                                                                                                                                                  |
| Memories:                                                | Alterna la superposición de canales de memoria en el panadapter.                                                                                                                                                                                                | `IsMemorySpotsEnabled`                                                                                                                                                            |
| Auto:                                                    | Cambia automáticamente el modo del slice al hacer clic en un punto que incluya información de modo (p. ej. CW, FT8, RTTY).                                                                                                                                      | La clave de ajuste cambió de `SpotsAutoMode` a `SpotAutoSwitchMode` en v26.5.1.                                                                                                   |
| Signals (Signal History)                                 | Marcadores dorados para señales detectadas de ancho de voz en el panadapter.                                                                                                                                                                                    | Nuevo en v26.5.1 (#2426). Clave de ajuste: `SHistoryMarkersEnabled`. Mismo interruptor que View > Signal History Markers.                                                         |
| QRM (Signal History)                                     | Marcadores rojos para portadoras persistentes e interferencia de banda ancha.                                                                                                                                                                                  | Nuevo en v26.5.1 (#2426). Clave de ajuste: `SHistoryQrmEnabled`. Mismo interruptor que View > QRM History Markers.                                                                |
| Clear All                                                | Limpia todos los puntos DX, el flujo de memoria, los marcadores de Signal History y los marcadores QRM del espectro.                                                                                                                                            | —                                                                                                                                                                                 |
| Levels:                                                  | Número de filas de apilamiento vertical para los puntos.                                                                                                                                                                                                        | La clave de ajuste migró de `SpotsStackLevels` en v0.9.7 a `SpotsMaxLevel`.                                                                                                       |
| Position:                                                | Posición vertical en el panadapter.                                                                                                                                                                                                                             | La clave de ajuste migró de `SpotsPosition` en v0.9.7 a `SpotsStartingHeightPercentage`.                                                                                          |
| Font Size:                                               | Tamaño del texto de los puntos.                                                                                                                                                                                                                                 | La clave de ajuste migró de `SpotsFontSize` en v0.9.7 a `SpotFontSize`.                                                                                                           |
| Spot Lifetime:                                           | Segundos antes de que un punto se desvanezca.                                                                                                                                                                                                                   | La clave de ajuste migró de `SpotsLifetime` en v0.9.7 a `DxClusterSpotLifetimeSec`. Migra la clave antigua basada en minutos `DxClusterSpotLifetime` en la primera lectura.        |
| Override Colors:                                         | Fuerza un único color de texto para todos los puntos. El botón de alternancia siempre muestra "Enabled" independientemente del estado.                                                                                                                           | `IsSpotsOverrideColorsEnabled`                                                                                                                                                    |
| Spot text color picker                                   | Abre QColorDialog para elegir el color del texto de los puntos.                                                                                                                                                                                                 | `SpotsOverrideColor`                                                                                                                                                              |
| Override Background: Enabled                             | Activa un color de fondo personalizado para los puntos.                                                                                                                                                                                                         | `IsSpotsOverrideBackgroundColorsEnabled`                                                                                                                                          |
| Override Background: Auto                                | Selecciona automáticamente el color de fondo para contraste.                                                                                                                                                                                                    | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                                                                                                     |
| Spot background color picker                             | Abre QColorDialog para el color de fondo de los puntos.                                                                                                                                                                                                         | `SpotsOverrideBgColor`                                                                                                                                                            |
| Background Opacity:                                      | Opacidad del color de fondo de los puntos.                                                                                                                                                                                                                      | La clave de ajuste migró de `SpotsOverrideBgOpacity` en v0.9.7 a `SpotsBackgroundOpacity`.                                                                                        |
| Spot Lines:                                              | Dibuja líneas verticales desde el espectro hasta cada etiqueta de punto. El botón de alternancia siempre muestra "Enabled" independientemente del estado. Desactívelo durante concursos para reducir el desorden visual.                                          | `IsSpotsLinesEnabled`                                                                                                                                                             |
| Total Spots:                                             | Lectura en vivo de cuántos puntos se rastrean actualmente en todas las fuentes. Se actualiza cuando se agregan o limpian puntos. Se restablece a 0 cuando se presiona "Clear All Spots".                                                                        | —                                                                                                                                                                                 |
| DXCC Colors:                                             | Colorea los puntos según el estado DXCC trabajado/confirmado/necesario. El botón de alternancia siempre muestra "Enabled" independientemente del estado.                                                                                                         | La clave de ajuste cambió de `DxccColoringEnabled` a `IsDx
