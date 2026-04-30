# Resumen de SpotHub

SpotHub es el centro principal de AetherSDR para recibir puntos DX de múltiples fuentes y mostrarlos como superposiciones en el panadapter. Úselo para conectarse a clusters DX tradicionales, la Red de Balizas Invertida, WSJT-X, SpotCollector, POTA y FreeDV, todo desde un solo diálogo.

## Antes de comenzar

- Abra SpotHub mediante `Settings > SpotHub...`. No se requiere conexión de radio.
- Tenga su indicativo de entrada listo si planea conectarse a un cluster DX o RBN.
- Tenga disponible un archivo de registro ADIF si desea coloración DXCC.

## Cómo funciona

SpotHub agrega puntos de hasta seis fuentes independientes. Cada fuente funciona de forma independiente: puede habilitar cualquier combinación simultáneamente. Todos los puntos entrantes se fusionan en una lista unificada y se renderizan como marcadores de frecuencia en el panadapter.

Los puntos de cada fuente tienen código de color separado para que pueda distinguir su origen de un vistazo. Una capa de visualización global (la pestaña **Display**) controla cómo aparecen todos los puntos en el panadapter, independientemente de la fuente.

### Fuentes

**Pestaña Cluster** — Se conecta a un cluster DX mediante una sesión telnet. Proporcione el nombre de host (`ClusterHost`), puerto (`ClusterPort`, 1–65535) e indicativo de entrada (`ClusterCallsign`). La **Cluster Console** muestra el tráfico telnet sin procesar. Puede escribir comandos de cluster en el campo de línea de comando y enviarlos con Send. El color del punto se establece mediante **Spot Color:**, persistido como `ClusterSpotColor`.

**Pestaña RBN** — Se conecta a la Red de Balizas Invertida mediante telnet. La configuración es similar a la pestaña Cluster: `RbnHost`, `RbnPort` (1–65535), `RbnCallsign`. El cuadro de rotación **Rate Limit:** (`RbnRateLimit`) limita el número de puntos aceptados por segundo, lo que es útil porque el volumen de tráfico de RBN puede ser muy alto. La **RBN Console** muestra el tráfico sin procesar. El color del punto se establece mediante **Spot Color:** (`RbnSpotColor`).

**Pestaña WSJT-X** — Escucha datagramas UDP emitidos por una instancia de WSJT-X en ejecución. Establezca la dirección de enlace (`WsjtxAddress`) y puerto (`WsjtxPort`, 1–65535), luego haga clic en Start. Tres casillas de verificación filtran qué decodificaciones aparecen como puntos: **CQ** (`WsjtxFilterCQ`), **CQ POTA** (`WsjtxFilterPOTA`) y **Calling Me** (`WsjtxFilterCallingMe`). Cada categoría tiene su propio selector de color: color CQ (`WsjtxColorCQ`), color POTA (`WsjtxColorPOTA`), color Calling Me (`WsjtxColorCallingMe`) y color predeterminado (`WsjtxColorDefault`). **Spot Life:** (`WsjtxSpotLife`) controla cuánto tiempo permanecen los puntos WSJT-X en el panadapter. La consola **WSJT-X Decodes** muestra el flujo de decodificación sin procesar.

**Pestaña SpotCollector** — Escucha en un puerto UDP las emisiones de puntos desde Ham Radio Deluxe SpotCollector. Establezca **UDP Port:** (`SpotCollectorPort`, 1–65535) y haga clic en Start. La consola **SpotCollector Spots** muestra los puntos recibidos.

**Pestaña POTA** — Consulta `api.pota.app` por HTTP a intervalos configurables (**Poll Interval:**, `PotaPollInterval`). La dirección del servidor es fija y se muestra como un indicador. La consola **POTA Activations** muestra el feed de activación. El color del punto se establece mediante **Spot Color:** (`PotaSpotColor`).

**Pestaña FreeDV** — Se conecta al Reportero QSO de FreeDV mediante WebSocket en `qso.freedv.org`. La dirección del servidor es fija. La consola **FreeDV Spots** muestra la actividad. El color del punto se establece mediante **Spot Color:** (`FreeDvSpotColor`). Esta pestaña solo está presente en compilaciones que incluyen soporte WebSocket.

### Conexión automática e inicio automático

Cada fuente tiene un conmutador **Auto-connect on startup** o **Auto-start on startup**. Cuando está habilitado, esa fuente se conecta o inicia automáticamente cada vez que se lanza AetherSDR, sin intervención manual. Las claves persistidas son `ClusterAutoConnect`, `RbnAutoConnect`, `WsjtxAutoStart`, `SpotCollectorAutoStart`, `PotaAutoStart` y `FreeDvAutoStart`.

### Pestaña Spot List

La pestaña **Spot List** muestra una tabla unificada y ordenable de todos los puntos activos de todas las fuentes activas. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band y Source. Las casillas de verificación por banda bajo **Bands:** alternan la visibilidad de cada banda de radio aficionada. Haga clic en **Clear** para vaciar la lista actual. Haga doble clic en cualquier fila para sintonizar el VFO activo a la frecuencia de ese punto.

### Pestaña Display

La pestaña **Display** controla cómo aparecen los puntos en el panadapter.

| Control | Clave de configuración | Predeterminado |
|---|---|---|
| **Spots:** | `IsSpotsEnabled` | Habilitado |
| **Memories:** | `IsMemoriesShownOnPanadapter` | Deshabilitado |
| **Auto Mode:** | `SpotsAutoMode` | — |
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

### Informes del Reportero de FreeDV

