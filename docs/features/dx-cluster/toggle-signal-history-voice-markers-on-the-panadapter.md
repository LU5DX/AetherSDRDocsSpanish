# SpotHub (Diálogo de DX Cluster)

## Propósito

SpotHub es la interfaz central para conectarse a fuentes de spots DX y configurar cómo se muestran los spots en el panadapter. Reúne seis fuentes de spots — DX Cluster, Reverse Beacon Network (RBN), WSJT-X, SpotCollector, POTA y FreeDV — en un solo diálogo con controles de pestañas y una lista unificada de spots.

## Abrir SpotHub

1. Abra **Settings > SpotHub...** o haga clic en el botón **SpotHub** en la barra de herramientas principal.
2. El diálogo tiene siete pestañas: **Cluster**, **RBN**, **WSJT-X**, **SpotCollector**, **POTA**, **FreeDV**, **Spot List** y **Display**.

---

## Pestaña Cluster

La pestaña **Cluster** proporciona una conexión telnet a un cluster DX tradicional.

### Configuración de conexión

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| **Server:** | (vacío) | Cualquier nombre de host o IP | `ClusterHost` |
| **Port:** | (vacío) | 1-65535 | `ClusterPort` |
| **Callsign:** | (vacío) | Cualquier indicativo de radioaficionado | `ClusterCallsign` |

### Controles de conexión

| Control | Comportamiento |
|---|---|
| **Connect / Disconnect** | Alterna la conexión telnet. |
| **Auto-connect on startup** | Si está habilitado, se conecta automáticamente cuando AetherSDR se inicia. Clave de configuración: `ClusterAutoConnect`. |

### Consola y línea de comandos

| Control | Comportamiento |
|---|---|
| **Cluster Console** | Área de texto de solo lectura que muestra el tráfico telnet en bruto. |
| **Send** (botón pulsador) | Envía el comando escrito al cluster. |

### Comandos de inicio

Haga clic en **Startup Commands…** en la pestaña Cluster para abrir un diálogo donde puede ingresar un comando por línea (por ejemplo, `SET/NAME`, `SET/QTH`, `ACCEPT/SPOT`). Estos comandos se envían automáticamente al cluster después de cada inicio de sesión. Los comandos se guardan en la configuración de la aplicación (`DxClusterStartupCommands` para la pestaña Cluster, `RbnStartupCommands` para la pestaña RBN).

### Color de spots

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Spot Color:** | Abre un selector de color para los spots del cluster. | `ClusterSpotColor` |

---

## Pestaña RBN

La pestaña **RBN** se conecta a la Reverse Beacon Network mediante telnet con limitación de velocidad.

### Configuración de conexión

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| **Server:** | (vacío) | Cualquier nombre de host o IP | `RbnHost` |
| **Port:** | (vacío) | 1-65535 | `RbnPort` |
| **Callsign:** | (vacío) | Cualquier indicativo de radioaficionado | `RbnCallsign` |
| **Rate Limit:** | (vacío) | (sin límite por defecto) | `RbnRateLimit` |

### Controles de conexión

| Control | Comportamiento |
|---|---|
| **Connect / Disconnect** | Alterna la conexión RBN. |
| **Auto-connect on startup** | Si está habilitado, se conecta automáticamente al iniciar. Clave de configuración: `RbnAutoConnect`. |

### Consola y línea de comandos

| Control | Comportamiento |
|---|---|
| **RBN Console** | Área de texto de solo lectura que muestra el tráfico RBN. |
| **Send** | Envía un comando a RBN. |

### Color de spots

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Spot Color:** | Abre un selector de color para los spots RBN. | `RbnSpotColor` |

---

## Pestaña WSJT-X

La pestaña **WSJT-X** escucha mensajes de difusión UDP de WSJT-X.

### Configuración del listener

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| **Address:** | (vacío) | Cualquier dirección IP local | `WsjtxAddress` |
| **Port:** | (vacío) | 1-65535 | `WsjtxPort` |

### Controles del listener

| Control | Comportamiento |
|---|---|
| **Start / Stop** | Inicia o detiene el listener UDP. |
| **Auto-start on startup** | Si está habilitado, inicia el listener automáticamente al iniciar. Clave de configuración: `WsjtxAutoStart`. |

### Filtros

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **CQ** | Muestra solo llamadas CQ. | `WsjtxFilterCQ` |
| **CQ POTA** | Muestra llamadas CQ POTA. | `WsjtxFilterPOTA` |
| **Calling Me** | Muestra solo decodificaciones dirigidas a su indicativo. | `WsjtxFilterCallingMe` |

