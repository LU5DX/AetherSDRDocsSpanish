# Descripción general de SpotHub

SpotHub es el centro central de AetherSDR para recibir spots de DX de múltiples fuentes y mostrarlos como superposiciones en el panadapter. Úselo para conectarse a clústeres de DX tradicionales, la Reverse Beacon Network, WSJT-X, SpotCollector, POTA y FreeDV, todo desde un único diálogo.

## Antes de comenzar

- Abra SpotHub desde `Settings > SpotHub...`. No se requiere conexión al radio.
- Tenga a mano su indicativo de inicio de sesión si planea conectarse a un clúster de DX o a RBN.
- Tenga disponible un archivo de registro ADIF si desea usar coloración DXCC.

## Cómo funciona

SpotHub agrega spots de hasta seis fuentes independientes. Cada fuente opera de forma independiente; puede habilitar cualquier combinación de manera simultánea. Todos los spots entrantes se fusionan en una lista unificada y se representan como marcadores de frecuencia en el panadapter.

Los spots de cada fuente tienen un código de color distinto para que pueda identificar su origen de un vistazo. Una capa de visualización global (la pestaña **Display**) controla cómo aparecen todos los spots en el panadapter, independientemente de su fuente.

### Fuentes

**Pestaña Cluster** — Se conecta a un clúster de DX mediante una sesión telnet. Proporcione el nombre de host (`ClusterHost`), el puerto (`ClusterPort`, 1–65535) y el indicativo de inicio de sesión (`ClusterCallsign`). La **Cluster Console** muestra el tráfico telnet sin procesar. Puede escribir comandos del clúster en el campo de línea de comandos y enviarlos con Send. El color del spot se establece mediante **Spot Color:**, persistido como `ClusterSpotColor`.

**Pestaña RBN** — Se conecta a la Reverse Beacon Network mediante telnet. La configuración es equivalente a la de la pestaña Cluster: `RbnHost`, `RbnPort` (1–65535), `RbnCallsign`. El control **Rate Limit:** (`RbnRateLimit`) limita la cantidad de spots aceptados por segundo, lo cual es útil porque el volumen de tráfico de RBN puede ser muy alto. La **RBN Console** muestra el tráfico sin procesar. El color del spot se establece mediante **Spot Color:** (`RbnSpotColor`).

**Pestaña WSJT-X** — Escucha datagramas UDP transmitidos por una instancia de WSJT-X en ejecución. Establezca la dirección de enlace (`WsjtxAddress`) y el puerto (`WsjtxPort`, 1–65535), luego haga clic en Start. Tres casillas de verificación filtran qué decodificaciones aparecen como spots: **CQ** (`WsjtxFilterCQ`), **CQ POTA** (`WsjtxFilterPOTA`) y **Calling Me** (`WsjtxFilterCallingMe`). Cada categoría tiene su propio selector de color: color CQ (`WsjtxColorCQ`), color POTA (`WsjtxColorPOTA`), color Calling Me (`WsjtxColorCallingMe`) y color predeterminado (`WsjtxColorDefault`). **Spot Life:** (`WsjtxSpotLife`) controla cuánto tiempo permanecen los spots de WSJT-X en el panadapter. La consola **WSJT-X Decodes** muestra el flujo de decodificaciones sin procesar.

**Pestaña SpotCollector** — Escucha en un puerto UDP los spots transmitidos por Ham Radio Deluxe SpotCollector. Establezca **UDP Port:** (`SpotCollectorPort`, 1–65535) y haga clic en Start. La consola **SpotCollector Spots** muestra los spots recibidos.

**Pestaña POTA** — Consulta `api.pota.app` mediante HTTP a un intervalo configurable (**Poll Interval:**, `PotaPollInterval`). La dirección del servidor es fija y se muestra como indicador. La consola **POTA Activations** muestra el flujo de activaciones. El color del spot se establece mediante **Spot Color:** (`PotaSpotColor`).

**Pestaña FreeDV** — Se conecta al FreeDV QSO Reporter mediante WebSocket en `qso.freedv.org`. La dirección del servidor es fija. La consola **FreeDV Spots** muestra la actividad. El color del spot se establece mediante **Spot Color:** (`FreeDvSpotColor`). Esta pestaña solo está presente en compilaciones que incluyen soporte para WebSocket.

### Conexión automática e inicio automático

