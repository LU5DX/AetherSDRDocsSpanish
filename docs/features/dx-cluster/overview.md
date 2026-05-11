# Resumen de SpotHub

SpotHub es el centro central de AetherSDR para recibir spots DX de múltiples fuentes y mostrarlos como superposiciones en el panadapter. Úselo para conectarse a clústeres DX tradicionales, la Reverse Beacon Network, WSJT-X, SpotCollector, POTA y FreeDV, todo desde un solo diálogo.

## Antes de comenzar

- Abra SpotHub mediante `Settings > SpotHub...`. No se requiere conexión de radio.
- Tenga listo su indicativo de inicio de sesión si planea conectarse a un clúster DX o a RBN.
- Tenga disponible un archivo de registro en formato ADIF si desea usar la coloración por DXCC.

## Cómo funciona

SpotHub agrega spots de hasta seis fuentes independientes. Cada fuente se ejecuta de forma independiente; puede habilitar cualquier combinación simultáneamente. Todos los spots entrantes se fusionan en una lista unificada y se representan como marcadores de frecuencia en el panadapter.

Los spots de cada fuente se codifican con colores separados para que pueda distinguir su origen de un vistazo. Una capa de visualización global (la pestaña **Display**) controla cómo aparecen todos los spots en el panadapter, independientemente de la fuente.

### Fuentes

**Pestaña Cluster** — Se conecta a un clúster DX mediante una sesión telnet. Proporcione el nombre de host (`ClusterHost`), el puerto (`ClusterPort`, 1–65535) y el indicativo de inicio de sesión (`ClusterCallsign`). **Cluster Console** muestra el tráfico telnet sin procesar. Puede escribir comandos del clúster en el campo de línea de comandos y enviarlos con Send. El color del spot se configura mediante **Spot Color:** y se persiste como `ClusterSpotColor`.

**Pestaña RBN** — Se conecta a la Reverse Beacon Network mediante telnet. La configuración es similar a la pestaña Cluster: `RbnHost`, `RbnPort` (1–65535), `RbnCallsign`. El control **Rate Limit:** (`RbnRateLimit`) limita la cantidad de spots aceptados por segundo, lo cual es útil porque el volumen de tráfico de RBN puede ser muy alto. **RBN Console** muestra el tráfico sin procesar. El color del spot se configura mediante **Spot Color:** (`RbnSpotColor`).

**Pestaña WSJT-X** — Escucha datagramas UDP transmitidos por una instancia de WSJT-X en ejecución. Configure la dirección de enlace (`WsjtxAddress`) y el puerto (`WsjtxPort`, 1–65535), luego haga clic en Start. Tres casillas de verificación filtran qué decodificaciones aparecen como spots: **CQ** (`WsjtxFilterCQ`), **CQ POTA** (`WsjtxFilterPOTA`) y **Calling Me** (`WsjtxFilterCallingMe`). Cada categoría tiene su propio selector de color: color CQ (`WsjtxColorCQ`), color POTA (`WsjtxColorPOTA`), color Calling Me (`WsjtxColorCallingMe`) y color Predeterminado (`WsjtxColorDefault`). **Spot Life:** (`WsjtxSpotLife`) controla cuánto tiempo permanecen los spots de WSJT-X en el panadapter. La consola **WSJT-X Decodes** muestra el flujo de decodificaciones sin procesar.

**Pestaña SpotCollector** — Escucha en un puerto UDP las transmisiones de spots de Ham Radio Deluxe SpotCollector. Configure **UDP Port:** (`SpotCollectorPort`, 1–65535) y haga clic en Start. La consola **SpotCollector Spots** muestra los spots recibidos.

**Pestaña POTA** — Consulta `api.pota.app` mediante HTTP en un intervalo configurable (**Poll Interval:**, `PotaPollInterval`). La dirección del servidor es fija y se muestra como un indicador. La consola **POTA Activations** muestra el feed de activaciones. El color del spot se configura mediante **Spot Color:** (`PotaSpotColor`).

**Pestaña FreeDV** — Se conecta al FreeDV QSO Reporter mediante WebSocket en `qso.freedv.org`. La dirección del servidor es fija. La consola **FreeDV Spots** muestra la actividad. El color del spot se configura mediante **Spot Color:** (`FreeDvSpotColor`). Esta pestaña solo está presente en las compilaciones que incluyen soporte para WebSocket.

### Conexión e inicio automáticos