### Duración de spots

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| **Spot Life:** | (vacío) | Segundos | `WsjtxSpotLife` |

### Colores de spots

| Control | Clave de configuración |
|---|---|
| **CQ color** | `WsjtxColorCQ` |
| **POTA color** | `WsjtxColorPOTA` |
| **Calling Me color** | `WsjtxColorCallingMe` |
| **Default color** | `WsjtxColorDefault` |

### Consola

| Control | Comportamiento |
|---|---|
| **WSJT-X Decodes** | Consola de transmisiones decodificadas. |

---

## Pestaña SpotCollector

La pestaña **SpotCollector** escucha mensajes de difusión UDP de Ham Radio Deluxe SpotCollector.

### Configuración del listener

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| **UDP Port:** | (vacío) | 1-65535 | `SpotCollectorPort` |

### Controles del listener

| Control | Comportamiento |
|---|---|
| **Start / Stop** | Inicia o detiene el listener UDP. |
| **Auto-start on startup** | Si está habilitado, inicia el listener automáticamente al iniciar. Clave de configuración: `SpotCollectorAutoStart`. |

### Consola

| Control | Comportamiento |
|---|---|
| **SpotCollector Spots** | Consola de los spots recibidos de SpotCollector. |

---

## Pestaña POTA

La pestaña **POTA** consulta api.pota.app para obtener activaciones actuales de Parks on the Air.

### Configuración de sondeo

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| **Server:** | api.pota.app (sondeo HTTP) | Punto final fijo (solo indicador) | — |
| **Poll Interval:** | (vacío) | Segundos entre sondeos | `PotaPollInterval` |

### Controles de sondeo

| Control | Comportamiento |
|---|---|
| **Start / Stop** | Inicia o detiene el sondeo de POTA. |
| **Auto-start on startup** | Si está habilitado, inicia el sondeo automáticamente al iniciar. Clave de configuración: `PotaAutoStart`. |

### Consola

| Control | Comportamiento |
|---|---|
| **POTA Activations** | Consola del flujo de activaciones. |

### Color de spots

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Spot Color:** | Abre un selector de color para los spots POTA. | `PotaSpotColor` |

---

## Pestaña FreeDV

La pestaña **FreeDV** se conecta al flujo WebSocket de qso.freedv.org para spots del reportero de QSO FreeDV. Esta pestaña solo está disponible cuando AetherSDR se compila con soporte WebSocket (`HAVE_WEBSOCKETS`).

### Configuración de conexión

| Control | Predeterminado | Clave de configuración |
|---|---|---|
| **Server:** | qso.freedv.org (WebSocket) | Punto final fijo (solo indicador) |

### Controles de conexión

| Control | Comportamiento |
|---|---|
| **Start / Stop** | Conecta o desconecta el WebSocket de FreeDV. |
| **Auto-start on startup** | Si está habilitado, se conecta automáticamente al iniciar. Clave de configuración: `FreeDvAutoStart`. |

### Consola

| Control | Comportamiento |
|---|---|
| **FreeDV Spots** | Consola de actividad de FreeDV. |

### Color de spots

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **Spot Color:** | Abre un selector de color para los spots FreeDV. | `FreeDvSpotColor` |

---

## Pestaña Spot List

La pestaña **Spot List** muestra una tabla unificada y buscable de todos los spots en vivo de todas las fuentes activas.

### Filtros de banda

| Control | Comportamiento |
|---|---|
| **Bands:** | Las casillas de verificación por banda alternan la visibilidad en la tabla. Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). Las casillas usan un diseño de flujo que se ajusta a una nueva fila cuando el diálogo es demasiado estrecho para todas las bandas en una sola línea. |

### Controles de tabla

| Control | Comportamiento |
|---|---|
| **Clear** | Vacía la lista de spots actual. |
| **Spot table** | Tabla ordenable de spots. Haga doble clic en una fila para sintonizar su slice activo a esa frecuencia. Columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. |

### Visibilidad de columnas

Haga clic derecho en cualquier encabezado de columna en la tabla de spots para mostrar u ocultar columnas. El menú permanece abierto mientras alterna múltiples columnas marcables, lo que le permite mostrar u ocultar varias columnas de una sola vez sin que el menú se cierre después de cada alternancia.

#### Ordenamiento

Haga clic en cualquier encabezado de columna para ordenar por esa columna. La columna **Time** es ordenable, por lo que siempre puede volver al orden de más reciente a más antiguo después de ordenar por otras columnas.