Cada fuente dispone de un interruptor **Auto-connect on startup** o **Auto-start on startup**. Cuando está habilitado, esa fuente se conecta o inicia automáticamente cada vez que AetherSDR se lanza, sin intervención manual. Las claves persistidas son `ClusterAutoConnect`, `RbnAutoConnect`, `WsjtxAutoStart`, `SpotCollectorAutoStart`, `PotaAutoStart` y `FreeDvAutoStart`.

### Pestaña Spot List

La pestaña **Spot List** muestra una tabla unificada y ordenable de todos los spots activos de todas las fuentes activas. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band y Source. Las casillas de verificación por banda bajo **Bands:** controlan la visibilidad de cada banda de radioaficionado. Haga clic en **Clear** para vaciar la lista actual. Haga doble clic en cualquier fila para sintonizar el VFO activo a la frecuencia de ese spot.

### Pestaña Display

La pestaña **Display** controla cómo aparecen los spots en el panadapter.

| Control | Clave de configuración | Predeterminado |
|---|---|---|
| **Spots:** | `IsSpotsEnabled` | Habilitado |
| **Memories:** | `IsMemoriesShownOnPanadapter` | Deshabilitado |
| **Auto Mode:** | `SpotsAutoMode` | Habilitado |
| **Levels:** | `SpotsStackLevels` | — |
| **Position:** | `SpotsPosition` | — |
| **Font Size:** | `SpotsFontSize` | — |
| **Spot Lifetime:** | `SpotsLifetime` | — |
| **Override Colors:** | `IsSpotsOverrideColorsEnabled` | — |
| **Override Background: Enabled** | `IsSpotsOverrideBackgroundColorsEnabled` | — |
| **Override Background: Auto** | `IsSpotsOverrideToAutoBackgroundColorEnabled` | — |
| **Background Opacity:** | `SpotsOverrideBgOpacity` | 48 |
| **DXCC Coloring** | `DxccColoringEnabled` | — |
| **Log File (ADIF):** | `DxccAdifPath` | — |
| **Auto-Reload Log:** | `DxccAutoReload` | — |
| **Clear All Spots** | — | — |

**Auto Mode:** está habilitado de forma predeterminada a partir de la v0.9.5.1. La clave de configuración `SpotAutoSwitchMode` ahora tiene el valor predeterminado `True`. Si anteriormente dependía de que Auto Mode estuviera desactivado por defecto, verifique esta configuración después de actualizar.

### Informes al FreeDV Reporter

La pestaña **FreeDV** incluye una sección **Station Reporting** que permite a AetherSDR transmitir la actividad de su estación al mapa público de FreeDV Reporter en `qso.freedv.org` cuando el módem RADE está activo. Esta función solo está presente en compilaciones compiladas con soporte para WebSocket.

#### Habilitar los informes

1. Abra la pestaña **FreeDV**.
2. Ingrese un indicativo válido y un cuadrado de localizador en los campos **Callsign:** y **Grid Square:** (consulte a continuación). La casilla de verificación no se puede habilitar si alguno de los campos está vacío o no puede resolverse.
3. Marque **Enable FreeDV Reporter reporting when RADE is active** (`FreeDvAutoReport`). Si el indicativo o el localizador no pueden resolverse, aparece un diálogo de advertencia y la casilla vuelve a estar desmarcada.

> **Nota:** Los datos del Reporter se publican en un mapa público compartido por la comunidad. No habilite los informes con valores de marcador de posición.

#### Campo Callsign

| Control | Clave de configuración | Predeterminado | Notas |
|---|---|---|---|
| **Callsign:** | `FreeDvMyCallsign` | — | El indicativo enviado al mapa de FreeDV Reporter. El campo es de solo lectura cuando **Use radio** está marcado. |
| **Use radio** | `FreeDvUseRadioCallsign` | True | Rellena previamente el indicativo desde el indicativo configurado en el radio y bloquea el campo como solo lectura. Se actualiza automáticamente si cambia el indicativo en Radio Setup. |

Cuando **Use radio** está marcado, el campo muestra el indicativo del radio. Desmárquelo para ingresar un indicativo manualmente.

#### Campo Grid Square

| Control | Clave de configuración | Predeterminado | Notas |
|---|---|---|---|
| **Grid Square:** | `FreeDvMyGrid` | — | Cuadrado de localizador Maidenhead enviado al mapa de FreeDV Reporter. El campo es de solo lectura cuando **Use GPS** está marcado. |
| **Use GPS** | `FreeDvUseGpsGrid` | True | Rellena previamente el localizador desde el módulo GPS del radio y bloquea el campo como solo lectura. Solo aparece en modelos de radio que tienen hardware GPS. |

