# Resumen de SpotHub

SpotHub es el centro central de AetherSDR para recibir spots de DX de múltiples fuentes y mostrarlos como superposiciones en el panadapter. Úselo para conectarse a clústeres de DX tradicionales, la Reverse Beacon Network, WSJT-X, SpotCollector, POTA y FreeDV, todo desde un solo diálogo.

## Antes de comenzar

- Abra SpotHub mediante `Settings > SpotHub...`. No se requiere conexión de radio.
- Tenga listo su indicativo de inicio de sesión si planea conectarse a un clúster de DX o a RBN.
- Tenga disponible un archivo de registro ADIF si desea el coloreado por DXCC.

## Cómo funciona

SpotHub agrega spots de hasta ocho fuentes independientes. Cada fuente funciona de forma independiente: puede habilitar cualquier combinación simultáneamente. Todos los spots entrantes se combinan en una lista unificada y se muestran como marcadores de frecuencia en el panadapter.

Los spots de cada fuente se codifican por colores por separado para que pueda distinguir su origen de un vistazo. Una capa de visualización global (la pestaña **Display**) controla cómo aparecen todos los spots en el panadapter, independientemente de la fuente.

### Fuentes

**Pestaña Cluster** — Se conecta a un clúster de DX mediante una sesión telnet. Usted proporciona el nombre de host (`ClusterHost`), el puerto (`ClusterPort`, 1–65535) y el indicativo de inicio de sesión (`ClusterCallsign`). La **Cluster Console** muestra el tráfico telnet crudo. Puede escribir comandos del clúster en el campo de línea de comandos y enviarlos con **Send**. El color del spot se establece mediante **Spot Color:** y se guarda como `ClusterSpotColor`.

El botón **Startup Commands…** abre un editor para los comandos del clúster que se envían automáticamente después de cada inicio de sesión. Ingrese un comando por línea, por ejemplo `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`. Los comandos se guardan como `DxClusterStartupCommands` y el cliente del clúster los reproduce después de cada inicio de sesión.

**Pestaña RBN** — Se conecta a la Reverse Beacon Network mediante telnet. La configuración es equivalente a la pestaña Cluster: `RbnHost`, `RbnPort` (1–65535), `RbnCallsign`. El cuadro giratorio **Rate Limit:** (`RbnRateLimit`) limita la cantidad de spots aceptados por segundo, lo cual es útil porque el volumen de tráfico de RBN puede ser muy alto. La **RBN Console** muestra el tráfico crudo. El color del spot se establece mediante **Spot Color:** (`RbnSpotColor`).

El botón **Startup Commands…** abre un editor para comandos específicos de RBN que se envían automáticamente después de cada inicio de sesión. Ingrese un comando por línea. Los comandos se guardan como `RbnStartupCommands` y se reproducen de forma independiente de los comandos de inicio del clúster de DX.

**Pestaña WSJT-X** — Escucha los datagramas UDP transmitidos por una instancia de WSJT-X en ejecución. Establezca la dirección de enlace (`WsjtxAddress`) y el puerto (`WsjtxPort`, 1–65535), luego haga clic en **Start**. Tres casillas de verificación filtran qué decodificaciones aparecen como spots: **CQ** (`WsjtxFilterCQ`), **CQ POTA** (`WsjtxFilterPOTA`) y **Calling Me** (`WsjtxFilterCallingMe`). Cada categoría tiene su propio selector de color: color CQ (`WsjtxColorCQ`), color POTA (`WsjtxColorPOTA`), color Calling Me (`WsjtxColorCallingMe`) y color predeterminado (`WsjtxColorDefault`). **Spot Life:** (`WsjtxSpotLife`) controla cuánto tiempo permanecen los spots de WSJT-X en el panadapter. La consola **WSJT-X Decodes** muestra el flujo de decodificaciones crudas.

**Pestaña SpotCollector** — Escucha en un puerto UDP las transmisiones de spots de Ham Radio Deluxe SpotCollector. Establezca **UDP Port:** (`SpotCollectorPort`, 1–65535) y haga clic en **Start**. La consola **SpotCollector Spots** muestra los spots recibidos.

**Pestaña POTA** — Consulta `api.pota.app` mediante HTTP en un intervalo configurable (**Poll Interval:**, `PotaPollInterval`). La dirección del servidor es fija y se muestra como un indicador. La consola **POTA Activations** muestra el flujo de activaciones. El color del spot se establece mediante **Spot Color:** (`PotaSpotColor`).

**Pestaña FreeDV** — Se conecta al QSO Reporter de FreeDV mediante WebSocket en `qso.freedv.org`. La dirección del servidor es fija. La consola **FreeDV Spots** muestra la actividad. El color del spot se establece mediante **Spot Color:** (`FreeDvSpotColor`). Esta pestaña solo está presente en compilaciones que incluyen soporte WebSocket.