Cada fuente tiene un conmutador **Auto-connect on startup** o **Auto-start on startup**. Cuando está habilitado, esa fuente se conecta o se inicia automáticamente cada vez que se lanza AetherSDR, sin intervención manual. Las claves persistentes son `ClusterAutoConnect`, `RbnAutoConnect`, `WsjtxAutoStart`, `SpotCollectorAutoStart`, `PotaAutoStart` y `FreeDvAutoStart`.

### Pestaña Spot List

La pestaña **Spot List** muestra una tabla unificada y ordenable de todos los spots activos de todas las fuentes activas. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band y Source. Las casillas de verificación por banda debajo de **Bands:** alternan la visibilidad de cada banda de aficionados. Haga clic en **Clear** para vaciar la lista actual. Haga doble clic en cualquier fila para sintonizar el VFO activo a la frecuencia de ese spot y, cuando el spot contenga información de modo (por ejemplo, CW, FT8 o RTTY), cambie automáticamente el slice a ese modo.

### Pestaña Display

La pestaña **Display** controla cómo aparecen los spots en el panadapter.

| Control | Clave de configuración | Predeterminado |
|---|---|---|
| **Spots:** | `IsSpotsEnabled` | Habilitado |
| **Memories:** | `IsMemorySpotsEnabled` | Deshabilitado |
| **Auto:** | `SpotAutoSwitchMode` | Habilitado |
| **Signals (Signal History)** | `SHistoryMarkersEnabled` | Deshabilitado |
| **QRM (Signal History)** | `SHistoryQrmEnabled` | Deshabilitado |
| **Clear All** | — | — |
| **Levels:** | `SpotsMaxLevel` | 3 |
| **Position:** | `SpotsStartingHeightPercentage` | 50 |
| **Font Size:** | `SpotFontSize` | 16 |
| **Spot Lifetime:** | `DxClusterSpotLifetimeSec` | — |
| **Override Colors:** | `IsSpotsOverrideColorsEnabled` | — |
| Selector de color de texto de spot | `SpotsOverrideColor` | #FFFF00 |
| **Override Background: Enabled** | `IsSpotsOverrideBackgroundColorsEnabled` | Habilitado |
| **Override Background: Auto** | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Habilitado |
| Selector de color de fondo de spot | `SpotsOverrideBgColor` | #000000 |
| **Background Opacity:** | `SpotsBackgroundOpacity` | 48 |
| **Spot Lines:** | `IsSpotsLinesEnabled` | Habilitado |
| **Total Spots:** | Lectura en vivo de cuántos spots se rastrean actualmente en todas las fuentes. | Se actualiza cuando se agregan o borran spots. Se restablece a 0 al presionar **Clear All**. |
| **DXCC Coloring (sección)** | Encabezado de sección para los controles de coloración DXCC en la columna izquierda debajo del divisor. | — |
| **DXCC Colors:** | `IsDxccColoringEnabled` | — |
| **Log File (ADIF):** | `DxccAdifFilePath` | — |
| **Imported: (estadísticas DXCC)** | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. | (ningún registro cargado) |
| **Muestras de color DXCC (New DXCC / New Band / New Mode / Worked)** | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` | — |
| **Signal History (sección)** | Encabezado de sección para los parámetros ajustables de Signal History en la columna derecha debajo del divisor. | — |
| **Marker Lifetime:** | `SHistoryLifetimeS` | 60 s |
| **QRM Gate:** | `SHistoryQrmGateS` | 6 s |
| **Edge Threshold:** | `SHistorySoftEdgeDb` | 3.0 dB |
| **Muestras de color Signal History (Signals / QRM)** | `SHistoryColorSignals` / `SHistoryColorQrm` | #FFC800 / #FF0000 |
| **Snap to Step:** | `SHistorySnapToStep` | Deshabilitado |

**Spot Lines:** dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot. Deshabilítelo durante concursos para reducir el desorden visual. La configuración se persiste como `IsSpotsLinesEnabled` y el valor predeterminado es Habilitado.

**Auto:** el valor predeterminado es **Enabled** (`SpotAutoSwitchMode` tiene como valor predeterminado `True`). Si anteriormente confiaba en que el Modo Automático estuviera desactivado por defecto, verifique esta configuración después de actualizar.

### Informes de FreeDV Reporter

La pestaña **FreeDV** incluye una sección **Station Reporting** que permite que AetherSDR transmita la actividad de su estación al mapa público de FreeDV Reporter en `qso.freedv.org` cada vez que el módem RADE está activo. Esta función solo está presente en las compilaciones compiladas con soporte para WebSocket.

#### Habilitar informes

1. Abra la pestaña **FreeDV**.
2. Complete un indicativo y una cuadrícula válidos en los campos **Callsign:** y **Grid Square:** (ver más abajo). La casilla de verificación se niega a habilitarse si alguno de los campos está en blanco o no se puede resolver.
3. Marque **Enable FreeDV Reporter reporting when RADE is active** (`FreeDvAutoReport`). Si el indicativo o la cuadrícula no se pueden resolver, aparece un diálogo de advertencia y la casilla de verificación vuelve a estar desmarcada.

> **Nota:** Los datos del Reporter se publican en un mapa público compartido por la comunidad. No habilite los informes con valores ficticios.

#### Campo Callsign

| Control | Clave de configuración | Predeterminado | Notas |
|---|---|---|---|
| **Callsign:** | `FreeDvMyCallsign` | — | El indicativo enviado al mapa de FreeDV Reporter. El campo es de solo lectura cuando **Use radio** está marcado. |
| **Use radio** | `FreeDvUseRadioCallsign` | True | Rellena previamente el indicativo desde el indicativo configurado en la radio y bloquea el campo como solo lectura. Se actualiza automáticamente si cambia el indicativo en Radio Setup. |

Cuando **Use radio** está marcado, el campo muestra el indicativo de la radio. Desmárquelo para ingresar un indicativo manualmente.

#### Campo Grid Square

| Control | Clave de configuración | Predeterminado | Notas |
|---|---|---|---|
| **Grid Square:** | `FreeDvMyGrid` | — | Cuadrícula Maidenhead enviada al mapa de FreeDV Reporter. El campo es de solo lectura cuando **Use GPS** está marcado. |
| **Use GPS** | `FreeDvUseGpsGrid` | True | Rellena previamente la cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. |

#### Mensaje de estación

| Control | Clave de configuración | Predeterminado | Notas |
|---|---|---|---|
| **Station Msg:** | `FreeDvMyMessage` | — | Texto libre opcional que se muestra junto a su indicativo en el mapa público de FreeDV Reporter. |

## Superposición de barrido SWR

La versión 0.9.4 agrega una superposición de barrido SWR que traza la ROE frente a la frecuencia directamente en el panadapter. Una fuente externa (por ejemplo, una integración de analizador de antena) proporciona los datos llamando a `setSwrSweepPoints()`. El panadapter renderiza la curva a través de la capa interna `drawSwrSweep()`.

### Suministro de datos de barrido

Llame a `setSwrSweepPoints()` con un vector de valores `SwrSweepPoint`. Cada punto lleva dos campos:

| Campo | Tipo | Predeterminado | Descripción |
|---|---|---|---|
| `freqMhz` | `double` | `0.0` | Frecuencia de la medición en MHz. |
| `swr` | `float` | `1.0` | Valor de ROE en esa frecuencia. |

La firma del método es:

```
setSwrSweepPoints(points, running, currentFreqMhz, sourceLabel)
```

| Parámetro | Tipo | Predeterminado | Descripción |
|---|---|---|---|
| `points` | `QVector<SwrSweepPoint>` | — | Los datos de barrido a mostrar. |
| `running` | `bool` | `false` | Pase `true` mientras un barrido está en progreso para indicar una traza en vivo e incompleta. |
| `currentFreqMhz` | `double` | `-1.0` | La frecuencia que se está barriendo actualmente. Pase `-1.0` para suprimir el cursor. |
| `sourceLabel` | `QString` | *(vacío)* | Etiqueta opcional que identifica la fuente de los datos de barrido, que se muestra en la superposición. |

### Borrado de datos de barrido

Llame a `clearSwrSweepPoints()` para eliminar todos los datos de barrido y ocultar la superposición.

## Consejos

- RBN produce una tasa de spots muy alta. Establezca **Rate Limit:** en un valor que su pantalla pueda manejar antes de conectarse, para evitar saturar el panadapter.
- Los spots de WSJT-X son efímeros por naturaleza. Establezca **Spot Life:** para que coincida con la duración del ciclo de transmisión FT8 o FT4 (15 o 7,5 segundos) si desea que los spots se borren entre períodos.
- El filtro **Calling Me** en la pestaña WSJT-X resalta las decodificaciones dirigidas específicamente a su indicativo, lo que facilita ver cuándo una estación está respondiendo a su CQ.
- **Auto:** tiene el valor predeterminado de Habilitado. Cambia automáticamente el modo del slice cuando hace doble clic en un spot que incluye información de modo (por ejemplo, CW, FT8 o RTTY).
- Al hacer doble clic en un spot en la **Spot List** ahora también se reenvía la sugerencia de modo del comentario del spot, por lo que el slice cambia a CW, SSB.
