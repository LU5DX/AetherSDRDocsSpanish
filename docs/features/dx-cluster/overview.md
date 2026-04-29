# Descripción general de SpotHub

SpotHub es el concentrador central de AetherSDR para recibir spots de DX de múltiples fuentes y mostrarlos como superposiciones en el panadapter. Úselo para conectarse a clústeres de DX tradicionales, la Reverse Beacon Network, WSJT-X, SpotCollector, POTA y FreeDV, todo desde un único diálogo.

## Antes de comenzar

- Abra SpotHub mediante `Settings > SpotHub...`. No se requiere conexión a la radio.
- Tenga a mano su indicativo de inicio de sesión si planea conectarse a un clúster de DX o a RBN.
- Tenga disponible un archivo de registro ADIF si desea usar el coloreado por DXCC.

## Cómo funciona

SpotHub agrega spots de hasta seis fuentes independientes. Cada fuente opera de forma independiente: puede habilitar cualquier combinación de ellas simultáneamente. Todos los spots entrantes se fusionan en una lista unificada y se representan como marcadores de frecuencia en el panadapter.

Los spots de cada fuente tienen un código de color distinto para que pueda identificar su origen de un vistazo. Una capa de visualización global (la pestaña **Display**) controla cómo aparecen todos los spots en el panadapter, independientemente de la fuente.

### Fuentes

**Pestaña Cluster** — Se conecta a un clúster de DX mediante una sesión telnet. Debe proporcionar el nombre del host (`ClusterHost`), el puerto (`ClusterPort`, 1–65535) y el indicativo de inicio de sesión (`ClusterCallsign`). El **Cluster Console** muestra el tráfico telnet en bruto. Puede escribir comandos del clúster en el campo de línea de comandos y enviarlos con Send. El color de los spots se define mediante **Spot Color:** y se almacena como `ClusterSpotColor`.

**Pestaña RBN** — Se conecta a la Reverse Beacon Network mediante telnet. La configuración es idéntica a la de la pestaña Cluster: `RbnHost`, `RbnPort` (1–65535), `RbnCallsign`. El control giratorio **Rate Limit:** (`RbnRateLimit`) limita el número de spots aceptados por segundo, lo cual es útil porque el volumen de tráfico de RBN puede ser muy elevado. El **RBN Console** muestra el tráfico en bruto. El color de los spots se define mediante **Spot Color:** (`RbnSpotColor`).

**Pestaña WSJT-X** — Escucha los datagramas UDP transmitidos por una instancia de WSJT-X en ejecución. Configure la dirección de enlace (`WsjtxAddress`) y el puerto (`WsjtxPort`, 1–65535) y, a continuación, haga clic en Start. Tres casillas de verificación filtran qué decodificaciones aparecen como spots: **CQ** (`WsjtxFilterCQ`), **CQ POTA** (`WsjtxFilterPOTA`) y **Calling Me** (`WsjtxFilterCallingMe`). Cada categoría tiene su propio selector de color: color de CQ (`WsjtxColorCQ`), color de POTA (`WsjtxColorPOTA`), color de Calling Me (`WsjtxColorCallingMe`) y color predeterminado (`WsjtxColorDefault`). **Spot Life:** (`WsjtxSpotLife`) controla cuánto tiempo permanecen los spots de WSJT-X en el panadapter. La consola **WSJT-X Decodes** muestra el flujo de decodificaciones en bruto.

**Pestaña SpotCollector** — Escucha en un puerto UDP los spots transmitidos por Ham Radio Deluxe SpotCollector. Configure **UDP Port:** (`SpotCollectorPort`, 1–65535) y haga clic en Start. La consola **SpotCollector Spots** muestra los spots recibidos.

**Pestaña POTA** — Consulta `api.pota.app` mediante HTTP a un intervalo configurable (**Poll Interval:**, `PotaPollInterval`). La dirección del servidor es fija y se muestra como indicador. La consola **POTA Activations** muestra el flujo de activaciones. El color de los spots se define mediante **Spot Color:** (`PotaSpotColor`).

**Pestaña FreeDV** — Se conecta al reportador de QSO de FreeDV mediante WebSocket en `qso.freedv.org`. La dirección del servidor es fija. La consola **FreeDV Spots** muestra la actividad. El color de los spots se define mediante **Spot Color:** (`FreeDvSpotColor`). Esta pestaña solo está presente en compilaciones que incluyen soporte para WebSocket.

### Conexión automática e inicio automático

Cada fuente dispone de un interruptor **Auto-connect on startup** o **Auto-start on startup**. Cuando está habilitado, esa fuente se conecta o se inicia automáticamente cada vez que AetherSDR se lanza, sin intervención manual. Las claves almacenadas son `ClusterAutoConnect`, `RbnAutoConnect`, `WsjtxAutoStart`, `SpotCollectorAutoStart`, `PotaAutoStart` y `FreeDvAutoStart`.

### Pestaña Spot List

La pestaña **Spot List** muestra una tabla unificada y ordenable de todos los spots activos de todas las fuentes activas. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band y Source. Las casillas de verificación por banda bajo **Bands:** permiten activar o desactivar la visibilidad de cada banda de radioaficionados. Haga clic en **Clear** para vaciar la lista actual. Haga doble clic en cualquier fila para sintonizar el VFO activo en la frecuencia de ese spot.

