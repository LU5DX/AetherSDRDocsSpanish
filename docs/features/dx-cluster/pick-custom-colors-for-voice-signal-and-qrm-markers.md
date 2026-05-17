# SpotHub

El cuadro de diálogo SpotHub es el control central para conectarse a fuentes de puntos DX, que incluyen un clúster DX tradicional, la Reverse Beacon Network (RBN), WSJT-X, SpotCollector, POTA y FreeDV. También proporciona controles completos sobre cómo aparecen los puntos en el panadapter, incluidos los marcadores de Historial de Señales y la coloración por DXCC.

## Abrir SpotHub

1. Haga clic en **Settings** > **SpotHub...**.

El cuadro de diálogo contiene pestañas para cada fuente de puntos y una pestaña Display unificada para la personalización visual.

---

## Cluster (pestaña)

Se conecta a un clúster DX tradicional a través de telnet.

| Control | Descripción | Setting key |
|---|---|---|
| **Server:** | Nombre del host del clúster DX. | `ClusterHost` |
| **Port:** | Puerto Telnet (1-65535). | `ClusterPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado al clúster. | `ClusterCallsign` |
| **Connect / Disconnect** | Activa o desactiva la conexión telnet. | — |
| **Auto-connect on startup** | Cuando está habilitado, se conecta automáticamente al inicio. | `ClusterAutoConnect` |
| **Startup Commands...** | Abre el editor de comandos de inicio. Los comandos ingresados aquí (uno por línea) se envían automáticamente después de cada inicio de sesión. Los comandos admitidos incluyen `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`, etc. | `DxClusterStartupCommands` |
| **Cluster Console** | Consola telnet de solo lectura que muestra el tráfico sin procesar del clúster. | — |
| **Send** | Envía un comando escrito al clúster. | — |
| **Spot Color:** | Abre un selector de color para los puntos del clúster en el panadapter. | `ClusterSpotColor` |

---

## RBN (pestaña)

Fuente telnet de la Reverse Beacon Network con limitación de velocidad.

| Control | Descripción | Setting key |
|---|---|---|
| **Server:** | Nombre del host telnet de RBN. | `RbnHost` |
| **Port:** | Puerto telnet de RBN (1-65535). | `RbnPort` |
| **Callsign:** | Indicativo de inicio de sesión para RBN. | `RbnCallsign` |
| **Rate Limit:** | Limita la cantidad de puntos RBN por segundo. | `RbnRateLimit` |
| **Connect / Disconnect** | Activa o desactiva la conexión RBN. | — |
| **Auto-connect on startup** | Cuando está habilitado, inicia RBN automáticamente al inicio. | `RbnAutoConnect` |
| **Startup Commands...** | Abre el editor de comandos de inicio para comandos específicos de RBN (independiente de la pestaña DX Cluster). Los comandos se envían después de cada inicio de sesión. | `RbnStartupCommands` |
| **RBN Console** | Consola de solo lectura del tráfico de RBN. | — |
| **Send** | Envía un comando a RBN. | — |
| **Spot Color:** | Selector de color para puntos RBN. | `RbnSpotColor` |

---

## WSJT-X (pestaña)

Receptor UDP para decodificaciones de WSJT-X con filtrado y personalización de color.

| Control | Descripción | Setting key |
|---|---|---|
| **Address:** | Dirección de enlace UDP para mensajes de WSJT-X. | `WsjtxAddress` |
| **Port:** | Puerto UDP para WSJT-X (1-65535). | `WsjtxPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia el receptor automáticamente al inicio. | `WsjtxAutoStart` |
| **CQ** | Muestra solo llamadas CQ. | `WsjtxFilterCQ` |
| **CQ POTA** | Muestra llamadas CQ POTA. | `WsjtxFilterPOTA` |
| **Calling Me** | Muestra solo decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` |
| **Spot Color: (CQ / POTA / Calling Me / Default)** | Selectores de color para cada categoría de punto WSJT-X. | `WsjtxColorCQ`, `WsjtxColorPOTA`, `WsjtxColorCallingMe`, `WsjtxColorDefault` |
| **WSJT-X Decodes** | Consola que muestra las transmisiones decodificadas. | — |
| **Spot Life:** | Segundos que los puntos WSJT-X permanecen en el panadapter. | `WsjtxSpotLife` |

---

## SpotCollector (pestaña)

Receptor UDP para transmisiones de Ham Radio Deluxe SpotCollector.

| Control | Descripción | Setting key |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que transmite SpotCollector (1-65535). | `SpotCollectorPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia el receptor automáticamente al inicio. | `SpotCollectorAutoStart` |
| **SpotCollector Spots** | Consola que muestra los puntos recibidos de SpotCollector. | — |

