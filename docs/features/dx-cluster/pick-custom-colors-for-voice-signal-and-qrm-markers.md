# SpotHub

El diálogo SpotHub es el control central para conectarse a fuentes de spots DX, incluyendo un clúster DX tradicional, la Reverse Beacon Network (RBN), WSJT-X, SpotCollector, POTA, FreeDV y N1MM. También proporciona controles completos sobre cómo aparecen los spots en el panadapter, incluidos los marcadores de Signal History y la coloración por DXCC.

## Abrir SpotHub

1. Haga clic en **Settings** > **SpotHub...**.

El diálogo contiene pestañas para cada fuente de spots y una pestaña Display unificada para la personalización visual.

---

## Cluster (pestaña)

Se conecta a un clúster DX tradicional mediante telnet.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host del clúster DX. | `ClusterHost` |
| **Port:** | Puerto telnet (1-65535). | `ClusterPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado al clúster. | `ClusterCallsign` |
| **Connect / Disconnect** | Alterna la conexión telnet. | — |
| **Auto-connect on startup** | Cuando está habilitado, se conecta automáticamente al iniciar. | `ClusterAutoConnect` |
| **Startup Commands...** | Abre el editor de comandos de inicio. Los comandos ingresados aquí (uno por línea) se envían automáticamente después de cada inicio de sesión. Los comandos admitidos incluyen `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`, etc. | `DxClusterStartupCommands` |
| **Cluster Console** | Consola telnet de solo lectura que muestra el tráfico sin procesar del clúster. | — |
| **Send** | Envía un comando escrito al clúster. | — |
| **Spot Color:** | Abre un selector de color para los spots del clúster en el panadapter. | `ClusterSpotColor` |

---

## RBN (pestaña)

Fuente telnet de Reverse Beacon Network con limitación de velocidad.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre de host telnet de RBN. | `RbnHost` |
| **Port:** | Puerto telnet de RBN (1-65535). | `RbnPort` |
| **Callsign:** | Indicativo de inicio de sesión para RBN. | `RbnCallsign` |
| **Rate Limit:** | Limita la cantidad de spots RBN por segundo. | `RbnRateLimit` |
| **Connect / Disconnect** | Alterna la conexión RBN. | — |
| **Auto-connect on startup** | Cuando está habilitado, inicia RBN automáticamente al arrancar. | `RbnAutoConnect` |
| **Startup Commands...** | Abre el editor de comandos de inicio para comandos específicos de RBN (independiente de la pestaña DX Cluster). Los comandos se envían después de cada inicio de sesión. | `RbnStartupCommands` |
| **RBN Console** | Consola de solo lectura del tráfico RBN. | — |
| **Send** | Envía un comando a RBN. | — |
| **Spot Color:** | Selector de color para spots RBN. | `RbnSpotColor` |

---

## WSJT-X (pestaña)

Receptor UDP para decodificaciones de WSJT-X con filtrado y personalización de colores.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Address:** | Dirección de enlace UDP para mensajes de WSJT-X. | `WsjtxAddress` |
| **Port:** | Puerto UDP para WSJT-X (1-65535). | `WsjtxPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia el receptor automáticamente al arrancar. | `WsjtxAutoStart` |
| **CQ** | Muestra solo llamadas CQ. | `WsjtxFilterCQ` |
| **CQ POTA** | Muestra llamadas CQ POTA. | `WsjtxFilterPOTA` |
| **Calling Me** | Muestra solo decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` |
| **Spot Color: (CQ / POTA / Calling Me / Default)** | Selectores de color para cada categoría de spot WSJT-X. | `WsjtxColorCQ`, `WsjtxColorPOTA`, `WsjtxColorCallingMe`, `WsjtxColorDefault` |
| **WSJT-X Decodes** | Consola que muestra las transmisiones decodificadas. | — |
| **Spot Life:** | Segundos que los spots WSJT-X permanecen en el panadapter. | `WsjtxSpotLife` |

---

## SpotCollector (pestaña)

Receptor UDP para las transmisiones de Ham Radio Deluxe SpotCollector.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que SpotCollector transmite (1-65535). | `SpotCollectorPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia el receptor automáticamente al arrancar. | `SpotCollectorAutoStart` |
| **SpotCollector Spots** | Consola que muestra los spots recibidos de SpotCollector. | — |

---

## POTA (pestaña)

Consulta api.pota.app para obtener activaciones actuales.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Punto final fijo: api.pota.app (sondeo HTTP). | — |
| **Poll Interval:** | Segundos entre sondeos de POTA. | `PotaPollInterval` |
| **Start / Stop** | Inicia o detiene el sondeo. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia el sondeo de POTA automáticamente al arrancar. | `PotaAutoStart` |
| **POTA Activations** | Consola que muestra la fuente de activaciones. | — |
| **Spot Color:** | Selector de color para spots POTA. | `PotaSpotColor` |

---

## FreeDV (pestaña)

Fuente WebSocket de spots del reportador QSO de FreeDV.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Punto final fijo: qso.freedv.org (WebSocket). | — |
| **Start / Stop** | Conecta o desconecta el WebSocket. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia FreeDV automáticamente al arrancar. | `FreeDvAutoStart` |
| **FreeDV Spots** | Consola que muestra la actividad de FreeDV. | — |
| **Spot Color:** | Selector de color para spots FreeDV. | `FreeDvSpotColor` |

---

## N1MM (pestaña)

Receptor UDP para transmisiones de spots de N1MM Logger+.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que N1MM Logger+ transmite (1-65535). | `N1MMPort` |
| **Start / Stop** | Inicia o detiene el receptor UDP. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia el receptor automáticamente al arrancar. | `N1MMAutoStart` |
| **N1MM Spots** | Consola que muestra los spots recibidos de N1MM. | — |

---

## Spot List (pestaña)

Tabla unificada y buscable de todos los spots activos de todas las fuentes.

Las casillas de verificación de filtro de banda utilizan un diseño de flujo que se ajusta a una nueva fila cuando el espacio horizontal se agota, en lugar de comprimir las etiquetas. Esto mantiene el estado marcado legible incluso cuando el diálogo SpotHub es estrecho.

| Control | Descripción |
|---|---|
| **Bands:** | Casillas de verificación por banda para alternar la visibilidad. Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). |
| **Clear** | Vacía la lista de spots actual. |
| **Spot table** | Tabla ordenable con columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. Haga doble clic en una fila para sintonizar esa frecuencia. Haga clic en cualquier encabezado de columna para ordenar por esa columna; haga clic en Time para volver al orden más reciente primero. |

### Mostrar y ocultar columnas de la tabla

Haga clic derecho en cualquier encabezado de columna de la tabla de spots para abrir un menú contextual. Cada nombre de columna aparece como un elemento de menú marcable. El menú permanece abierto mientras alterna varias columnas, de modo que puede mostrar u ocultar varias columnas de una sola vez sin tener que reabrir el menú para cada columna.

1. Haga clic derecho en un encabezado de columna de la tabla de spots.
2. Marque o desmarque cualquier nombre de columna para mostrarla u ocultarla.
3. Haga clic fuera del menú o presione Escape para cerrarlo.

---

## Display (pestaña)

Controla cómo aparecen los spots y marcadores en el panadapter. Esta pestaña combina la configuración de visualización de spots, la coloración DXCC y los ajustes de Signal History.

### Fila superior de alternancias

| Control | Predeterminado | Descripción | Clave de configuración |
|---|---|---|---|
| **Spots:** | Habilitado | Alternancia principal para la superposición de spots DX. | `IsSpotsEnabled` |
| **Memories:** | Deshabilitado | Alterna la superposición de canales de memoria en el panadapter. | `IsMemorySpotsEnabled` |
| **Auto:** | Habilitado | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (p. ej., CW, FT8, RTTY). | `SpotAutoSwitchMode` |
| **Signals** (Signal History) | Deshabilitado | Marcadores dorados para señales detectadas de ancho de voz en el panadapter. Misma alternancia que **View > Signal History Markers**. | `SHistoryMarkersEnabled` |
| **QRM** (Signal History) | Deshabilitado | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Misma alternancia que **View > QRM History Markers**. | `SHistoryQrmEnabled` |
| **Clear All** | — | Borra todos los spots DX, la fuente de memoria, los marcadores de Signal History y los marcadores QRM del espectro. | — |

### Controles deslizantes de apariencia de spots

| Control | Predeterminado | Rango válido | Descripción | Clave de configuración |
|---|---|---|---|---|
| **Levels:** | 3 | 1-10 | Número de filas de apilamiento vertical para spots. | `SpotsMaxLevel` |
| **Position:** | 50 | 0-100 | Posición vertical en el panadapter. | `SpotsStartingHeightPercentage` |
| **Font Size:** | 16 | 8-32 | Tamaño del texto de los spots. | `SpotFontSize` |
| **Spot Lifetime:** | — | 10 seg – 24 horas (pasos no lineales) | Segundos antes de que un spot se desvanezca. | `DxClusterSpotLifetimeSec` |

### Colores de anulación

| Control | Predeterminado | Descripción | Clave de configuración |
|---|---|---|---|
| **Override Colors:** | Deshabilitado | Fuerza un único color de texto para todos los spots. La etiqueta del botón es estática y siempre muestra "Enabled" cuando está marcada. | `IsSpotsOverrideColorsEnabled` |
| **Selector de color de texto de spots** | `#FFFF00` | Abre un selector de color para el color del texto de los spots. | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilitado | Habilita un color de fondo personalizado para los spots. | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Habilitado | Selecciona automáticamente el color de fondo para contraste. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| **Selector de color de fondo de spots** | `#000000` | Abre un selector de color para el color de fondo de los spots. | `SpotsOverrideBgColor` |
| **Background Opacity:** | 48 | 0-100 | Opacidad del color de fondo de los spots. | `SpotsBackgroundOpacity` |
| **Spot Lines:** | Habilitado | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Deshabilite durante concursos para reducir el desorden visual. La etiqueta del botón es estática y siempre muestra "Enabled" cuando está marcada. | `IsSpotsLinesEnabled` |

### Indicador Total Spots

Conteo en vivo de los spots actualmente rastreados en todas las fuentes.

### DXCC Coloring (sección)

Colorea los spots según el estado DXCC trabajado/confirmado/necesario utilizando un registro ADIF importado.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **DXCC Colors:** | Habilita la coloración de spots basada en DXCC. La etiqueta del botón es estática y siempre muestra "Enabled" cuando está marcada. | `IsDxccColoringEnabled` |
| **Log File (ADIF):** | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Vigila automáticamente el archivo para detectar cambios después de la selección. | `DxccAdifFilePath` |
| **Imported: (estadísticas DXCC)** | Muestra el conteo de QSO y el conteo de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`. | — |
| **Muestras de color New DXCC / New Band / New Mode / Worked** | Abre un selector de color para cada categoría de estado DXCC. | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` |

### Signal History (sección)

Controles para el comportamiento y la apariencia de los marcadores de Signal History.

| Control | Predeterminado | Rango válido | Descripción | Clave de configuración |
|---|---|---|---|---|
| **Marker Lifetime:** | 60 | 15-300 seg | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado. | `SHistoryLifetimeS` |
| **QRM Gate:** | 6 | 3-30 seg | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM. | `SHistoryQrmGateS` |
| **Edge Threshold:** | 3.0 | 1.0-10.0 dB | Umbral por encima del nivel de ruido para la caminata de borde de pendiente que refina el borde del lado de la portadora de S-History. Los valores más bajos acercan el marcador a la portadora. | `SHistorySoftEdgeDb` |
| **Muestra de color Signals** | `#FFC800` (dorado) | Cualquier QColor | Color para los marcadores de señales de voz. | `SHistoryColorSignals` |
| **Muestra de color QRM** | `#FF0000` (rojo) | Cualquier QColor | Color para los marcadores QRM. | `SHistoryColorQrm` |
| **Snap to Step:** | Deshabilitado | — | Redondea el clic-para-sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. La etiqueta del botón