---

## Pestaña Display

La pestaña **Display** controla cómo aparecen los spots en el panadapter, la configuración de marcadores de Signal History y el coloreado DXCC.

### Conmutadores principales

| Control | Predeterminado | Clave de configuración |
|---|---|---|
| **Spots:** | Habilitado | `IsSpotsEnabled` |
| **Memories:** | Deshabilitado | `IsMemorySpotsEnabled` |
| **Auto:** | Habilitado | `SpotAutoSwitchMode` |

- **Spots:** Conmutador principal para la superposición de spots DX en el panadapter.
- **Memories:** Alterna la superposición de canales de memoria en el panadapter.
- **Auto:** Cuando está habilitado y un spot incluye información de modo (por ejemplo, CW, FT8, RTTY), al hacer clic en el spot se cambia automáticamente el slice activo a ese modo.

### Conmutadores de Signal History

| Control | Predeterminado | Clave de configuración |
|---|---|---|
| **Signals** (etiquetado "Signal History") | Deshabilitado | `SHistoryMarkersEnabled` |
| **QRM** (etiquetado "QRM History") | Deshabilitado | `SHistoryQrmEnabled` |

- **Signals:** Marcadores dorados en el panadapter para señales detectadas de ancho de voz. Este conmutador también puede activarse desde **View > Signal History Markers**.
- **QRM:** Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Este conmutador también puede activarse desde **View > QRM History Markers**.

### Limpiar todo

| Control | Comportamiento |
|---|---|
| **Clear All** | Limpia todos los spots DX, el flujo de memoria, los marcadores de Signal History y los marcadores QRM del espectro. |

### Controles deslizantes de visualización de spots

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| **Levels:** | 3 | 1-10 | `SpotsMaxLevel` |
| **Position:** | 50 | 0-100 | `SpotsStartingHeightPercentage` |
| **Font Size:** | 16 | 8-32 | `SpotFontSize` |
| **Spot Lifetime:** | (varía) | 10 seg – 24 hrs (pasos no lineales) | `DxClusterSpotLifetimeSec` |

- **Levels:** Número de filas de apilamiento vertical para los spots.
- **Position:** Posición vertical de los spots en el panadapter.
- **Font Size:** Tamaño del texto de los spots.
- **Spot Lifetime:** Cuánto tiempo permanece visible un spot antes de desvanecerse.

### Controles de anulación de color

| Control | Predeterminado | Clave de configuración |
|---|---|---|
| **Override Colors:** | Off | `IsSpotsOverrideColorsEnabled` |
| **Spot text color picker** | #FFFF00 | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilitado | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Habilitado | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| **Spot background color picker** | #000000 | `SpotsOverrideBgColor` |
| **Background Opacity:** | 48 | 0-100 | `SpotsBackgroundOpacity` |

- **Override Colors:** Cuando está habilitado, fuerza un solo color de texto para todos los spots.
- **Override Background: Enabled:** Cuando está habilitado, permite un color de fondo personalizado para los spots.
- **Override Background: Auto:** Cuando está habilitado, selecciona automáticamente el color de fondo para el contraste.

### Líneas de spots

| Control | Predeterminado | Clave de configuración |
|---|---|---|
| **Spot Lines:** | Habilitado | `IsSpotsLinesEnabled` |

Cuando está habilitado, dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Deshabilítelo durante concursos para reducir el desorden visual.

### Total de spots

| Control | Comportamiento |
|---|---|
| **Total Spots:** | Conteo en vivo de los spots actualmente rastreados en todas las fuentes. |

---

### Sección de coloreado DXCC

Controles para colorear spots según el estado de trabajado/confirmado/necesario de DXCC.

| Control | Predeterminado | Clave de configuración |
|---|---|---|
| **DXCC Colors:** | Off | `IsDxccColoringEnabled` |
| **Log File (ADIF):** | (sin archivo) | `DxccAdifFilePath` |
| **Imported:** | (sin registro cargado) | — (indicador) |

- **DXCC Colors:** Cuando está habilitado, colorea los spots según el estado de DXCC trabajado/confirmado/necesario.
- **Log File (ADIF):** Haga clic para cargar un archivo de registro ADIF. AetherSDR vigila automáticamente el archivo para detectar cambios y lo recarga cuando se detectan modificaciones.
- **Imported:** Muestra el conteo de QSO y el conteo de entidades del registro cargado. Formato: `<N> QSOs / <M> entities`.

#### Muestras de color DXCC

| Control | Clave de configuración |
|---|---|
| **New