---

## POTA (pestaña)

Consulta api.pota.app para obtener activaciones actuales.

| Control | Descripción | Setting key |
|---|---|---|
| **Server:** | Punto final fijo: api.pota.app (consulta HTTP). | — |
| **Poll Interval:** | Segundos entre consultas a POTA. | `PotaPollInterval` |
| **Start / Stop** | Inicia o detiene la consulta. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia la consulta a POTA automáticamente al inicio. | `PotaAutoStart` |
| **POTA Activations** | Consola que muestra el flujo de activaciones. | — |
| **Spot Color:** | Selector de color para puntos POTA. | `PotaSpotColor` |

---

## FreeDV (pestaña)

Fuente WebSocket de puntos del reportero de QSO de FreeDV.

| Control | Descripción | Setting key |
|---|---|---|
| **Server:** | Punto final fijo: qso.freedv.org (WebSocket). | — |
| **Start / Stop** | Conecta o desconecta el WebSocket. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia FreeDV automáticamente al inicio. | `FreeDvAutoStart` |
| **FreeDV Spots** | Consola que muestra la actividad de FreeDV. | — |
| **Spot Color:** | Selector de color para puntos FreeDV. | `FreeDvSpotColor` |

---

## Spot List (pestaña)

Tabla unificada y buscable de todos los puntos activos de todas las fuentes.

| Control | Descripción |
|---|---|
| **Bands:** | Casillas de verificación por banda para alternar la visibilidad. Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). |
| **Clear** | Vacia la lista de puntos actual. |
| **Spot table** | Tabla ordenable con las columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. Haga doble clic en una fila para sintonizar esa frecuencia. |

---

## Display (pestaña)

Controla cómo aparecen los puntos y marcadores en el panadapter. Esta pestaña combina la configuración de visualización de puntos, la coloración por DXCC y los ajustes del Historial de Señales.

### Fila de activación superior

| Control | Predeterminado | Descripción | Setting key |
|---|---|---|---|
| **Spots:** | Habilitado | Activación principal de la superposición de puntos DX. | `IsSpotsEnabled` |
| **Memories:** | Deshabilitado | Alterna la superposición de canales de memoria en el panadapter. | `IsMemorySpotsEnabled` |
| **Auto:** | Habilitado | Cambia automáticamente el modo del slice al hacer clic en un punto que incluye información de modo (ej. CW, FT8, RTTY). | `SpotAutoSwitchMode` |
| **Signals** (Signal History) | Deshabilitado | Marcadores dorados para señales de ancho de voz detectadas en el panadapter. Misma activación que **View > Signal History Markers**. | `SHistoryMarkersEnabled` |
| **QRM** (Signal History) | Deshabilitado | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Misma activación que **View > QRM History Markers**. | `SHistoryQrmEnabled` |
| **Clear All** | — | Borra todos los puntos DX, el feed de memoria, los marcadores de Historial de Señales y los marcadores de QRM del espectro. | — |

### Deslizadores de apariencia de puntos

| Control | Predeterminado | Rango válido | Descripción | Setting key |
|---|---|---|---|---|
| **Levels:** | 3 | 1-10 | Número de filas de apilamiento vertical para puntos. | `SpotsMaxLevel` |
| **Position:** | 50 | 0-100 | Posición vertical en el panadapter. | `SpotsStartingHeightPercentage` |
| **Font Size:** | 16 | 8-32 | Tamaño del texto del punto. | `SpotFontSize` |
| **Spot Lifetime:** | — | 10 seg – 24 hrs (pasos no lineales) | Segundos antes de que un punto se desvanezca. | `DxClusterSpotLifetimeSec` |

### Colores de anulación

