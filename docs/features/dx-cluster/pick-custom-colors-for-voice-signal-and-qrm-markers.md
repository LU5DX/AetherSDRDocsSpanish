# SpotHub

El cuadro de diálogo de SpotHub es el control central para conectarse a fuentes de avisos de DX, incluyendo un clúster de DX tradicional, la Red Inversa de Balizas (RBN), WSJT-X, SpotCollector, POTA y FreeDV. También proporciona controles completos sobre cómo aparecen los avisos en el panadapter, incluyendo los marcadores de Historial de Señales y el coloreado por DXCC.

## Abrir SpotHub

1. Haga clic en **Settings** > **SpotHub...**.

El cuadro de diálogo contiene pestañas para cada fuente de avisos y una pestaña unificada Display para la personalización visual.

---

## Cluster (pestaña)

Se conecta a un clúster de DX tradicional a través de telnet.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host del clúster de DX. | `ClusterHost` |
| **Port:** | Puerto Telnet (1-65535). | `ClusterPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado al clúster. | `ClusterCallsign` |
| **Connect / Disconnect** | Activa o desactiva la conexión telnet. | — |
| **Auto-connect on startup** | Cuando está habilitado, se conecta automáticamente al iniciar. | `ClusterAutoConnect` |
| **Startup Commands...** | Abre el editor de comandos de inicio. Los comandos introducidos aquí (uno por línea) se envían automáticamente después de cada inicio de sesión. Los comandos compatibles incluyen `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`, etc. | `DxClusterStartupCommands` |
| **Cluster Console** | Consola telnet de solo lectura que muestra el tráfico bruto del clúster. | — |
| **Send** | Envía un comando escrito al clúster. | — |
| **Spot Color:** | Abre un selector de color para los avisos del clúster en el panadapter. | `ClusterSpotColor` |

---

## RBN (pestaña)

Fuente telnet de la Red Inversa de Balizas con limitación de velocidad.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host telnet de RBN. | `RbnHost` |
| **Port:** | Puerto telnet de RBN (1-65535). | `RbnPort` |
| **Callsign:** | Indicativo de inicio de sesión para RBN. | `RbnCallsign` |
| **Rate Limit:** | Limita el número de avisos de RBN por segundo. | `RbnRateLimit` |
| **Connect / Disconnect** | Activa o desactiva la conexión RBN. | — |
| **Auto-connect on startup** | Cuando está habilitado, inicia RBN automáticamente al iniciar. | `RbnAutoConnect` |
| **Startup Commands...** | Abre el editor de comandos de inicio para comandos específicos de RBN (independiente de la pestaña DX Cluster). Los comandos se envían después de cada inicio de sesión. | `RbnStartupCommands` |
| **RBN Console** | Consola de solo lectura del tráfico de RBN. | — |
| **Send** | Envía un comando a RBN. | — |
| **Spot Color:** | Selector de color para avisos de RBN. | `RbnSpotColor` |

---

## WSJT-X (pestaña)

Receptor UDP para decodificaciones de WSJT-X con filtrado y personalización de color.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Address:** | Dirección de enlace UDP para mensajes de WSJT-X. | `WsjtxAddress` |
| **Port:** | Puerto UDP para WSJT-X (1-65535). | `WsjtxPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia el receptor automáticamente al iniciar. | `WsjtxAutoStart` |
| **CQ** | Muestra solo llamadas CQ. | `WsjtxFilterCQ` |
| **CQ POTA** | Muestra llamadas CQ POTA. | `WsjtxFilterPOTA` |
| **Calling Me** | Muestra solo decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` |
| **Spot Color: (CQ / POTA / Calling Me / Default)** | Selectores de color para cada categoría de aviso de WSJT-X. | `WsjtxColorCQ`, `WsjtxColorPOTA`, `WsjtxColorCallingMe`, `WsjtxColorDefault` |
| **WSJT-X Decodes** | Consola que muestra las transmisiones decodificadas. | — |
| **Spot Life:** | Segundos que los avisos de WSJT-X permanecen en el panadapter. | `WsjtxSpotLife` |

---

## SpotCollector (pestaña)

Receptor UDP para las transmisiones de Ham Radio Deluxe SpotCollector.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que SpotCollector transmite (1-65535). | `SpotCollectorPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia el receptor automáticamente al iniciar. | `SpotCollectorAutoStart` |
| **SpotCollector Spots** | Consola que muestra los avisos recibidos de SpotCollector. | — |

