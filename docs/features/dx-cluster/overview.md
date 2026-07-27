# Resumen de SpotHub

SpotHub es el centro central de AetherSDR para recibir spots de DX de múltiples fuentes y mostrarlos como superposiciones en el panadapter. Úselo para conectarse a clústeres de DX tradicionales, la Reverse Beacon Network, WSJT-X, SpotCollector, POTA y FreeDV, todo desde un solo diálogo.

## Antes de comenzar

- Abra SpotHub a través de `Settings > SpotHub...`. No se requiere conexión de radio.
- Tenga preparado su indicativo de inicio de sesión si planea conectarse a un clúster de DX o a RBN.
- Tenga disponible un archivo de registro ADIF si desea el coloreado por DXCC.

## Cómo funciona

SpotHub agrega spots de hasta seis fuentes independientes. Cada fuente se ejecuta de forma independiente; puede activar cualquier combinación simultáneamente. Todos los spots entrantes se fusionan en una lista unificada y se representan como marcadores de frecuencia en el panadapter.

Los spots de cada fuente se codifican por colores por separado para que pueda distinguir su origen de un vistazo. Una capa de visualización global (la pestaña **Display**) controla cómo aparecen todos los spots en el panadapter, independientemente de la fuente.

### Fuentes

**Pestaña Cluster** — Se conecta a un clúster de DX a través de una sesión telnet. Usted proporciona el nombre de host (`ClusterHost`), el puerto (`ClusterPort`, 1–65535) y el indicativo de inicio de sesión (`ClusterCallsign`). La **Cluster Console** muestra el tráfico telnet sin procesar. Puede escribir comandos del clúster en el campo de línea de comandos y enviarlos con **Send**. El color del spot se establece mediante **Spot Color:**, que se guarda como `ClusterSpotColor`.

El botón **Startup Commands…** abre un editor para los comandos del clúster que se envían automáticamente después de cada inicio de sesión. Ingrese un comando por línea, por ejemplo, `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`. Los comandos se guardan como `DxClusterStartupCommands` y el cliente del clúster los reproduce después de cada inicio de sesión.

**Pestaña RBN** — Se conecta a la Reverse Beacon Network a través de telnet. La configuración es similar a la pestaña Cluster: `RbnHost`, `RbnPort` (1–65535), `RbnCallsign`. El cuadro de giro **Rate Limit:** (`RbnRateLimit`) limita la cantidad de spots aceptados por segundo, lo cual es útil porque el volumen de tráfico de RBN puede ser muy alto. La **RBN Console** muestra el tráfico sin procesar. El color del spot se establece mediante **Spot Color:** (`RbnSpotColor`).

El botón **Startup Commands…** abre un editor para comandos de clúster específicos de RBN que se envían automáticamente después de cada inicio de sesión. Ingrese un comando por línea. Los comandos se guardan como `RbnStartupCommands` y se reproducen de forma independiente de los comandos de inicio del clúster de DX.

**Pestaña WSJT-X** — Escucha datagramas UDP transmitidos por una instancia en ejecución de WSJT-X. Establezca la dirección de enlace (`WsjtxAddress`) y el puerto (`WsjtxPort`, 1–65535), luego haga clic en **Start**. Tres casillas de verificación filtran qué decodificaciones aparecen como spots: **CQ** (`WsjtxFilterCQ`), **CQ POTA** (`WsjtxFilterPOTA`) y **Calling Me** (`WsjtxFilterCallingMe`). Cada categoría tiene su propio selector de color: color CQ (`WsjtxColorCQ`), color POTA (`WsjtxColorPOTA`), color Calling Me (`WsjtxColorCallingMe`) y color Predeterminado (`WsjtxColorDefault`). **Spot Life:** (`WsjtxSpotLife`) controla cuánto tiempo permanecen los spots de WSJT-X en el panadapter. La consola **WSJT-X Decodes** muestra el flujo de decodificaciones sin procesar.

**Pestaña SpotCollector** — Escucha en un puerto UDP las transmisiones de spots de Ham Radio Deluxe SpotCollector. Establezca **UDP Port:** (`SpotCollectorPort`, 1–65535) y haga clic en **Start**. La consola **SpotCollector Spots** muestra los spots recibidos.

**Pestaña POTA** — Consulta `api.pota.app` a través de HTTP en un intervalo configurable (**Poll Interval:**, `PotaPollInterval`). La dirección del servidor es fija y se muestra como un indicador. La consola **POTA Activations** muestra el feed de activaciones. El color del spot se establece mediante **Spot Color:** (`PotaSpotColor`).

