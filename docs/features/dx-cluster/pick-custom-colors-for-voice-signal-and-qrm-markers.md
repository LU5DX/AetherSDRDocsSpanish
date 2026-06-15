# SpotHub

El diálogo SpotHub es el control central para conectarse a fuentes de spots de DX, incluido un clúster DX tradicional, la Red de Balizas Inversa (RBN), WSJT-X, SpotCollector, POTA y FreeDV. También proporciona controles integrales sobre cómo aparecen los spots en el panadapter, incluidos los marcadores de Historial de Señales y la coloración por DXCC.

## Abrir SpotHub

1. Haga clic en **Settings** > **SpotHub...**.

El diálogo contiene pestañas para cada fuente de spots y una pestaña Display unificada para la personalización visual.

---

## Cluster (pestaña)

Se conecta a un clúster DX tradicional mediante telnet.

| Control | Descripción | Clave de ajuste |
|---|---|---|
| **Server:** | Nombre de host del clúster DX. | `ClusterHost` |
| **Port:** | Puerto Telnet (1-65535). | `ClusterPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado al clúster. | `ClusterCallsign` |
| **Connect / Disconnect** | Alterna la conexión telnet. | — |
| **Auto-connect on startup** | Cuando está habilitado, se conecta automáticamente al iniciar. | `ClusterAutoConnect` |
| **Startup Commands...** | Abre el editor de comandos de inicio. Los comandos ingresados aquí (uno por línea) se envían automáticamente después de cada inicio de sesión. Los comandos compatibles incluyen `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`, etc. | `DxClusterStartupCommands` |
| **Cluster Console** | Consola telnet de solo lectura que muestra el tráfico sin procesar del clúster. | — |
| **Send** | Envía un comando escrito al clúster. | — |
| **Spot Color:** | Abre un selector de color para los spots del clúster en el panadapter. | `ClusterSpotColor` |

---

## RBN (pestaña)

Fuente telnet de la Red de Balizas Inversa con limitación de velocidad.

| Control | Descripción | Clave de ajuste |
|---|---|---|
| **Server:** | Nombre de host telnet del RBN. | `RbnHost` |
| **Port:** | Puerto telnet del RBN (1-65535). | `RbnPort` |
| **Callsign:** | Indicativo de inicio de sesión para el RBN. | `RbnCallsign` |
| **Rate Limit:** | Limita la cantidad de spots del RBN por segundo. | `RbnRateLimit` |
| **Connect / Disconnect** | Alterna la conexión RBN. | — |
| **Auto-connect on startup** | Cuando está habilitado, inicia el RBN automáticamente al iniciar. | `RbnAutoConnect` |
| **Startup Commands...** | Abre el editor de comandos de inicio para comandos específicos del RBN (independiente de la pestaña DX Cluster). Los comandos se envían después de cada inicio de sesión. | `RbnStartupCommands` |
| **RBN Console** | Consola de solo lectura del tráfico del RBN. | — |
| **Send** | Envía un comando al RBN. | — |
| **Spot Color:** | Selector de color para spots del RBN. | `RbnSpotColor` |

---

## WSJT-X (pestaña)

Receptor UDP para decodificaciones de WSJT-X con filtrado y personalización de color.

| Control | Descripción | Clave de ajuste |
|---|---|---|
| **Address:** | Dirección de enlace UDP para mensajes de WSJT-X. | `WsjtxAddress` |
| **Port:** | Puerto UDP para WSJT-X (1-65535). | `WsjtxPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia el receptor automáticamente al iniciar. | `WsjtxAutoStart` |
| **CQ** | Muestra solo llamadas CQ. | `WsjtxFilterCQ` |
| **CQ POTA** | Muestra llamadas CQ POTA. | `WsjtxFilterPOTA` |
| **Calling Me** | Muestra solo decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` |
| **Spot Color: (CQ / POTA / Calling Me / Default)** | Selectores de color para cada categoría de spot de WSJT-X. | `WsjtxColorCQ`, `WsjtxColorPOTA`, `WsjtxColorCallingMe`, `WsjtxColorDefault` |
| **WSJT-X Decodes** | Consola que muestra las transmisiones decodificadas. | — |
| **Spot Life:** | Segundos que los spots de WSJT-X permanecen en el panadapter. | `WsjtxSpotLife` |

---

## SpotCollector (pestaña)

Receptor UDP para transmisiones de Ham Radio Deluxe SpotCollector.

| Control | Descripción | Clave de ajuste |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que transmite SpotCollector (1-65535). | `SpotCollectorPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia el receptor automáticamente al iniciar. | `SpotCollectorAutoStart` |
| **SpotCollector Spots** | Consola que muestra los spots recibidos de SpotCollector. | — |

