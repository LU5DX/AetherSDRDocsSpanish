# Descripción general de SpotHub

SpotHub es el concentrador central de AetherSDR para recibir spots de DX de múltiples fuentes y mostrarlos como superposiciones en el panadapter. Úselo para conectarse a un cluster de DX, la Reverse Beacon Network (RBN), WSJT-X, SpotCollector, POTA y FreeDV, y para controlar cómo se ven los spots en pantalla.

## Antes de comenzar

- No se requiere conexión de radio para configurar SpotHub.
- Abra SpotHub desde `Settings > SpotHub...`.

## Cómo funciona

SpotHub agrega spots de hasta seis fuentes independientes. Cada fuente tiene su propia pestaña para los ajustes de conexión, una consola de solo lectura que muestra el tráfico en vivo y un selector de color para los spots. Todos los spots entrantes se integran en una lista unificada y se dibujan como marcadores etiquetados en el panadapter.

### Fuentes

| Pestaña | Cómo se conecta | Qué recibe |
|---|---|---|
| Cluster | Telnet a un host y puerto especificados por el usuario | Spots de DX de un cluster de paquetes tradicional |
| RBN | Telnet a la Reverse Beacon Network | Spots de skimmer de CW, RTTY y FT8 con limitación de tasa opcional |
| WSJT-X | Listener UDP en una dirección y puerto locales | Transmisiones decodificadas de una instancia de WSJT-X en ejecución |
| SpotCollector | Listener UDP en un puerto local | Spots difundidos por Ham Radio Deluxe SpotCollector |
| POTA | Sondeo HTTP de `api.pota.app` | Activaciones actuales de Parks on the Air |
| FreeDV | Conexión WebSocket a `qso.freedv.org` | Spots del reportero de QSO de FreeDV (requiere soporte WebSocket) |

Cada fuente puede iniciarse manualmente o configurarse para iniciarse automáticamente cuando AetherSDR se lanza, usando su respectivo interruptor "Auto-connect on startup" o "Auto-start on startup".

### Pestaña Spot List

La pestaña Spot List muestra una tabla unificada y ordenable de todos los spots activos de cada fuente activa. Las columnas son Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band y Source. Las casillas de verificación por banda filtran qué bandas aparecen en la tabla. Haga doble clic en cualquier fila para sintonizar el VFO activo a la frecuencia de ese spot. Haga clic en Clear para vaciar la lista actual.

### Pestaña Display

La pestaña Display controla cómo aparecen los spots en el panadapter y no afecta la conectividad.

## Qué hace cada control

### Pestaña Cluster

| Control | Comportamiento | Clave de ajuste |
|---|---|---|
| Server: | Nombre de host del cluster de DX | `ClusterHost` |
| Port: | Puerto Telnet (1–65535) | `ClusterPort` |
| Callsign: | Indicativo de inicio de sesión enviado al cluster | `ClusterCallsign` |
| Connect / Disconnect | Activa o desactiva la conexión Telnet | — |
| Auto-connect on startup | Se conecta automáticamente al iniciar | `ClusterAutoConnect` |
| Cluster Console | Visualización de solo lectura del tráfico sin procesar del cluster | — |
| Send | Envía un comando escrito al cluster | — |
| Spot Color: | Abre un selector de color para los spots del cluster | `ClusterSpotColor` |

### Pestaña RBN

| Control | Comportamiento | Clave de ajuste |
|---|---|---|
| Server: | Nombre de host Telnet de RBN | `RbnHost` |
| Port: | Puerto Telnet de RBN (1–65535) | `RbnPort` |
| Callsign: | Indicativo de inicio de sesión enviado a RBN | `RbnCallsign` |
| Rate Limit: | Máximo de spots de RBN por segundo | `RbnRateLimit` |
| Connect / Disconnect | Activa o desactiva la conexión RBN | — |
| Auto-connect on startup | Conecta RBN automáticamente al iniciar | `RbnAutoConnect` |
| RBN Console | Visualización de solo lectura del tráfico sin procesar de RBN | — |
| Send | Envía un comando a RBN | — |
| Spot Color: | Abre un selector de color para los spots de RBN | `RbnSpotColor` |

### Pestaña WSJT-X

| Control | Comportamiento | Clave de ajuste |
|---|---|---|
| Address: | Dirección de enlace UDP para mensajes de WSJT-X | `WsjtxAddress` |
| Port: | Puerto UDP (1–65535) | `WsjtxPort` |
| Start / Stop | Inicia o detiene el listener UDP | — |
| Auto-start on startup | Inicia el listener automáticamente al iniciar | `WsjtxAutoStart` |
| CQ | Muestra spots solo para llamadas CQ | `WsjtxFilterCQ` |
| CQ POTA | Muestra llamadas CQ POTA | `WsjtxFilterPOTA` |
| Calling Me | Muestra decodificaciones dirigidas a su indicativo | `WsjtxFilterCallingMe` |
| CQ color | Color para spots CQ | `WsjtxColorCQ` |
| POTA color | Color para spots CQ POTA | `WsjtxColorPOTA` |
| Calling Me color | Color para spots que lo llaman a usted | `WsjtxColorCallingMe` |
| Default color | Color para todos los demás spots de WSJT-X | `WsjtxColorDefault` |
| WSJT-X Decodes | Consola de solo lectura de transmisiones decodificadas | — |
| Spot Life: | Segundos que los spots de WSJT-X permanecen en el panadapter | `WsjtxSpotLife` |