#### Mensaje de estación

| Control | Clave de configuración | Predeterminado | Notas |
|---|---|---|---|
| **Station Msg:** | `FreeDvMyMessage` | — | Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público de FreeDV Reporter. |

## Superposición de barrido de ROS

La v0.9.4 agrega una superposición de barrido de ROS (SWR) que traza el ROS frente a la frecuencia directamente en el panadapter. Una fuente externa (por ejemplo, la integración de un analizador de antena) suministra los datos llamando a `setSwrSweepPoints()`. El panadapter representa la curva mediante la capa interna `drawSwrSweep()`.

### Suministro de datos de barrido

Llame a `setSwrSweepPoints()` con un vector de valores `SwrSweepPoint`. Cada punto contiene dos campos:

| Campo | Tipo | Predeterminado | Descripción |
|---|---|---|---|
| `freqMhz` | `double` | `0.0` | Frecuencia de la medición en MHz. |
| `swr` | `float` | `1.0` | Valor de ROS en esa frecuencia. |

La firma del método es:

```
setSwrSweepPoints(points, running, currentFreqMhz, sourceLabel)
```

| Parámetro | Tipo | Predeterminado | Descripción |
|---|---|---|---|
| `points` | `QVector<SwrSweepPoint>` | — | Los datos de barrido a mostrar. |
| `running` | `bool` | `false` | Pase `true` mientras el barrido está en curso para indicar una traza activa e incompleta. |
| `currentFreqMhz` | `double` | `-1.0` | La frecuencia que se está barriendo actualmente. Pase `-1.0` para suprimir el cursor. |
| `sourceLabel` | `QString` | *(vacío)* | Etiqueta opcional que identifica la fuente de los datos de barrido, mostrada en la superposición. |

### Borrar datos de barrido

Llame a `clearSwrSweepPoints()` para eliminar todos los datos de barrido y ocultar la superposición.

## Consejos

- RBN produce una tasa de spots muy alta. Establezca **Rate Limit:** en un valor que su pantalla pueda gestionar antes de conectarse, para evitar saturar el panadapter.
- Los spots de WSJT-X son efímeros por naturaleza. Establezca **Spot Life:** para que coincida con la duración del ciclo de transmisión FT8 o FT4 (15 o 7.5 segundos) si desea que los spots se borren entre períodos.
- El filtro **Calling Me** en la pestaña WSJT-X resalta las decodificaciones dirigidas específicamente a su indicativo, lo que facilita ver cuándo una estación responde a su CQ.
- **Auto Mode:** está habilitado de forma predeterminada en la v0.9.5.1. Ajusta automáticamente la densidad de spots a medida que acerca o aleja el zoom del panadapter, lo cual es útil durante concursos o DXpediciones cuando la densidad de spots varía significativamente entre bandas y niveles de zoom.
- Antes de habilitar **Enable FreeDV Reporter reporting when RADE is active**, confirme que su indicativo y cuadrado de localizador estén correctamente configurados. La casilla de verificación no se habilitará si alguno de los valores está en blanco.
- Llame a `clearSwrSweepPoints()` después de que finalice un barrido si no desea que la traza terminada persista en el panadapter.

## Solución de problemas

- **El clúster o RBN se conecta pero no aparecen spots en el panadapter** — Verifique que **Spots:** en la pestaña **Display** esté establecido en Enabled (`IsSpotsEnabled`). Compruebe también que las casillas de verificación de banda correspondientes en la pestaña **Spot List** estén marcadas.
- **No se reciben spots de WSJT-X** — Confirme que WSJT-X esté configurado para enviar transmisiones UDP a la misma dirección y puerto que se muestran en la pestaña WSJT-X de AetherSDR, y que el receptor esté iniciado (Start / Stop muestra el estado en ejecución).
- **La pestaña FreeDV no es visible** — Esta pestaña solo está presente en compilaciones compiladas con soporte para WebSocket. Es posible que su compilación instalada no la incluya.
- **La casilla de verificación de FreeDV Reporter no permanece habilitada** — Tanto el indicativo como el cuadrado de localizador deben poder resolverse para que la casilla pueda permanecer marcada. Verifique el campo **Call**