---

## POTA (pestaña)

Consulta api.pota.app para obtener activaciones actuales.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Punto final fijo: api.pota.app (consulta HTTP). | — |
| **Poll Interval:** | Segundos entre consultas a POTA. | `PotaPollInterval` |
| **Start / Stop** | Inicia o detiene la consulta. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia la consulta a POTA automáticamente al iniciar. | `PotaAutoStart` |
| **POTA Activations** | Consola que muestra el flujo de activaciones. | — |
| **Spot Color:** | Selector de color para avisos de POTA. | `PotaSpotColor` |

---

## FreeDV (pestaña)

Flujo WebSocket de avisos del reportador de QSO de FreeDV.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Punto final fijo: qso.freedv.org (WebSocket). | — |
| **Start / Stop** | Conecta o desconecta el WebSocket. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia FreeDV automáticamente al iniciar. | `FreeDvAutoStart` |
| **FreeDV Spots** | Consola que muestra la actividad de FreeDV. | — |
| **Spot Color:** | Selector de color para avisos de FreeDV. | `FreeDvSpotColor` |

---

## Spot List (pestaña)

Tabla unificada y buscable de todos los avisos activos de todas las fuentes.

| Control | Descripción |
|---|---|
| **Bands:** | Casillas de verificación por banda para alternar la visibilidad. Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). |
| **Clear** | Vacía la lista de avisos actual. |
| **Spot table** | Tabla ordenable con columnas: Hora, Frec, Indicativo DX, Comentario, Reportador, Banda, Modo, Fuente. Haga doble clic en una fila para sintonizar esa frecuencia. |

---

## Display (pestaña)

Controla cómo aparecen los avisos y marcadores en el panadapter. Esta pestaña combina la configuración de visualización de avisos, el coloreado por DXCC y los ajustes del Historial de Señales.

### Fila de activación superior

| Control | Valor predeterminado | Descripción | Clave de configuración |
|---|---|---|---|
| **Spots:** | Habilitado | Activación general para la superposición de avisos de DX. | `IsSpotsEnabled` |
| **Memories:** | Deshabilitado | Alterna la superposición de canales de memoria en el panadapter. | `IsMemorySpotsEnabled` |
| **Auto:** | Habilitado | Cambia automáticamente el modo del slice al hacer clic en un aviso que incluye información de modo (p. ej., CW, FT8, RTTY). | `SpotAutoSwitchMode` |
| **Signals** (Historial de Señales) | Deshabilitado | Marcadores dorados para señales de ancho de voz detectadas en el panadapter. Misma activación que **View > Signal History Markers**. | `SHistoryMarkersEnabled` |
| **QRM** (Historial de Señales) | Deshabilitado | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Misma activación que **View > QRM History Markers**. | `SHistoryQrmEnabled` |
| **Clear All** | — | Limpia todos los avisos de DX, el feed de memoria, los marcadores de Historial de Señales y los marcadores de QRM del espectro. | — |

### Controles deslizantes de apariencia de avisos

| Control | Valor predeterminado | Rango válido | Descripción | Clave de configuración |
|---|---|---|---|---|
| **Levels:** | 3 | 1-10 | Número de filas de apilamiento vertical para avisos. | `SpotsMaxLevel` |
| **Position:** | 50 | 0-100 | Posición vertical en el panadapter. | `SpotsStartingHeightPercentage` |
| **Font Size:** | 16 | 8-32 | Tamaño del texto del aviso. | `SpotFontSize` |
| **Spot Lifetime:** | — | 10 seg – 24 horas (pasos no lineales) | Segundos antes de que un aviso se desvanezca. | `DxClusterSpotLifetimeSec` |

### Colores de anulación

| Control | Valor predeterminado | Descripción | Clave de configuración |
|---|---|---|---|
| **Override Colors:** | Deshabilitado | Fuerza un solo color de texto para todos los avisos. | `IsSpotsOverrideColorsEnabled` |
| **Selector de color de texto de aviso** | `#FFFF00` | Abre el selector de color para el color del texto del aviso. | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilitado | Habilita el color de fondo personalizado del aviso. | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Habilitado | Selecciona automáticamente el color de fondo para contraste. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| **Selector de color de fondo de aviso** | `#000000` | Abre el selector de color para el color de fondo del aviso. | `SpotsOverrideBgColor` |
| **Background Opacity:** | 48 | 0-100 | Opacidad del color de fondo del aviso. | `SpotsBackgroundOpacity` |
| **Spot Lines:** | Habilitado | Dibuja líneas verticales desde el espectro hasta cada etiqueta de aviso. Deshabilítelo durante concursos para reducir el desorden visual. | `IsSpotsLinesEnabled` |

### Indicador de avisos totales

Recuento en vivo de los avisos actualmente rastreados en todas las fuentes.

### Coloreado DXCC (sección)

Colorea los avisos según el estado de DXCC trabajado/confirmado/necesario utilizando un registro ADIF importado.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **DXCC Colors:** | Habilita el coloreado de avisos basado en DXCC. | `IsDxccColoringEnabled` |
| **Log File (ADIF):** | Carga un archivo de registro ADIF para impulsar el coloreado DXCC. Vigila automáticamente el archivo para detectar cambios después de la selección. | `DxccAdifFilePath` |
| **Imported: (estadísticas DXCC)** | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`. | — |
| **Muestras de color Nuevo DXCC / Nueva Banda / Nuevo Modo / Trabajado** | Abre un selector de color para cada categoría de estado DXCC. | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` |

### Historial de Señales (sección)

Controles para el comportamiento y la apariencia de los marcadores del Historial de Señales.

| Control | Valor predeterminado | Rango válido | Descripción | Clave de configuración |
|---|---|---|---|---|
| **Marker Lifetime:** | 60 | 15-300 seg | Cuánto tiempo persiste un marcador inactivo del Historial de Señales antes de ser eliminado. | `SHistoryLifetimeS` |
| **QRM Gate:** | 6 | 3-30 seg | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM. | `SHistoryQrmGateS` |
| **Edge Threshold:** | 3.0 | 1.0-10.0 dB | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde del lado de la portadora de S-History. Los valores más bajos acercan el marcador a la portadora. | `SHistorySoftEdgeDb` |
| **Muestra de color Signals** | `#FFC800` (dorado) | Cualquier QColor | Color para los marcadores de señal de voz. | `SHistoryColorSignals` |
| **Muestra de color QRM** | `#FF0000` (rojo) | Cualquier QColor | Color para los marcadores QRM. | `SHistoryColorQrm` |
| **Snap to Step:** | Deshabilitado | — | Redondea el clic-para-sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. | `SHistorySnapToStep` |

---

## Editor de comandos de inicio

Las pestañas **Cluster** y **RBN** tienen cada una un botón **Startup Commands...** que abre un cuadro de diálogo para editar los comandos enviados automáticamente después de cada inicio de sesión. Cada fuente almacena sus comandos de forma independiente.

### Edición de comandos de inicio

1. Haga clic en **Startup Commands...** en la pestaña Cluster o RBN.
2. Introduzca un comando por línea (p. ej., `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`).
3. Haga clic en **OK** para guardar o **Cancel** para descartar los cambios.

Los comandos surten efecto en la siguiente conexión o reconexión al clúster.

---

## Indicadores

El cuadro de diálogo SpotHub muestra el estado actual de cada fuente:

| Etiqueta | Estados posibles |
|---|---|
| Estado (Cluster/RBN/WSJT-X/SpotCollector/POTA/FreeDV) | Desconectado, Conectado, Detenido, Escuchando, Consultando |
| Recuento de avisos totales | Recuento en vivo de todos los avisos rastreados en todas las fuentes |
| Estadísticas DXCC | Recuento de QSO y entidades importados del registro ADIF. Formato: `<N> QSOs / <M> entities`. |

---

## Relacionados

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Toggle QRM markers to see persistent carriers and interference](toggle-qrm-markers-to-see-persistent-carriers-and-interference.md)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm
