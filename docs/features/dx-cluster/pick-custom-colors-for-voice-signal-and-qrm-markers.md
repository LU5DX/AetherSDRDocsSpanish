# SpotHub

El diálogo SpotHub es el centro de control para conectar fuentes de spots de DX, incluyendo un cluster DX tradicional, la Red Inversa de Balizas (RBN), WSJT-X, SpotCollector, POTA y FreeDV. También proporciona controles completos para cómo aparecen los spots en el panadapter, incluyendo marcadores de Historial de Señales y coloreado por DXCC.

## Abrir SpotHub

1. Haga clic en **Settings** > **SpotHub...**.

El diálogo contiene pestañas para cada fuente de spots y una pestaña unificada Display para personalización visual.

---

## Cluster (pestaña)

Se conecta a un cluster DX tradicional mediante telnet.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre del host del cluster DX. | `ClusterHost` |
| **Port:** | Puerto telnet (1-65535). | `ClusterPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado al cluster. | `ClusterCallsign` |
| **Connect / Disconnect** | Conecta o desconecta la conexión telnet. | — |
| **Auto-connect on startup** | Cuando está habilitado, se conecta automáticamente al inicio. | `ClusterAutoConnect` |
| **Startup Commands...** | Abre el editor de comandos de inicio. Los comandos ingresados aquí (uno por línea) se envían automáticamente después de cada inicio de sesión. Los comandos compatibles incluyen `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`, etc. | `DxClusterStartupCommands` |
| **Cluster Console** | Consola telnet de solo lectura que muestra el tráfico bruto del cluster. | — |
| **Send** | Envía un comando escrito al cluster. | — |
| **Spot Color:** | Abre un selector de color para los spots del cluster en el panadapter. | `ClusterSpotColor` |

---

## RBN (pestaña)

Fuente telnet de la Red Inversa de Balizas con limitación de tasa.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre del host telnet de RBN. | `RbnHost` |
| **Port:** | Puerto telnet de RBN (1-65535). | `RbnPort` |
| **Callsign:** | Indicativo de inicio de sesión para RBN. | `RbnCallsign` |
| **Rate Limit:** | Limita la cantidad de spots de RBN por segundo. | `RbnRateLimit` |
| **Connect / Disconnect** | Conecta o desconecta la conexión RBN. | — |
| **Auto-connect on startup** | Cuando está habilitado, inicia RBN automáticamente al inicio. | `RbnAutoConnect` |
| **Startup Commands...** | Abre el editor de comandos de inicio para comandos específicos de RBN (independiente de la pestaña DX Cluster). Los comandos se envían después de cada inicio de sesión. | `RbnStartupCommands` |
| **RBN Console** | Consola de solo lectura del tráfico de RBN. | — |
| **Send** | Envía un comando a RBN. | — |
| **Spot Color:** | Selector de color para los spots de RBN. | `RbnSpotColor` |

---

## WSJT-X (pestaña)

Escucha UDP para decodificaciones de WSJT-X con filtrado y personalización de colores.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Address:** | Dirección de enlace UDP para mensajes de WSJT-X. | `WsjtxAddress` |
| **Port:** | Puerto UDP para WSJT-X (1-65535). | `WsjtxPort` |
| **Start / Stop** | Inicia o detiene el escucha UDP. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia el escucha automáticamente al inicio. | `WsjtxAutoStart` |
| **CQ** | Muestra solo llamadas CQ. | `WsjtxFilterCQ` |
| **CQ POTA** | Muestra llamadas CQ POTA. | `WsjtxFilterPOTA` |
| **Calling Me** | Muestra solo decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` |
| **Spot Color: (CQ / POTA / Calling Me / Default)** | Selectores de color para cada categoría de spot de WSJT-X. | `WsjtxColorCQ`, `WsjtxColorPOTA`, `WsjtxColorCallingMe`, `WsjtxColorDefault` |
| **WSJT-X Decodes** | Consola que muestra las transmisiones decodificadas. | — |
| **Spot Life:** | Segundos que los spots de WSJT-X permanecen en el panadapter. | `WsjtxSpotLife` |

---

## SpotCollector (pestaña)

Escucha UDP para transmisiones de Ham Radio Deluxe SpotCollector.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **UDP Port:** | Puerto UDP en el que SpotCollector transmite (1-65535). | `SpotCollectorPort` |
| **Start / Stop** | Inicia o detiene el escucha UDP. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia el escucha automáticamente al inicio. | `SpotCollectorAutoStart` |
| **SpotCollector Spots** | Consola que muestra los spots recibidos de SpotCollector. | — |

---

## POTA (pestaña)

Consulta api.pota.app para activaciones actuales.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Punto final fijo: api.pota.app (consulta HTTP). | — |
| **Poll Interval:** | Segundos entre consultas de POTA. | `PotaPollInterval` |
| **Start / Stop** | Inicia o detiene la consulta. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia la consulta de POTA automáticamente al inicio. | `PotaAutoStart` |
| **POTA Activations** | Consola que muestra el flujo de activaciones. | — |
| **Spot Color:** | Selector de color para los spots de POTA. | `PotaSpotColor` |

---

## FreeDV (pestaña)

Flujo WebSocket de spots del reportador de QSO de FreeDV.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Punto final fijo: qso.freedv.org (WebSocket). | — |
| **Start / Stop** | Conecta o desconecta el WebSocket. | — |
| **Auto-start on startup** | Cuando está habilitado, inicia FreeDV automáticamente al inicio. | `FreeDvAutoStart` |
| **FreeDV Spots** | Consola que muestra la actividad de FreeDV. | — |
| **Spot Color:** | Selector de color para los spots de FreeDV. | `FreeDvSpotColor` |

---

## Spot List (pestaña)

Tabla unificada y buscable de todos los spots activos de todas las fuentes.

Las casillas de verificación de filtro por banda utilizan un diseño de flujo que pasa a una nueva fila cuando se agota el espacio horizontal, en lugar de comprimir las etiquetas. Esto mantiene legible el estado marcado incluso cuando el diálogo SpotHub es estrecho.

| Control | Descripción |
|---|---|
| **Bands:** | Casillas de verificación por banda para alternar la visibilidad. Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). |
| **Clear** | Vacía la lista de spots actual. |
| **Spot table** | Tabla ordenable con columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. Haga doble clic en una fila para sintonizar esa frecuencia. |

### Mostrar y ocultar columnas de la tabla

Haga clic derecho en cualquier encabezado de columna de la tabla de spots para abrir un menú contextual. Cada nombre de columna aparece como un elemento de menú seleccionable. El menú permanece abierto mientras alterna varias columnas, por lo que puede mostrar u ocultar varias columnas en una sola pasada en lugar de volver a abrir el menú para cada columna.

1. Haga clic derecho en un encabezado de columna de la tabla de spots.
2. Marque o desmarque cualquier nombre de columna para mostrarla u ocultarla.
3. Haga clic fuera del menú o presione Escape para cerrarlo.

---

## Display (pestaña)

Controla cómo aparecen los spots y marcadores en el panadapter. Esta pestaña combina ajustes de visualización de spots, coloreado por DXCC y parámetros del Historial de Señales.

### Fila superior de alternancia

| Control | Valor predeterminado | Descripción | Clave de configuración |
|---|---|---|---|
| **Spots:** | Habilitado | Alternancia maestra para la superposición de spots DX. | `IsSpotsEnabled` |
| **Memories:** | Deshabilitado | Alterna la superposición de canales de memoria en el panadapter. | `IsMemorySpotsEnabled` |
| **Auto:** | Habilitado | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (ej. CW, FT8, RTTY). | `SpotAutoSwitchMode` |
| **Signals** (Signal History) | Deshabilitado | Marcadores dorados para señales detectadas de ancho de voz en el panadapter. Misma alternancia que **View > Signal History Markers**. | `SHistoryMarkersEnabled` |
| **QRM** (Signal History) | Deshabilitado | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Misma alternancia que **View > QRM History Markers**. | `SHistoryQrmEnabled` |
| **Clear All** | — | Limpia todos los spots DX, el flujo de memoria, los marcadores de Historial de Señales y los marcadores de QRM del espectro. | — |

### Deslizadores de apariencia de spots