**Pestaña FreeDV** — Se conecta al FreeDV QSO Reporter a través de WebSocket en `qso.freedv.org`. La dirección del servidor es fija. La consola **FreeDV Spots** muestra la actividad. El color del spot se establece mediante **Spot Color:** (`FreeDvSpotColor`). Esta pestaña solo está presente en las compilaciones que incluyen soporte para WebSocket.

### Conexión e inicio automáticos

Cada fuente tiene una opción **Auto-connect on startup** o **Auto-start on startup**. Cuando está activada, esa fuente se conecta o se inicia automáticamente cada vez que se lanza AetherSDR, sin intervención manual. Las claves guardadas son `ClusterAutoConnect`, `RbnAutoConnect`, `WsjtxAutoStart`, `SpotCollectorAutoStart`, `PotaAutoStart` y `FreeDvAutoStart`.

### Pestaña Spot List

La pestaña **Spot List** muestra una tabla unificada y ordenable de todos los spots activos de todas las fuentes activas. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band y Source. Las casillas de verificación por banda debajo de **Bands:** activan o desactivan la visibilidad de cada banda de aficionados. Las casillas de verificación utilizan un diseño de flujo que se ajusta a nuevas filas cuando el diálogo de SpotHub es estrecho, manteniendo cada casilla legible. Haga clic en **Clear** para vaciar la lista actual. Haga doble clic en cualquier fila para sintonizar el VFO activo a la frecuencia de ese spot y, cuando el spot contenga información de modo (por ejemplo, CW, FT8 o RTTY), cambie automáticamente el slice a ese modo.

El menú del encabezado de columna muestra u oculta columnas individuales. Haga clic en el menú contextual del encabezado para activar o desactivar columnas. El menú permanece abierto mientras alterna varias columnas marcables, para que pueda mostrar u ocultar varias columnas de una sola vez sin que el menú se cierre después de cada clic.

### Pestaña Display

La pestaña **Display** controla cómo aparecen los spots en el panadapter.