La pestaña **FreeDV** incluye una sección **Station Reporting** que permite que AetherSDR emita la actividad de su estación al mapa público del Reportero de FreeDV en `qso.freedv.org` cada vez que el módem RADE está activo. Esta función solo está presente en compilaciones compiladas con soporte WebSocket.

#### Habilitar informes

1. Abra la pestaña **FreeDV**.
2. Rellene un indicativo válido y localizador en los campos **Callsign:** y **Grid Square:** (véase a continuación). La casilla de verificación se niega a habilitarse si alguno de los campos está en blanco o no se puede resolver.
3. Marque **Enable FreeDV Reporter reporting when RADE is active** (`FreeDvAutoReport`). Si el indicativo o la cuadrícula no se pueden resolver, aparece un diálogo de advertencia y la casilla de verificación vuelve a no marcarse.

> **Nota:** Los datos del reportero se publican en un mapa público compartido por la comunidad. No habilite informes con valores de marcador de posición.

#### Campo de indicativo

| Control | Clave de configuración | Predeterminado | Notas |
|---|---|---|---|
| **Callsign:** | `FreeDvMyCallsign` | — | El indicativo enviado al mapa del Reportero de FreeDV. El campo es de solo lectura cuando se marca **Use radio**. |
| **Use radio** | `FreeDvUseRadioCallsign` | Verdadero | Rellena previamente el indicativo del indicativo configurado de la radio y bloquea el campo como de solo lectura. Se actualiza automáticamente si cambia el indicativo en Radio Setup. |

Cuando **Use radio** está marcado, el campo muestra el indicativo de la radio. Desmarquélo para introducir un indicativo manualmente.

#### Campo de localizador

| Control | Clave de configuración | Predeterminado | Notas |
|---|---|---|---|
| **Grid Square:** | `FreeDvMyGrid` | — | Localizador de cuadrícula Maidenhead enviado al mapa del Reportero de FreeDV. El campo es de solo lectura cuando se marca **Use GPS**. |
| **Use GPS** | `FreeDvUseGpsGrid` | Verdadero | Rellena previamente la cuadrícula desde el módulo GPS de la radio y bloquea el campo como de solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. |

#### Mensaje de estación

| Control | Clave de configuración | Predeterminado | Notas |
|---|---|---|---|
| **Station Msg:** | `FreeDvMyMessage` | — | Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público del Reportero de FreeDV. |

## Consejos

- RBN produce una tasa de puntos muy alta. Establezca **Rate Limit:** a un valor que su pantalla pueda manejar antes de conectarse, para evitar saturar el panadapter.
- Los puntos WSJT-X son efímeros por naturaleza. Establezca **Spot Life:** para que coincida con la duración del ciclo de transmisión FT8 o FT4 (15 o 7,5 segundos) si desea que los puntos se eliminen entre períodos.
- El filtro **Calling Me** en la pestaña WSJT-X destaca decodificaciones específicamente dirigidas a su indicativo, lo que facilita ver cuándo una estación está respondiendo a su CQ.
- **Auto Mode:** es útil durante concursos o expediciones DX cuando la densidad de puntos varía significativamente entre bandas y niveles de zoom.
- Antes de habilitar **Enable FreeDV Reporter reporting when RADE is active**, confirme que su indicativo y localizador estén configurados correctamente. La casilla de verificación no se habilitará si alguno de los valores está en blanco.

## Solución de problemas

- **El cluster o RBN se conecta pero no aparecen puntos en el panadapter** — Compruebe que **Spots:** en la pestaña **Display** esté establecido en Enabled (`IsSpotsEnabled`). También verifique que las casillas de verificación de banda relevantes en la pestaña **Spot List** estén marcadas.
- **Los puntos WSJT-X no se reciben** — Confirme que WSJT-X esté configurado para enviar emisiones UDP a la misma dirección y puerto que se muestran en la pestaña WSJT-X de AetherSDR, y que el oyente esté iniciado (Start / Stop muestra el estado de ejecución).
- **La pestaña FreeDV no es visible** — Esta pestaña solo está presente en compilaciones compiladas con soporte WebSocket. Su compilación instalada puede no incluirla.
- **La casilla de verificación del Reportero de FreeDV no permanece habilitada** — Tanto un indicativo como un localizador deben ser resolubles antes de que se pueda activar la casilla de verificación. Si **Use radio** está marcado pero la radio no tiene un indicativo configurado, o **Use GPS** está marcado pero GPS no tiene una posición, introduzca valores manualmente después de desmarcar esas opciones.
- **La coloración DXCC no funciona** — Asegúrese de que se ha cargado un archivo ADIF mediante **Log File (ADIF):** y que **DXCC Coloring** esté habilitado. El indicador de estadísticas DXCC muestra cuántos QSO se importaron desde el archivo.

## Relacionado

- [Conectarse a un cluster DX](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectarse a la Red de Balizas Invertida](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
- [Iniciar oyente UDP WSJT-X y filtrar CQ, POTA o llamadas para mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Habilitar feed UDP de SpotCollector](enable-spotcollector-udp-feed.md)
- [Consultar activaciones POTA](poll-pota-activations.md)
- [Habilitar WebSocket del reportero QSO de FreeDV](enable-freedv-qso-reporter-websocket.md)
- [Habilitar coloración DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Recargar automáticamente el registro ADIF cuando se actualiza mediante un registrador](auto-reload-adif-log-when-updated-by-a-logger.md)
- [Ajustar densidad de puntos, posición, tamaño de fuente y duración](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un punto haciendo doble clic en la lista de puntos](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Seleccionar colores para cada fuente de puntos](pick-colors-for-each-spot-source)