**Pestaña Eibi** — Consulta la base de datos de onda corta EiBi para obtener spots de transmisión actuales. La dirección del servidor es fija. La consola **Eibi Spots** muestra el flujo. El color del spot se establece mediante **Spot Color:** (`EibiSpotColor`).

**Pestaña N1MM** — Escucha mensajes de spot de N1MM Logger+. Establezca el puerto UDP y haga clic en **Start**. La consola **N1MM Spots** muestra los spots recibidos. El color del spot se establece mediante **Spot Color:** (`N1mmSpotColor`).

### Auto-conexión y auto-inicio

Cada fuente tiene un conmutador **Auto-connect on startup** o **Auto-start on startup**. Cuando está habilitado, esa fuente se conecta o se inicia automáticamente cada vez que se lanza AetherSDR, sin intervención manual. Las claves guardadas son `ClusterAutoConnect`, `RbnAutoConnect`, `WsjtxAutoStart`, `SpotCollectorAutoStart`, `PotaAutoStart`, `FreeDvAutoStart`, `EibiAutoStart` y `N1mmAutoStart`.

### Pestaña Spot List

La pestaña **Spot List** muestra una tabla unificada y ordenable de todos los spots activos de todas las fuentes activas. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band y Source. Las casillas de verificación por banda debajo de **Bands:** alternan la visibilidad de cada banda de aficionados. Las casillas utilizan un diseño de flujo que se ajusta a nuevas filas cuando el diálogo de SpotHub es angosto, manteniendo cada casilla legible. Haga clic en **Clear** para vaciar la lista actual. Haga doble clic en cualquier fila para sintonizar el VFO activo a la frecuencia de ese spot y, cuando el spot incluya información de modo (por ejemplo, CW, FT8 o RTTY), cambie automáticamente el slice a ese modo.

Las columnas **Time** y **Freq** se ordenan numéricamente al hacer clic en sus encabezados; todas las demás columnas se ordenan alfabéticamente. Ordenar por Time restablece el orden más reciente primero si ha ordenado por otra columna.

El menú de encabezado de columna muestra u oculta columnas individuales. Haga clic en el menú contextual del encabezado para alternar columnas. El menú permanece abierto mientras alterna varias columnas marcables, de modo que puede mostrar u ocultar varias columnas de una sola vez sin que el menú se cierre después de cada clic.

### Pestaña Display

La pestaña **Display** controla cómo aparecen los spots en el panadapter.

| Control                                                       | Clave de configuración                                                                                                  | Predeterminado                                                                                                      |
|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **Spots:**                                                    | `IsSpotsEnabled`                                                                                                         | Habilitado                                                                                                          |
| **Memories:**                                                 | `IsMemorySpotsEnabled`                                                                                                   | Deshabilitado                                                                                                       |
| **Auto:**                                                     | `SpotAutoSwitchMode`                                                                                                     | Habilitado                                                                                                          |
| **Signals (Signal History)**                                  | `SHistoryMarkersEnabled`                                                                                                 | Deshabilitado                                                                                                       |
| **QRM (Signal History)**                                      | `SHistoryQrmEnabled`                                                                                                     | Deshabilitado                                                                                                       |
| **Clear All**                                                 | —                                                                                                                        | —                                                                                                                  |
| **Levels:**                                                   | `SpotsMaxLevel`                                                                                                          | 3                                                                                                                  |
| **Position:**                                                 | `SpotsStartingHeightPercentage`                                                                                          | 50                                                                                                                 |
| **Font Size:**                                                | `SpotFontSize`                                                                                                           | 16                                                                                                                 |
| **Spot Lifetime:**                                            | `DxClusterSpotLifetimeSec`                                                                                               | —                                                                                                                  |
| **Override Colors:**                                          | `IsSpotsOverrideColorsEnabled`                                                                                           | —                                                                                                                  |
| **Selector de color de texto del spot**                       | `SpotsOverrideColor`                                                                                                     | #FFFF00                                                                                                            |
| **Override Background: Enabled**                              | `IsSpotsOverrideBackgroundColorsEnabled`                                                                                 | Habilitado                                                                                                          |
| **Override Background: Auto**                                 | `IsSpotsOverrideToAutoBackgroundColorEnabled`                                                                            | Habilitado                                                                                                          |
| **Selector de color de fondo del spot**                       | `SpotsOverrideBgColor`                                                                                                   | #000000                                                                                                            |
| **Background Opacity:**                                       | `SpotsBackgroundOpacity`                                                                                                 | 48                                                                                                                 |
| **Spot Lines:**                                               | `IsSpotsLinesEnabled`                                                                                                    | Habilitado                                                                                                          |
| **Total Spots:**                                              | Lectura en vivo de cuántos spots se rastrean actualmente en todas las fuentes.                                           | Se actualiza cada vez que se agregan o borran spots. Vuelve a 0 al presionar **Clear All**.                        |
| **DXCC Coloring (sección)**                                   | Encabezado de sección para los controles de coloreado DXCC en la columna izquierda debajo del divisor.                   | —                                                                                                                  |
| **DXCC Colors:**                                              | `IsDxccColoringEnabled`                                                                                                  | —                                                                                                                  |
| **Log File (ADIF):**                                          | `DxccAdifFilePath`                                                                                                       | —                                                                                                                  |
| **Imported: (estadísticas DXCC)**                             | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro.                                       | (sin registro cargado)                                                                                             |
| **Muestras de color DXCC (New DXCC / New Band / New Mode / Worked)** | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked`                                     | —                                                                                                                  |
| **Signal History (sección)**                                  | Encabezado de sección para los parámetros ajustables de Signal History en la columna derecha debajo del divisor.         | —                                                                                                                  |
| **Marker Lifetime:**                                          | `SHistoryLifetimeS`                                                                                                      | 60 s                                                                                                               |
| **QRM Gate:**                                                 | `SHistoryQrmGateS`                                                                                                       | 6 s                                                                                                                |
| **Edge Threshold:**                                           | `SHistorySoftEdgeDb`                                                                                                     | 3.0 dB                                                                                                             |
| **Muestras de color de Signal History (Signals / QRM)**       | `SHistoryColorSignals` / `SHistoryColorQrm`                                                                              | #FFC800 / #FF0000                                                                                                  |
| **Snap to Step:**                                             | `SHistorySnapToStep`                                                                                                     | Deshabilitado                                                                                                       |

**Spot Lines:** dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot. Deshabilítelo durante concursos para reducir el desorden visual. La configuración se guarda como `IsSpotsLinesEnabled` y tiene como valor predeterminado Habilitado.

**Auto:** tiene como valor predeterminado **Habilitado** (`SpotAutoSwitchMode` tiene como valor predeterminado `True`). Si anteriormente dependía de que el modo Auto estuviera deshabilitado por defecto, verifique esta configuración después de actualizar.

**Override Colors:** el botón siempre muestra el texto "Enabled". Cuando está marcado, fuerza un solo color de texto para todos los spots. La etiqueta del botón no cambia al alternarlo.

**DXCC Colors:** el botón siempre muestra el texto "Enabled". Cuando está marcado, colorea los spots según el estado de DXCC trabajado/confirmado/necesario. La etiqueta del botón no cambia al alternarlo.

**Spot Lines:** el botón siempre muestra el texto "Enabled". Cuando está marcado, dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. La etiqueta del botón no cambia al alternarlo.

**Snap to Step:** el botón siempre muestra el texto "Enabled". Cuando está marcado, redondea el clic para sintonizar del Signal History al múltiplo más cercano del tamaño de paso del slice activo. La etiqueta del botón no cambia al alternarlo.

## Informes a FreeDV Reporter

La pestaña **FreeDV** incluye una sección **Station Reporting** que permite a AetherSDR transmitir la actividad de su estación al mapa público de FreeDV Reporter en `qso.freedv.org` siempre que el módem RADE esté activo. Esta función solo está presente en compilaciones compiladas con soporte WebSocket.

### Habilitar los informes

1. Abra la pestaña **FreeDV**.
2. Complete un indicativo y una cuadrícula válidos en los campos **Callsign:** y **Grid Square:** (consulte a continuación). La casilla de verificación se niega a habilitarse si alguno de los campos está vacío o no se puede resolver.
3. Marque **Enable FreeDV Reporter reporting when RADE is active** (`FreeDvAutoReport`). Si el indicativo o la cuadrícula no se pueden resolver, aparece un diálogo de advertencia y la casilla de verificación vuelve a su estado desmarcado.

> **Nota:** Los datos de Reporter se publican en un mapa público compartido por la comunidad. No habilite los informes con valores de marcador de posición.

#### Campo Callsign

| Control | Clave de configuración | Predeterminado | Notas |
|---|---|---|---|
| **Callsign:** | `FreeDvMyCallsign` | — | El indicativo enviado al mapa de FreeDV Reporter. El campo es de solo lectura cuando **Use radio** está marcado. |
| **Use radio** | `FreeDvUseRadioCallsign` | True | Rellena previamente el indicativo desde el indicativo configurado de la radio y bloquea el campo como solo lectura. Se actualiza automáticamente si cambia el indicativo en Radio Setup. |

Cuando **Use radio** está marcado, el campo muestra el indicativo de la radio. Desmárquelo para ingresar un indicativo manualmente.

#### Campo Grid Square

| Control | Clave de configuración | Predeterminado | Notas |
|---|---|---|---|
| **Grid Square:** | `FreeDvMyGrid` | — | Cuadrícula Maidenhead enviada al mapa de FreeDV Reporter. El campo es de solo lectura cuando **Use GPS** está marcado. |
| **Use GPS** | `FreeDvUseGpsGrid` | True | Rellena previamente la cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. |

#### Mensaje de estación

| Control | Clave de configuración | Predeterminado | Notas |
|---|---|---|---|
| **Station Msg:** | `FreeDvMyMessage` | — | Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público de FreeDV Reporter. Limitado a 100 caracteres. |