| Control | Clave de configuración | Valor predeterminado |
|---|---|---|
| **Spots:** | `IsSpotsEnabled` | Activado |
| **Memories:** | `IsMemorySpotsEnabled` | Desactivado |
| **Auto:** | `SpotAutoSwitchMode` | Activado |
| **Signals (Signal History)** | `SHistoryMarkersEnabled` | Desactivado |
| **QRM (Signal History)** | `SHistoryQrmEnabled` | Desactivado |
| **Clear All** | — | — |
| **Levels:** | `SpotsMaxLevel` | 3 |
| **Position:** | `SpotsStartingHeightPercentage` | 50 |
| **Font Size:** | `SpotFontSize` | 16 |
| **Spot Lifetime:** | `DxClusterSpotLifetimeSec` | — |
| **Override Colors:** | `IsSpotsOverrideColorsEnabled` | — |
| **Selector de color de texto de spot** | `SpotsOverrideColor` | #FFFF00 |
| **Override Background: Enabled** | `IsSpotsOverrideBackgroundColorsEnabled` | Activado |
| **Override Background: Auto** | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Activado |
| **Selector de color de fondo de spot** | `SpotsOverrideBgColor` | #000000 |
| **Background Opacity:** | `SpotsBackgroundOpacity` | 48 |
| **Spot Lines:** | `IsSpotsLinesEnabled` | Activado |
| **Total Spots:** | Lectura en vivo de cuántos spots se rastrean actualmente en todas las fuentes. | Se actualiza cada vez que se añaden o borran spots. Se restablece a 0 al presionar **Clear All** |
| **DXCC Coloring (sección)** | Encabezado de sección para los controles de coloreado DXCC en la columna izquierda debajo del divisor. | — |
| **DXCC Colors:** | `IsDxccColoringEnabled` | — |
| **Log File (ADIF):** | `DxccAdifFilePath` | — |
| **Imported: (estadísticas DXCC)** | Muestra el recuento de QSO y de entidades cuando se carga un registro. | (sin registro cargado) |
| **Muestras de color DXCC (New DXCC / New Band / New Mode / Worked)** | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` | — |
| **Signal History (sección)** | Encabezado de sección para los parámetros ajustables de Signal History en la columna derecha debajo del divisor. | — |
| **Marker Lifetime:** | `SHistoryLifetimeS` | 60 s |
| **QRM Gate:** | `SHistoryQrmGateS` | 6 s |
| **Edge Threshold:** | `SHistorySoftEdgeDb` | 3.0 dB |
| **Muestras de color de Signal History (Signals / QRM)** | `SHistoryColorSignals` / `SHistoryColorQrm` | #FFC800 / #FF0000 |
| **Snap to Step:** | `SHistorySnapToStep` | Desactivado |

**Spot Lines:** dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir el desorden visual. La configuración se guarda como `IsSpotsLinesEnabled` y el valor predeterminado es Activado.

**Auto:** el valor predeterminado es **Activado** (`SpotAutoSwitchMode` predeterminado en `True`). Si anteriormente confiaba en que el Modo Automático estuviera desactivado de forma predeterminada, verifique esta configuración después de actualizar.

**Override Colors:** el botón siempre muestra el texto "Enabled". Cuando está marcado, fuerza un color de texto único para todos los spots. La etiqueta del botón no cambia al alternarlo.

**DXCC Colors:** el botón siempre muestra el texto "Enabled". Cuando está marcado, colorea los spots según el estado de DXCC trabajado/confirmado/necesario. La etiqueta del botón no cambia al alternarlo.

**Spot Lines:** el botón siempre muestra el texto "Enabled". Cuando está marcado, dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. La etiqueta del botón no cambia al alternarlo.

**Snap to Step:** el botón siempre muestra el texto "Enabled". Cuando está marcado, redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo. La etiqueta del botón no cambia al alternarlo.

## Informes del FreeDV Reporter

La pestaña **FreeDV** incluye una sección **Station Reporting** que permite a AetherSDR transmitir su actividad de estación al mapa público del FreeDV Reporter en `qso.freedv.org` siempre que el módem RADE esté activo. Esta función solo está presente en las compilaciones compiladas con soporte para WebSocket.

### Habilitar informes

1. Abra la pestaña **FreeDV**.
2. Complete un indicativo y un cuadrado de cuadrícula válidos en los campos **Callsign:** y **Grid Square:** (ver más abajo). La casilla de verificación se negará a activarse si alguno de los campos está en blanco o no se puede resolver.
3. Marque **Enable FreeDV Reporter reporting when RADE is active** (`FreeDvAutoReport`). Si el indicativo o la cuadrícula no se pueden resolver, aparecerá un diálogo de advertencia y la casilla de verificación volverá al estado desmarcado.

> **Nota:** Los datos del Reporter se publican en un mapa público compartido por la comunidad. No active los informes con valores de marcador de posición.

#### Campo de indicativo

| Control | Clave de configuración | Valor predeterminado | Notas |
|---|---|---|---|
| **Callsign:** | `FreeDvMyCallsign` | — | El indicativo enviado al mapa del FreeDV Reporter. El campo es de solo lectura cuando **Use radio** está marcado. |
| **Use radio** | `FreeDvUseRadioCallsign` | True | Precarga el indicativo desde el indicativo configurado en la radio y bloquea el campo como solo lectura. Se actualiza automáticamente si cambia el indicativo en Radio Setup. |

Cuando **Use radio** está marcado, el campo muestra el indicativo de la radio. Desmárquelo para ingresar un indicativo manualmente.

#### Campo de cuadrado de cuadrícula

| Control | Clave de configuración | Valor predeterminado | Notas |
|---|---|---|---|
| **Grid Square:** | `FreeDvMyGrid` | — | Cuadrado de cuadrícula de Maidenhead enviado al mapa del FreeDV Reporter. El campo es de solo lectura cuando **Use GPS** está marcado. |
| **Use GPS** | `FreeDvUseGpsGrid` | True | Precarga la cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. |

#### Mensaje de estación

| Control | Clave de configuración | Valor predeterminado | Notas |
|---|---|---|---|
| **Station Msg:** | `FreeDvMyMessage` | — | Texto libre opcional que se muestra junto a su indicativo en el mapa público del FreeDV Reporter. |

## Superposición de barrido de ROE

La versión V0.9.4 añade una superposición de barrido de ROE que traza la ROE frente a la frecuencia directamente en el panadapter. Una fuente externa (por ejemplo, una integración de analizador de antenas) proporciona los datos llamando a `setSwrSweepPoints()`. El panadapter representa la curva a través de la capa interna `drawSwrSweep()`.

### Suministro de datos de barrido

Llame a `setSwrSweepPoints()` con un vector de valores `SwrSweepPoint`. Cada punto tiene dos campos:

| Campo | Tipo | Valor predeterminado | Descripción |
|---|---|---|---|
| `freqMhz` | `double` | `0.0` | Frecuencia de la medición en MHz. |
| `swr` | `float` | `1.0` | Valor de ROE en esa frecuencia. |

La firma del método es:

```
setSwrSweepPoints(p