| Control | Predeterminado | Descripción | Setting key |
|---|---|---|---|
| **Override Colors:** | Deshabilitado | Fuerza un solo color de texto para todos los puntos. | `IsSpotsOverrideColorsEnabled` |
| **Spot text color picker** | `#FFFF00` | Abre un selector de color para el color del texto del punto. | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilitado | Habilita un color de fondo de punto personalizado. | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Habilitado | Selecciona automáticamente el color de fondo para contraste. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| **Spot background color picker** | `#000000` | Abre un selector de color para el color de fondo del punto. | `SpotsOverrideBgColor` |
| **Background Opacity:** | 48 | 0-100 | Opacidad del color de fondo del punto. | `SpotsBackgroundOpacity` |
| **Spot Lines:** | Habilitado | Dibuja líneas verticales desde el espectro hasta cada etiqueta de punto. Deshabilítelo durante concursos para reducir el desorden visual. | `IsSpotsLinesEnabled` |

### Indicador de puntos totales

Recuento en vivo de los puntos actualmente rastreados en todas las fuentes.

### DXCC Coloring (sección)

Colorea los puntos por estado de DXCC trabajado/confirmado/necesario usando un registro ADIF importado.

| Control | Descripción | Setting key |
|---|---|---|
| **DXCC Colors:** | Habilita la coloración de puntos basada en DXCC. | `IsDxccColoringEnabled` |
| **Log File (ADIF):** | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Vigila automáticamente el archivo en busca de cambios después de la selección. | `DxccAdifFilePath` |
| **Imported: (DXCC stats)** | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`. | — |
| **New DXCC / New Band / New Mode / Worked** | Abre un selector de color para cada categoría de estado DXCC. | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` |

### Signal History (sección)

Controles para el comportamiento y la apariencia de los marcadores del Historial de Señales.

| Control | Predeterminado | Rango válido | Descripción | Setting key |
|---|---|---|---|---|
| **Marker Lifetime:** | 60 | 15-300 seg | Cuánto tiempo persiste un marcador de Historial de Señales inactivo antes de ser eliminado. | `SHistoryLifetimeS` |
| **QRM Gate:** | 6 | 3-30 seg | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM. | `SHistoryQrmGateS` |
| **Edge Threshold:** | 3,0 | 1,0-10,0 dB | Umbral por encima del piso de ruido para el recorrido del borde de pendiente que refina el borde del lado de la portadora de S-History. Valores más bajos acercan el marcador a la portadora. | `SHistorySoftEdgeDb` |
| **Signals** | `#FFC800` (dorado) | Cualquier QColor | Color para marcadores de señal de voz. | `SHistoryColorSignals` |
| **QRM** | `#FF0000` (rojo) | Cualquier QColor | Color para marcadores de QRM. | `SHistoryColorQrm` |
| **Snap to Step:** | Deshabilitado | — | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. | `SHistorySnapToStep` |

---

## Editor de Comandos de Inicio

Las pestañas **Cluster** y **RBN** tienen cada una un botón **Startup Commands...** que abre un cuadro de diálogo para editar los comandos enviados automáticamente después de cada inicio de sesión. Cada fuente almacena sus comandos de forma independiente.

### Editar comandos de inicio

1. Haga clic en **Startup Commands...** en la pestaña Cluster o RBN.
2. Ingrese un comando por línea (ej. `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`).
3. Haga clic en **OK** para guardar, o **Cancel** para descartar los cambios.

Los comandos surten efecto en la próxima conexión o reconexión al clúster.

---

## Indicadores

El cuadro de diálogo SpotHub muestra el estado actual de cada fuente:

| Etiqueta | Estados posibles |
|---|---|
| Status (Cluster/RBN/WSJT-X/SpotCollector/POTA/FreeDV) | Disconnected, Connected, Stopped, Listening, Polling |
| Total spots count | Recuento en vivo de todos los puntos rastreados en todas las fuentes |
| DXCC stats | Recuento de QSO y entidades importados desde el registro ADIF. Formato: `<N> QSOs / <M> entities`. |

---

## Relacionado

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Toggle QRM markers to see persistent carriers and interference](toggle-qrm-markers-to-see-persistent-carriers-and-interference.md)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm
