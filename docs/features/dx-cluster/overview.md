# Descripción general de SpotHub

SpotHub es el concentrador central de AetherSDR para recibir spots de DX de múltiples fuentes y mostrarlos como superposiciones en el panadapter. Úselo para conectarse a clústeres de DX tradicionales, la Reverse Beacon Network, WSJT-X, SpotCollector, POTA y FreeDV, todo desde un solo cuadro de diálogo.

## Antes de comenzar

- Abra SpotHub mediante `Settings > SpotHub...`. No se requiere conexión a una radio.
- Tenga listo su indicativo de inicio de sesión si planea conectarse a un clúster de DX o a RBN.
- Tenga disponible un archivo de registro ADIF si desea usar el coloreado por DXCC.

## Cómo funciona

SpotHub agrega spots de hasta seis fuentes independientes. Cada fuente opera de manera independiente: puede habilitar cualquier combinación de ellas simultáneamente. Todos los spots entrantes se combinan en una lista unificada y se representan como marcadores de frecuencia en el panadapter.

Los spots de cada fuente reciben un código de color independiente para que pueda distinguir su origen de un vistazo. Una capa de visualización global (la pestaña **Display**) controla cómo aparecen todos los spots en el panadapter, independientemente de su fuente.

### Fuentes

**Pestaña Cluster** — Se conecta a un clúster de DX mediante una sesión telnet. Usted proporciona el nombre de host (`ClusterHost`), el puerto (`ClusterPort`, 1–65535) y el indicativo de inicio de sesión (`ClusterCallsign`). La **Cluster Console** muestra el tráfico telnet sin procesar. Puede escribir comandos del clúster en el campo de línea de comandos y enviarlos con Send. El color de los spots se establece mediante **Spot Color:**, almacenado como `ClusterSpotColor`.

**Pestaña RBN** — Se conecta a la Reverse Beacon Network mediante telnet. La configuración es idéntica a la de la pestaña Cluster: `RbnHost`, `RbnPort` (1–65535), `RbnCallsign`. El cuadro de giro **Rate Limit:** (`RbnRateLimit`) limita la cantidad de spots aceptados por segundo, lo cual resulta útil porque el volumen de tráfico de RBN puede ser muy alto. La **RBN Console** muestra el tráfico sin procesar. El color de los spots se establece mediante **Spot Color:** (`RbnSpotColor`).

**Pestaña WSJT-X** — Escucha los datagramas UDP transmitidos por una instancia de WSJT-X en ejecución. Establezca la dirección de enlace (`WsjtxAddress`) y el puerto (`WsjtxPort`, 1–65535), luego haga clic en Start. Tres casillas de verificación filtran qué decodificaciones aparecen como spots: **CQ** (`WsjtxFilterCQ`), **CQ POTA** (`WsjtxFilterPOTA`) y **Calling Me** (`WsjtxFilterCallingMe`). Cada categoría tiene su propio selector de color: color de CQ (`WsjtxColorCQ`), color de POTA (`WsjtxColorPOTA`), color de Calling Me (`WsjtxColorCallingMe`) y color predeterminado (`WsjtxColorDefault`). **Spot Life:** (`WsjtxSpotLife`) controla cuánto tiempo permanecen los spots de WSJT-X en el panadapter. La consola **WSJT-X Decodes** muestra el flujo de decodificación sin procesar.

**Pestaña SpotCollector** — Escucha en un puerto UDP los spots transmitidos por SpotCollector de Ham Radio Deluxe. Establezca **UDP Port:** (`SpotCollectorPort`, 1–65535) y haga clic en Start. La consola **SpotCollector Spots** muestra los spots recibidos.

**Pestaña POTA** — Consulta `api.pota.app` mediante HTTP a un intervalo configurable (**Poll Interval:**, `PotaPollInterval`). La dirección del servidor es fija y se muestra como indicador. La consola **POTA Activations** muestra el flujo de activaciones. El color de los spots se establece mediante **Spot Color:** (`PotaSpotColor`).

**Pestaña FreeDV** — Se conecta al reportero de QSO de FreeDV mediante WebSocket en `qso.freedv.org`. La dirección del servidor es fija. La consola **FreeDV Spots** muestra la actividad. El color de los spots se establece mediante **Spot Color:** (`FreeDvSpotColor`). Esta pestaña solo está presente en compilaciones que incluyen soporte para WebSocket.

### Conexión automática e inicio automático

Cada fuente tiene un interruptor **Auto-connect on startup** o **Auto-start on startup**. Cuando está habilitado, esa fuente se conecta o inicia automáticamente cada vez que AetherSDR se lanza, sin intervención manual. Las claves almacenadas son `ClusterAutoConnect`, `RbnAutoConnect`, `WsjtxAutoStart`, `SpotCollectorAutoStart`, `PotaAutoStart` y `FreeDvAutoStart`.

### Pestaña Spot List

La pestaña **Spot List** muestra una tabla unificada y ordenable de todos los spots activos de todas las fuentes activas. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band y Source. Las casillas de verificación por banda bajo **Bands:** alternan la visibilidad para cada banda de radioaficionado. Haga clic en **Clear** para vaciar la lista actual. Haga doble clic en cualquier fila para sintonizar el VFO activo a la frecuencia de ese spot.

### Pestaña Display

La pestaña **Display** controla cómo aparecen los spots en el panadapter.

| Control | Clave de configuración | Valor predeterminado | Qué hace |
|---|---|---|---|
| **Spots:** | `IsSpotsEnabled` | Habilitado | Interruptor principal de la superposición de spots. Deshabilítelo para ocultar todos los spots sin desconectar las fuentes. |
| **Memories:** | `IsMemoriesShownOnPanadapter` | Deshabilitado | Superpone los canales de memoria almacenados en el panadapter junto con los spots. |
| **Auto Mode:** | `SpotsAutoMode` | — | Ajusta automáticamente la densidad de spots según el nivel de zoom actual del panadapter. |
| **Levels:** | `SpotsStackLevels` | — | Número de filas verticales usadas cuando los spots en frecuencias cercanas se superpondrían. |
| **Position:** | `SpotsPosition` | — | Ubicación vertical de la superposición de spots en el panadapter. |
| **Font Size:** | `SpotsFontSize` | — | Tamaño de texto de las etiquetas de spots. |
| **Spot Lifetime:** | `SpotsLifetime` | — | Cuánto tiempo permanece visible un spot antes de desvanecerse, en segundos. |
| **Override Colors:** | `IsSpotsOverrideColorsEnabled` | — | Fuerza todas las etiquetas de spots a un único color de texto, ignorando los colores por fuente. |
| **Override Background: Enabled** | `IsSpotsOverrideBackgroundColorsEnabled` | — | Habilita un color de fondo personalizado detrás de las etiquetas de spots. |
| **Override Background: Auto** | `IsSpotsOverrideToAutoBackgroundColorEnabled` | — | Selecciona un color de contraste automático para los fondos de los spots. |
| **Background Opacity:** | `SpotsOverrideBgOpacity` | 48 | Opacidad del fondo de los spots. |
| **DXCC Coloring** | `DxccColoringEnabled` | — | Colorea los spots según el estado de la entidad DXCC: trabajada, confirmada o necesaria, derivado de un registro ADIF cargado. |
| **Log File (ADIF):** | `DxccAdifPath` | — | Abre un selector de archivos para cargar un registro ADIF para el coloreado por DXCC. |
| **Auto-Reload Log:** | `DxccAutoReload` | — | Monitorea el archivo ADIF en busca de cambios y lo vuelve a leer automáticamente cuando se actualiza. |
| **Clear All Spots** | — | — | Elimina inmediatamente todos los spots rastreados actualmente en todas las fuentes. |

## Consejos

- RBN produce una tasa de spots muy alta. Establezca **Rate Limit:** en un valor que su pantalla pueda manejar antes de conectarse, para evitar saturar el panadapter.
- Los spots de WSJT-X son efímeros por naturaleza. Establezca **Spot Life:** para que coincida con la duración del ciclo de transmisión FT8 o FT4 (15 o 7,5 segundos) si desea que los spots se borren entre períodos.
- El filtro **Calling Me** en la pestaña WSJT-X resalta las decodificaciones dirigidas específicamente a su indicativo, lo que facilita identificar cuándo una estación está respondiendo a su CQ.
- **Auto Mode:** es útil durante concursos o DXpediciones cuando la densidad de spots varía significativamente entre bandas y niveles de zoom.

## Solución de problemas

- **El clúster o RBN se conecta pero no aparecen spots en el panadapter** — Verifique que **Spots:** en la pestaña **Display** esté establecido en Enabled (`IsSpotsEnabled`). También compruebe que las casillas de verificación de banda correspondientes en la pestaña **Spot List** estén marcadas.
- **No se reciben spots de WSJT-X** — Confirme que WSJT-X esté configurado para enviar transmisiones UDP a la misma dirección y puerto que se muestran en la pestaña WSJT-X de AetherSDR, y que el receptor esté iniciado (Start / Stop muestra el estado de ejecución).
- **La pestaña FreeDV no es visible** — Esta pestaña solo está presente en compilaciones compiladas con soporte para WebSocket. Es posible que su compilación instalada no lo incluya.
- **El coloreado por DXCC no funciona** — Asegúrese de que se haya cargado un archivo ADIF mediante **Log File (ADIF):** y que **DXCC Coloring** esté habilitado. El indicador de estadísticas DXCC muestra cuántos QSO se importaron del archivo.

## Temas relacionados

- [Conectarse a un clúster de DX](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectarse a la Reverse Beacon Network](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Habilitar el flujo UDP de SpotCollector](enable-spotcollector-udp-feed.md)
- [Consultar activaciones de POTA](poll-pota-activations.md)
- [Habilitar el WebSocket del reportero de QSO de FreeDV](enable-freedv-qso-reporter-websocket.md)
- [Habilitar el coloreado por DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Recargar automáticamente el registro ADIF cuando lo actualiza un programa de registro](auto-reload-adif-log-when-updated-by-a-logger.md)
- [Ajustar la densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source