---

## POTA (pestaña)

Consulta api.pota.app para obtener activaciones actuales.

| Control | Descripción | Clave de ajuste |
|---|---|---|
| **Server:** | Punto final fijo: api.pota.app (consulta HTTP). | — |
| **Poll Interval:** | Segundos entre consultas a POTA. | `PotaPollInterval` |
| **Start / Stop** | Inicia o detiene las consultas. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia las consultas a POTA automáticamente al iniciar. | `PotaAutoStart` |
| **POTA Activations** | Consola que muestra el flujo de activaciones. | — |
| **Spot Color:** | Selector de color para spots de POTA. | `PotaSpotColor` |

---

## FreeDV (pestaña)

Flujo WebSocket de spots del reportador de QSO de FreeDV.

| Control | Descripción | Clave de ajuste |
|---|---|---|
| **Server:** | Punto final fijo: qso.freedv.org (WebSocket). | — |
| **Start / Stop** | Conecta o desconecta el WebSocket. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia FreeDV automáticamente al iniciar. | `FreeDvAutoStart` |
| **FreeDV Spots** | Consola que muestra la actividad de FreeDV. | — |
| **Spot Color:** | Selector de color para spots de FreeDV. | `FreeDvSpotColor` |

---

## Spot List (pestaña)

Tabla de búsqueda unificada de todos los spots activos de todas las fuentes.

| Control | Descripción |
|---|---|
| **Bands:** | Casillas de verificación por banda para alternar la visibilidad. Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). |
| **Clear** | Vacía la lista de spots actual. |
| **Spot table** | Tabla ordenable con columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. Haga doble clic en una fila para sintonizar esa frecuencia. |

---

## Display (pestaña)

Controla cómo aparecen los spots y marcadores en el panadapter. Esta pestaña combina la configuración de visualización de spots, la coloración por DXCC y los parámetros ajustables del Historial de Señales.

### Filas de alternancia superiores

| Control | Predeterminado | Descripción | Clave de ajuste |
|---|---|---|---|
| **Spots:** | Habilitado | Alternancia maestra para la superposición de spots DX. | `IsSpotsEnabled` |
| **Memories:** | Deshabilitado | Alterna la superposición de canales de memoria en el panadapter. | `IsMemorySpotsEnabled` |
| **Auto:** | Habilitado | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (p. ej., CW, FT8, RTTY). | `SpotAutoSwitchMode` |
| **Signals** (Signal History) | Deshabilitado | Marcadores dorados para señales de ancho de voz detectadas en el panadapter. Misma alternancia que **View > Signal History Markers**. | `SHistoryMarkersEnabled` |
| **QRM** (Signal History) | Deshabilitado | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Misma alternancia que **View > QRM History Markers**. | `SHistoryQrmEnabled` |
| **Clear All** | — | Limpia todos los spots DX, el feed de memoria, los marcadores de Signal History y los marcadores QRM del espectro. | — |

### Deslizadores de apariencia de spots

| Control | Predeterminado | Rango válido | Descripción | Clave de ajuste |
|---|---|---|---|---|
| **Levels:** | 3 | 1-10 | Número de filas de apilamiento vertical para spots. | `SpotsMaxLevel` |
| **Position:** | 50 | 0-100 | Posición vertical en el panadapter. | `SpotsStartingHeightPercentage` |
| **Font Size:** | 16 | 8-32 | Tamaño del texto del spot. | `SpotFontSize` |
| **Spot Lifetime:** | — | 10 seg – 24 horas (pasos no lineales) | Segundos antes de que un spot se desvanezca. | `DxClusterSpotLifetimeSec` |

### Colores de anulación

