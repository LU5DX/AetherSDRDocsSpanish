# Descripción general de SpotHub

SpotHub es el concentrador central de AetherSDR para recibir spots de DX desde múltiples fuentes y mostrarlos como superposiciones en el panadapter. Úselo para conectarse a un cluster de DX, la Reverse Beacon Network, WSJT-X, SpotCollector, POTA o FreeDV, y para controlar el aspecto y el comportamiento de los spots en pantalla.

## Antes de comenzar

- AetherSDR no necesita estar conectado a un radio para configurar SpotHub, pero las superposiciones de spots en el panadapter solo aparecen cuando hay un radio conectado.
- La pestaña FreeDV solo está presente en versiones que incluyen soporte para WebSocket.

## Cómo funciona

Abra SpotHub desde `Settings > SpotHub...`. El cuadro de diálogo contiene ocho pestañas: **Cluster**, **RBN**, **WSJT-X**, **SpotCollector**, **POTA**, **FreeDV**, **Spot List** y **Display**.

Cada pestaña de fuente gestiona de forma independiente una entrada de spots. Los spots de todas las fuentes activas fluyen hacia un único conjunto unificado, visible en la pestaña **Spot List** y representados como superposiciones en el panadapter según la configuración de la pestaña **Display**.

### Pestaña Cluster

Se conecta a un cluster de DX mediante telnet. La **Cluster Console** muestra el tráfico telnet sin procesar. Puede escribir comandos en la línea de comandos y hacer clic en **Send** para enviarlos.

| Control | Ajuste persistente | Notas |
|---|---|---|
| `Server:` | `ClusterHost` | Nombre de host del cluster de DX. |
| `Port:` | `ClusterPort` | Puerto telnet; rango válido 1–65535. |
| `Callsign:` | `ClusterCallsign` | Indicativo de inicio de sesión enviado al conectar. |
| `Connect` / `Disconnect` | — | Activa o desactiva la conexión telnet. |
| `Auto-connect on startup` | `ClusterAutoConnect` | Se reconecta automáticamente al iniciar. |
| `Spot Color:` | `ClusterSpotColor` | Selector de color para las etiquetas de spots del cluster. |

### Pestaña RBN

Se conecta a la Reverse Beacon Network mediante telnet. Incluye un limitador de velocidad para reducir la acumulación de spots de balizas en el panadapter.

| Control | Ajuste persistente | Notas |
|---|---|---|
| `Server:` | `RbnHost` | Nombre de host telnet de RBN. |
| `Port:` | `RbnPort` | Puerto telnet; rango válido 1–65535. |
| `Callsign:` | `RbnCallsign` | Indicativo de inicio de sesión enviado a RBN. |
| `Rate Limit:` | `RbnRateLimit` | Limita el número de spots de RBN por segundo. |
| `Connect` / `Disconnect` | — | Activa o desactiva la conexión a RBN. |
| `Auto-connect on startup` | `RbnAutoConnect` | Se reconecta automáticamente al iniciar. |
| `Spot Color:` | `RbnSpotColor` | Selector de color para las etiquetas de spots de RBN. |

### Pestaña WSJT-X

Escucha en un puerto UDP las transmisiones decodificadas de una instancia de WSJT-X en ejecución. Los filtros permiten reducir la visualización a solo los decodificados que sean relevantes.

| Control | Ajuste persistente | Notas |
|---|---|---|
| `Address:` | `WsjtxAddress` | Dirección de enlace UDP. |
| `Port:` | `WsjtxPort` | Puerto UDP; rango válido 1–65535. |
| `Start` / `Stop` | — | Inicia o detiene el receptor UDP. |
| `Auto-start on startup` | `WsjtxAutoStart` | Inicia el receptor automáticamente al arrancar. |
| `CQ` | `WsjtxFilterCQ` | Muestra solo llamadas CQ. |
| `CQ POTA` | `WsjtxFilterPOTA` | Muestra llamadas CQ POTA. |
| `Calling Me` | `WsjtxFilterCallingMe` | Muestra solo decodificados dirigidos a su indicativo. |
| Selectores de color CQ / POTA / Calling Me / Default | `WsjtxColorCQ` / `WsjtxColorPOTA` / `WsjtxColorCallingMe` / `WsjtxColorDefault` | Colores de spots por categoría. |
| `Spot Life:` | `WsjtxSpotLife` | Segundos que los spots de WSJT-X permanecen en el panadapter. |

### Pestaña SpotCollector

Escucha en un puerto UDP las difusiones de spots de Ham Radio Deluxe SpotCollector.

| Control | Ajuste persistente | Notas |
|---|---|---|
| `UDP Port:` | `SpotCollectorPort` | Rango válido 1–65535. |
| `Start` / `Stop` | — | Inicia o detiene el receptor UDP. |
| `Auto-start on startup` | `SpotCollectorAutoStart` | Inicia el receptor automáticamente al arrancar. |

### Pestaña POTA

Consulta `api.pota.app` mediante HTTP a un intervalo configurable para obtener las activaciones actuales de Parks on the Air.