### Pestaña Display

La pestaña **Display** controla cómo aparecen los spots en el panadapter.

| Control | Clave de configuración | Valor predeterminado | Función |
|---|---|---|---|
| **Spots:** | `IsSpotsEnabled` | Habilitado | Interruptor maestro para la superposición de spots. Desactívelo para ocultar todos los spots sin desconectar las fuentes. |
| **Memories:** | `IsMemoriesShownOnPanadapter` | Deshabilitado | Superpone los canales de memoria almacenados en el panadapter junto con los spots. |
| **Auto Mode:** | `SpotsAutoMode` | — | Ajusta automáticamente la densidad de spots según el nivel de zoom actual del panadapter. |
| **Levels:** | `SpotsStackLevels` | — | Número de filas verticales utilizadas cuando los spots en frecuencias cercanas se solaparían. |
| **Position:** | `SpotsPosition` | — | Posición vertical de la superposición de spots en el panadapter. |
| **Font Size:** | `SpotsFontSize` | — | Tamaño del texto de las etiquetas de spots. |
| **Spot Lifetime:** | `SpotsLifetime` | — | Tiempo en segundos que un spot permanece visible antes de desvanecerse. |
| **Override Colors:** | `IsSpotsOverrideColorsEnabled` | — | Fuerza un único color de texto para todas las etiquetas de spots, ignorando los colores por fuente. |
| **Override Background: Enabled** | `IsSpotsOverrideBackgroundColorsEnabled` | — | Habilita un color de fondo personalizado detrás de las etiquetas de spots. |
| **Override Background: Auto** | `IsSpotsOverrideToAutoBackgroundColorEnabled` | — | Selecciona automáticamente un color de contraste para el fondo de los spots. |
| **Background Opacity:** | `SpotsOverrideBgOpacity` | 48 | Opacidad del fondo de los spots. |
| **DXCC Coloring** | `DxccColoringEnabled` | — | Colorea los spots según el estado de la entidad DXCC: trabajada, confirmada o pendiente, derivado de un registro ADIF cargado. |
| **Log File (ADIF):** | `DxccAdifPath` | — | Abre un selector de archivos para cargar un registro ADIF para el coloreado por DXCC. |
| **Auto-Reload Log:** | `DxccAutoReload` | — | Supervisa el archivo ADIF para detectar cambios y lo vuelve a leer automáticamente cuando se actualiza. |
| **Clear All Spots** | — | — | Elimina de inmediato todos los spots rastreados actualmente en todas las fuentes. |

## Consejos

- RBN genera una tasa de spots muy elevada. Configure **Rate Limit:** a un valor que su pantalla pueda manejar antes de conectarse, para evitar saturar el panadapter.
- Los spots de WSJT-X son efímeros por naturaleza. Configure **Spot Life:** para que coincida con la duración del ciclo de transmisión de FT8 o FT4 (15 o 7.5 segundos) si desea que los spots se borren entre períodos.
- El filtro **Calling Me** en la pestaña WSJT-X resalta las decodificaciones dirigidas específicamente a su indicativo, lo que facilita detectar cuándo una estación está respondiendo a su CQ.
- **Auto Mode:** es útil durante concursos o DXpediciones cuando la densidad de spots varía significativamente entre bandas y niveles de zoom.

## Solución de problemas

- **El clúster o RBN se conecta pero no aparecen spots en el panadapter** — Verifique que **Spots:** en la pestaña **Display** esté configurado como Enabled (`IsSpotsEnabled`). Compruebe también que las casillas de verificación de banda correspondientes en la pestaña **Spot List** estén marcadas.
- **No se reciben spots de WSJT-X** — Confirme que WSJT-X está configurado para enviar transmisiones UDP a la misma dirección y puerto que se muestran en la pestaña WSJT-X de AetherSDR, y que el receptor esté iniciado (Start / Stop muestra el estado de ejecución).
- **La pestaña FreeDV no es visible** — Esta pestaña solo está presente en compilaciones compiladas con soporte para WebSocket. Su compilación instalada puede no incluirla.
- **El coloreado por DXCC no funciona** — Asegúrese de que se haya cargado un archivo ADIF mediante **Log File (ADIF):** y que **DXCC Coloring** esté habilitado. El indicador de estadísticas DXCC muestra cuántos QSO fueron importados del archivo.

## Relacionados

- [Conectarse a un clúster de DX](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectarse a la Reverse Beacon Network](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Habilitar el flujo UDP de SpotCollector](enable-spotcollector-udp-feed.md)
- [Consultar activaciones de POTA](poll-pota-activations.md)
- [Habilitar el WebSocket del reportador de QSO de FreeDV](enable-freedv-qso-reporter-websocket.md)
- [Habilitar el coloreado por DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Recargar automáticamente el registro ADIF cuando lo actualiza un logger](auto-reload-adif-log-when-updated-by-a-logger.md)
- [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Seleccionar colores para cada fuente de spots](pick-colors-for-each-spot-source)