| Control | Predeterminado | Descripción | Clave de ajuste |
|---|---|---|---|
| **Override Colors:** | Deshabilitado | Fuerza un solo color de texto para todos los spots. La etiqueta del botón es estática y siempre muestra "Enabled" cuando está marcado. | `IsSpotsOverrideColorsEnabled` |
| **Selector de color de texto de spot** | `#FFFF00` | Abre el selector de color para el color del texto del spot. | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilitado | Habilita un color de fondo personalizado para los spots. | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Habilitado | Selecciona automáticamente el color de fondo para el contraste. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| **Selector de color de fondo de spot** | `#000000` | Abre el selector de color para el color de fondo del spot. | `SpotsOverrideBgColor` |
| **Background Opacity:** | 48 | 0-100 | Opacidad del color de fondo del spot. | `SpotsBackgroundOpacity` |
| **Spot Lines:** | Habilitado | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Deshabilítelo durante concursos para reducir el desorden visual. La etiqueta del botón es estática y siempre muestra "Enabled" cuando está marcado. | `IsSpotsLinesEnabled` |

### Indicador Total Spots

Recuento en vivo de los spots actualmente rastreados en todas las fuentes.

### DXCC Coloring (sección)

Colorea los spots según el estado DXCC trabajado/confirmado/necesario utilizando un registro ADIF importado.

| Control | Descripción | Clave de ajuste |
|---|---|---|
| **DXCC Colors:** | Habilita la coloración de spots basada en DXCC. La etiqueta del botón es estática y siempre muestra "Enabled" cuando está marcado. | `IsDxccColoringEnabled` |
| **Log File (ADIF):** | Carga un archivo de registro ADIF para impulsar la coloración por DXCC. Vigila automáticamente el archivo en busca de cambios después de la selección. | `DxccAdifFilePath` |
| **Imported: (estadísticas DXCC)** | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`. | — |
| **New DXCC / New Band / New Mode / Worked** muestras de color | Abre un selector de color para cada categoría de estado DXCC. | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` |

### Signal History (sección)

Controles para el comportamiento y la apariencia de los marcadores de Signal History.

| Control | Predeterminado | Rango válido | Descripción | Clave de ajuste |
|---|---|---|---|---|
| **Marker Lifetime:** | 60 | 15-300 seg | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado. | `SHistoryLifetimeS` |
| **QRM Gate:** | 6 | 3-30 seg | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM. | `SHistoryQrmGateS` |
| **Edge Threshold:** | 3.0 | 1.0-10.0 dB | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde del lado de la portadora de S-History. Los valores más bajos acercan el marcador a la portadora. | `SHistorySoftEdgeDb` |
| **Signals** muestra de color | `#FFC800` (dorado) | Cualquier QColor | Color para los marcadores de señales de voz. | `SHistoryColorSignals` |
| **QRM** muestra de color | `#FF0000` (rojo) | Cualquier QColor | Color para los marcadores QRM. | `SHistoryColorQrm` |
| **Snap to Step:** | Deshabilitado | — | Redondea el clic-para-sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. La etiqueta del botón es estática y siempre muestra "Enabled" cuando está marcado. | `SHistorySnapToStep` |

> **Nota:** En v26.6.3, varios botones de alternancia se actualizaron para mostrar una etiqueta estática (siempre "Enabled") cuando están en estado marcado, en lugar de cambiar dinámicamente entre "Enabled" y "Disabled". Esto afecta a: **Override Colors:**, **Spot Lines:**, **DXCC Colors:** y **Snap to Step:**. La apariencia visual del botón (presionado/suelto) aún indica el estado actual.

---

## Editor de comandos de inicio

Las pestañas **Cluster** y **RBN** tienen cada una un botón **Startup Commands...** que abre un diálogo para editar comandos enviados automáticamente después de cada inicio de sesión. Cada fuente almacena sus comandos de forma independiente.

### Edición de comandos de inicio

1. Haga clic en **Startup Commands...** en la pestaña Cluster o RBN.
2. Ingrese un comando por línea (p. ej., `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`).
3. Haga clic en **OK** para guardar, o en **Cancel** para descartar los cambios.

Los comandos surten efecto en la siguiente conexión o reconexión al clúster.

---

## Indicadores

El diálogo SpotHub muestra el estado actual de cada fuente:

| Etiqueta | Estados posibles |
|---|---|
| Status (Cluster/RBN/WSJT-X/SpotCollector/POTA/FreeDV) | Disconnected, Connected, Stopped