| Control | Ajuste persistente | Notas |
|---|---|---|
| `Poll Interval:` | `PotaPollInterval` | Segundos entre consultas a la API de POTA. |
| `Start` / `Stop` | — | Inicia o detiene las consultas. |
| `Auto-start on startup` | `PotaAutoStart` | Inicia las consultas automáticamente al arrancar. |
| `Spot Color:` | `PotaSpotColor` | Selector de color para las etiquetas de spots de POTA. |

### Pestaña FreeDV

Se conecta al reportador de QSO de FreeDV en `qso.freedv.org` mediante WebSocket. Esta pestaña solo está presente en versiones con soporte para WebSocket.

| Control | Ajuste persistente | Notas |
|---|---|---|
| `Start` / `Stop` | — | Conecta o desconecta la fuente WebSocket. |
| `Auto-start on startup` | `FreeDvAutoStart` | Se conecta automáticamente al arrancar. |
| `Spot Color:` | `FreeDvSpotColor` | Selector de color para las etiquetas de spots de FreeDV. |

### Pestaña Spot List

Muestra una tabla unificada y ordenable de todos los spots activos de cada fuente activa. Las columnas son Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band y Source. Al hacer doble clic en una fila, el VFO activo se sintoniza a la frecuencia de ese spot.

Las casillas de verificación por banda en la parte superior de la pestaña alternan la visibilidad de los spots según la banda (de 160m a 2m). Haga clic en **Clear** para vaciar la lista de spots actual sin desconectar ninguna fuente.

### Pestaña Display

Controla cómo se representan los spots en el panadapter y si el estado de premio DXCC afecta a su color.

| Control | Ajuste persistente | Valor predeterminado | Notas |
|---|---|---|---|
| `Spots:` | `IsSpotsEnabled` | Habilitado | Interruptor principal de la superposición de spots. Desactívelo para ocultar todos los spots sin desconectar las fuentes. |
| `Memories:` | `IsMemoriesShownOnPanadapter` | Deshabilitado | Activa o desactiva los marcadores de canales de memoria en el panadapter. |
| `Auto Mode:` | `SpotsAutoMode` | — | Ajusta automáticamente la densidad de spots según el nivel de zoom del panadapter. |
| `Levels:` | `SpotsStackLevels` | — | Número de filas de apilamiento vertical usadas cuando los spots se superponen. |
| `Position:` | `SpotsPosition` | — | Posición vertical de las etiquetas de spots en el panadapter. |
| `Font Size:` | `SpotsFontSize` | — | Tamaño del texto de las etiquetas de spots. |
| `Spot Lifetime:` | `SpotsLifetime` | — | Segundos antes de que una etiqueta de spot desaparezca. |
| `Override Colors:` | `IsSpotsOverrideColorsEnabled` | — | Fuerza un único color de texto para todos los spots, ignorando los colores por fuente. |
| `Override Background:` Enabled / Auto | `IsSpotsOverrideBackgroundColorsEnabled` / `IsSpotsOverrideToAutoBackgroundColorEnabled` | — | Habilita un color de fondo personalizado para los spots; Auto selecciona automáticamente un fondo con contraste adecuado. |
| `Background Opacity:` | `SpotsOverrideBgOpacity` | 48 | Opacidad del relleno de fondo de los spots. |
| `DXCC Coloring` | `DxccColoringEnabled` | — | Colorea los spots según el estado DXCC: trabajado, confirmado o necesario. |
| `Log File (ADIF):` | `DxccAdifPath` | — | Ruta a un archivo de registro ADIF utilizado para determinar el estado DXCC. |
| `Auto-Reload Log:` | `DxccAutoReload` | — | Vuelve a leer el archivo ADIF automáticamente cuando una aplicación de registro lo actualiza. |
| `Clear All Spots` | — | — | Elimina todos los spots rastreados actualmente en todas las fuentes. |

## Consejos

- Cada pestaña de fuente muestra un indicador de estado: **Connected**, **Disconnected**, **Listening**, **Polling** o **Stopped**. Verifíquelo antes de asumir que una fuente está activa.
- El número total de spots rastreados en ese momento se muestra en el cuadro de diálogo y se actualiza a medida que llegan nuevos spots.
- Cada consola de fuente (Cluster Console, RBN Console, WSJT-X Decodes, POTA Activations, FreeDV Spots, SpotCollector Spots) desplaza automáticamente el contenido cuando usted está al final, pero deja de seguir si sube para revisar el tráfico anterior.
- El coloreado DXCC no tiene efecto a menos que haya cargado un archivo ADIF con `Log File (ADIF):`.

## Relacionado

- [Conectarse a un cluster de DX](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectarse a la Reverse Beacon Network](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Habilitar la fuente UDP de SpotCollector](enable-spotcollector-udp-feed.md)
- [Consultar activaciones de POTA](poll-pota-activations.md)
- [Habilitar el WebSocket del reportador de QSO de FreeDV](enable-freedv-qso-reporter-websocket)