### Pestaña SpotCollector

| Control | Comportamiento | Clave de ajuste |
|---|---|---|
| UDP Port: | Puerto en el que SpotCollector difunde (1–65535) | `SpotCollectorPort` |
| Start / Stop | Inicia o detiene el listener UDP | — |
| Auto-start on startup | Inicia el listener automáticamente al iniciar | `SpotCollectorAutoStart` |
| SpotCollector Spots | Consola de solo lectura de spots recibidos | — |

### Pestaña POTA

| Control | Comportamiento | Clave de ajuste |
|---|---|---|
| Server: | Punto de acceso fijo: `api.pota.app` (sondeo HTTP) | — |
| Poll Interval: | Segundos entre sondeos de POTA | `PotaPollInterval` |
| Start / Stop | Inicia o detiene el sondeo de POTA | — |
| Auto-start on startup | Inicia el sondeo de POTA automáticamente al iniciar | `PotaAutoStart` |
| POTA Activations | Consola de solo lectura del feed de activaciones | — |
| Spot Color: | Abre un selector de color para los spots de POTA | `PotaSpotColor` |

### Pestaña FreeDV

FreeDV está disponible solo en versiones que incluyen soporte WebSocket.

| Control | Comportamiento | Clave de ajuste |
|---|---|---|
| Server: | Punto de acceso fijo: `qso.freedv.org` (WebSocket) | — |
| Start / Stop | Conecta o desconecta el WebSocket de FreeDV | — |
| Auto-start on startup | Se conecta automáticamente al iniciar | `FreeDvAutoStart` |
| FreeDV Spots | Consola de solo lectura de la actividad de FreeDV | — |
| Spot Color: | Abre un selector de color para los spots de FreeDV | `FreeDvSpotColor` |

### Pestaña Display

| Control | Valor predeterminado | Comportamiento | Clave de ajuste |
|---|---|---|---|
| Spots: | Habilitado | Interruptor principal para la superposición de spots en el panadapter | `IsSpotsEnabled` |
| Memories: | Deshabilitado | Activa o desactiva los marcadores de canales de memoria en el panadapter | `IsMemoriesShownOnPanadapter` |
| Auto Mode: | — | Selecciona automáticamente la densidad de spots según el nivel de zoom | `SpotsAutoMode` |
| Levels: | — | Número de filas de apilamiento vertical para las etiquetas de spots | `SpotsStackLevels` |
| Position: | — | Posición vertical de las etiquetas de spots en el panadapter | `SpotsPosition` |
| Font Size: | — | Tamaño del texto de las etiquetas de spots | `SpotsFontSize` |
| Spot Lifetime: | — | Segundos antes de que un spot desaparezca del panadapter | `SpotsLifetime` |
| Override Colors: | — | Fuerza un único color de texto para todos los spots | `IsSpotsOverrideColorsEnabled` |
| Override Background: Enabled | — | Habilita un color de fondo personalizado para las etiquetas de spots | `IsSpotsOverrideBackgroundColorsEnabled` |
| Override Background: Auto | — | Aplica contraste automático a los fondos de las etiquetas de spots | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Background Opacity: | 48 | Opacidad del fondo de las etiquetas de spots | `SpotsOverrideBgOpacity` |
| DXCC Coloring | — | Colorea los spots según el estado trabajado/confirmado/necesario a partir de un registro ADIF | `DxccColoringEnabled` |
| Log File (ADIF): | — | Carga un archivo de registro ADIF para gestionar el coloreado DXCC | `DxccAdifPath` |
| Auto-Reload Log: | — | Vuelve a leer el archivo ADIF automáticamente cuando cambia | `DxccAutoReload` |
| Clear All Spots | — | Elimina todos los spots actualmente rastreados en todas las fuentes | — |

## Consejos

- El color de los spots de cada fuente puede configurarse de forma independiente. Si habilita Override Colors: en la pestaña Display, ese único color tiene prioridad sobre todos los colores por fuente.
- Auto Mode: reduce el desorden automáticamente en niveles de zoom amplios. Si los spots se superponen, habilítelo antes de ajustar Levels: manualmente.
- DXCC Coloring requiere un archivo de registro ADIF. Habilite Auto-Reload Log: si su software de registro actualiza el archivo durante una sesión, para que el coloreado se mantenga actualizado sin necesidad de reabrir SpotHub.

## Relacionados

- [Conectarse a un cluster de DX](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectarse a la Reverse Beacon Network](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
- [Iniciar el listener UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Habilitar el feed UDP de SpotCollector](enable-spotcollector-udp-feed.md)
- [Sondear activaciones de POTA](poll-pota-activations.md)
- [Habilitar el WebSocket del reportero de QSO de FreeDV](enable-freedv-qso-reporter-websocket.