| Control | Valor predeterminado | Rango válido | Descripción | Clave de configuración |
|---|---|---|---|---|
| **Levels:** | 3 | 1-10 | Número de filas de apilamiento vertical para los spots. | `SpotsMaxLevel` |
| **Position:** | 50 | 0-100 | Posición vertical en el panadapter. | `SpotsStartingHeightPercentage` |
| **Font Size:** | 16 | 8-32 | Tamaño del texto de los spots. | `SpotFontSize` |
| **Spot Lifetime:** | — | 10 seg – 24 hrs (pasos no lineales) | Segundos antes de que un spot se desvanezca. | `DxClusterSpotLifetimeSec` |

### Colores de anulación

| Control | Valor predeterminado | Descripción | Clave de configuración |
|---|---|---|---|
| **Override Colors:** | Deshabilitado | Fuerza un solo color de texto para todos los spots. La etiqueta del botón es estática y siempre muestra "Enabled" cuando está marcado. | `IsSpotsOverrideColorsEnabled` |
| **Spot text color picker** | `#FFFF00` | Abre el selector de color para el color del texto de los spots. | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilitado | Habilita el color de fondo personalizado de los spots. | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Habilitado | Selecciona automáticamente el color de fondo para contraste. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| **Spot background color picker** | `#000000` | Abre el selector de color para el color de fondo de los spots. | `SpotsOverrideBgColor` |
| **Background Opacity:** | 48 | 0-100 | Opacidad del color de fondo de los spots. | `SpotsBackgroundOpacity` |
| **Spot Lines:** | Habilitado | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Deshabilítelo durante concursos para reducir el desorden visual. La etiqueta del botón es estática y siempre muestra "Enabled" cuando está marcado. | `IsSpotsLinesEnabled` |

### Indicador Total Spots

Conteo en vivo de los spots actualmente rastreados en todas las fuentes.

### DXCC Coloring (sección)

Colorea los spots según el estado de DXCC trabajado/confirmado/necesitado utilizando un registro ADIF importado.

| Control | Descripción | Clave de configuración |
|---|---|---|
| **DXCC Colors:** | Habilita el coloreado de spots basado en DXCC. La etiqueta del botón es estática y siempre muestra "Enabled" cuando está marcado. | `IsDxccColoringEnabled` |
| **Log File (ADIF):** | Carga un archivo de registro ADIF para impulsar el coloreado por DXCC. Vigila automáticamente el archivo en busca de cambios después de la selección. | `DxccAdifFilePath` |
| **Imported: (DXCC stats)** | Muestra el conteo de QSO y el conteo de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`. | — |
| **New DXCC / New Band / New Mode / Worked** color swatches | Abre un selector de color para cada categoría de estado DXCC. | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` |

### Signal History (sección)

Controles para el comportamiento y la apariencia de los marcadores de Historial de Señales.

| Control | Valor predeterminado | Rango válido | Descripción | Clave de configuración |
|---|---|---|---|---|
| **Marker Lifetime:** | 60 | 15-300 seg | Cuánto tiempo persiste un marcador de Historial de Señales inactivo antes de ser eliminado. | `SHistoryLifetimeS` |
| **QRM Gate:** | 6 | 3-30 seg | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de ser clasificada como QRM. | `SHistoryQrmGateS` |
| **Edge Threshold:** | 3.0 | 1.0-10.0 dB | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde lateral de la portadora de S-History. Valores más bajos acercan el marcador a la portadora. | `SHistorySoftEdgeDb` |
| **Signals** color swatch | `#FFC800` (dorado) | Cualquier QColor | Color para los marcadores de señales de voz. | `SHistoryColorSignals` |
| **QRM** color swatch | `#FF0000` (rojo) | Cualquier QColor | Color para los marcadores de QRM. | `SHistoryColorQrm` |
| **Snap to Step:** | Deshabilitado | — | Redondea el clic-para-sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. La etiqueta del botón es estática y siempre muestra "Enabled" cuando está marcado. | `SHistorySnapToStep` |

> **Nota:** En v26.6.3, varios botones de alternancia se actualizaron para mostrar una etiqueta estática (siempre "Enabled") cuando están en estado marcado, en lugar de cambiar dinámicamente entre "Enabled" y "Disabled". Esto afecta a: **Override Colors:**, **Spot Lines:**, **DXCC Colors:** y **Snap to Step:**. La apariencia visual del botón (presionado/suelto) aún indica el estado actual.

---

## Editor de Comandos de Inicio

Las pestañas **Cluster** y **RBN** tienen cada una un botón **Startup Commands...** que abre un diálogo para editar los comandos enviados automáticamente
