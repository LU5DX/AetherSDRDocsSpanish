# SpotHub

La ventana **SpotHub** es el centro central para conectarse a fuentes de spots de DX — clúster DX, Reverse Beacon Network (RBN), WSJT-X, SpotCollector, POTA y FreeDV — y configurar cómo se muestran los spots en el panadapter.

## Abrir SpotHub

Haga clic en el botón **SpotHub** en la barra de herramientas, o presione `Ctrl+Shift+S`.

## Diseño de SpotHub

La ventana SpotHub contiene una interfaz con pestañas con las siguientes pestañas:

| Pestaña | Propósito |
|---------|-----------|
| **Cluster** | Conexión telnet a un clúster DX |
| **RBN** | Reverse Beacon Network |
| **WSJT-X** | Receptor UDP de WSJT-X |
| **SpotCollector** | SpotCollector de Ham Radio Deluxe |
| **POTA** | Activaciones Parks on the Air |
| **FreeDV** | Reportero de QSO de FreeDV |
| **Spot List** | Tabla unificada y buscable de spots en vivo |
| **Display** | Visualización de spots en el panadapter, Signal History y coloreado por DXCC |

Cada pestaña de fuente proporciona controles de conexión, una vista de consola y un selector de color de spot. Los indicadores de estado de la fuente aparecen en la parte superior de la pestaña: **Disconnected**, **Connected**, **Stopped**, **Listening** o **Polling**.

## Pestaña Cluster

La pestaña Cluster se conecta a un clúster DX tradicional mediante telnet.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| **Server:** | (vacío) | nombre de host | `ClusterHost` | Nombre de host del clúster DX |
| **Port:** | 23 | 1–65535 | `ClusterPort` | Puerto Telnet |
| **Callsign:** | (vacío) | indicativo | `ClusterCallsign` | Indicativo de inicio de sesión |
| **Connect / Disconnect** | Connect | — | — | Alterna la conexión telnet |
| **Auto-connect on startup** | off | on/off | `ClusterAutoConnect` | Se conecta automáticamente al iniciar |
| **Cluster Console** | (solo lectura) | — | — | Tráfico telnet sin procesar |
| **Send** | — | — | — | Envía un comando al clúster |
| **Spot Color:** | — | color | `ClusterSpotColor` | Abre el selector de color para el texto del spot |

## Pestaña RBN

La pestaña RBN se conecta a la Reverse Beacon Network.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| **Server:** | (vacío) | nombre de host | `RbnHost` | Nombre de host de RBN |
| **Port:** | 23 | 1–65535 | `RbnPort` | Puerto telnet de RBN |
| **Callsign:** | (vacío) | indicativo | `RbnCallsign` | Indicativo de inicio de sesión |
| **Rate Limit:** | 10 | 1–100 | `RbnRateLimit` | Límite de spots por segundo |
| **Connect / Disconnect** | Connect | — | — | Alterna la conexión RBN |
| **Auto-connect on startup** | off | on/off | `RbnAutoConnect` | Se inicia automáticamente |
| **RBN Console** | (solo lectura) | — | — | Tráfico RBN sin procesar |
| **Send** | — | — | — | Envía un comando a RBN |
| **Spot Color:** | — | color | `RbnSpotColor` | Selector de color para spots de RBN |

## Pestaña WSJT-X

La pestaña WSJT-X escucha mensajes de difusión UDP de WSJT-X. El relleno y el borde del botón **Start/Stop** se vuelven verdes cuando el receptor está en ejecución.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| **Address:** | 127.0.0.1 | dirección IP | `WsjtxAddress` | Dirección de enlace UDP |
| **Port:** | 2237 | 1–65535 | `WsjtxPort` | Puerto UDP |
| **Start / Stop** | Stop | — | — | Inicia/detiene el receptor UDP |
| **Auto-start on startup** | off | on/off | `WsjtxAutoStart` | Inicia el receptor al lanzar |
| **CQ** | off | on/off | `WsjtxFilterCQ` | Muestra solo llamadas CQ |
| **CQ POTA** | off | on/off | `WsjtxFilterPOTA` | Muestra llamadas CQ POTA |
| **Calling Me** | off | on/off | `WsjtxFilterCallingMe` | Muestra solo decodificaciones dirigidas a su indicativo |
| **CQ color** | — | color | `WsjtxColorCQ` | Selector de color para spots CQ |
| **POTA color** | — | color | `WsjtxColorPOTA` | Selector de color para spots POTA |
| **Calling Me color** | — | color | `WsjtxColorCallingMe` | Selector de color para spots Calling Me |
| **Default color** | — | color | `WsjtxColorDefault` | Selector de color para spots predeterminados |
| **WSJT-X Decodes** | (solo lectura) | — | — | Consola de transmisiones decodificadas |
| **Spot Life:** | 60 | 10–3600 s | `WsjtxSpotLife` | Segundos que los spots permanecen en el panadapter |

## Pestaña SpotCollector

Se conecta a SpotCollector de Ham Radio Deluxe mediante difusión UDP.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| **UDP Port:** | 58779 | 1–65535 | `SpotCollectorPort` | Puerto UDP para difusiones |
| **Start / Stop** | Stop | — | — | Inicia/detiene el receptor |
| **Auto-start on startup** | off | on/off | `SpotCollectorAutoStart` | Inicia el receptor al lanzar |
| **SpotCollector Spots** | (solo lectura) | — | — | Consola de spots recibidos |

## Pestaña POTA

Consulta api.pota.app para obtener las activaciones actuales de Parks on the Air.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| **Server:** | api.pota.app (sondeo HTTP) | — | — | Indicador de punto final fijo |
| **Poll Interval:** | 60 | 10–3600 s | `PotaPollInterval` | Segundos entre sondeos |
| **Start / Stop** | Stop | — | — | Inicia/detiene el sondeo |
| **Auto-start on startup** | off | on/off | `PotaAutoStart` | Inicia el sondeo al lanzar |
| **POTA Activations** | (solo lectura) | — | — | Consola del feed de activaciones |
| **Spot Color:** | — | color | `PotaSpotColor` | Selector de color para spots de POTA |

## Pestaña FreeDV

Se conecta al reportero de QSO de FreeDV a través de WebSocket.

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| **Server:** | qso.freedv.org (WebSocket) | — | — | Indicador de punto final fijo |
| **Start / Stop** | Stop | — | — | Conecta/desconecta WebSocket |
| **Auto-start on startup** | off | on/off | `FreeDvAutoStart` | Inicia FreeDV al lanzar |
| **FreeDV Spots** | (solo lectura) | — | — | Consola de actividad de FreeDV |
| **Spot Color:** | — | color | `FreeDvSpotColor` | Selector de color para spots de FreeDV |

## Pestaña Spot List

Una tabla unificada y buscable de todos los spots activos de todas las fuentes.

| Control | Comportamiento |
|---------|----------------|
| **Bands:** | Casillas de verificación por banda que alternan la visibilidad en la tabla |
| **Clear** | Vacía la lista de spots actual |
| **Spot table** | Tabla ordenable. Haga doble clic en una fila para sintonizar. Columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source |

## Pestaña Display

Controla cómo aparecen los spots en el panadapter. La pestaña Display presenta controles en un diseño único con una fila superior de conmutadores, una fila común de deslizadores y una sección de dos columnas para DXCC Coloring (izquierda) y Signal History (derecha).

### Fila superior de conmutadores

| Control | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|---------------------|------------------------|----------------|
| **Spots:** | Enabled | `IsSpotsEnabled` | Conmutador principal para la superposición de spots DX |
| **Memories:** | Disabled | `IsMemorySpotsEnabled` | Superposición de canales de memoria en el panadapter |
| **Auto:** | Enabled | `SpotAutoSwitchMode` | Cambia automáticamente el modo del slice al hacer clic en un spot con información de modo |
| **Signals (Signal History)** | Disabled | `SHistoryMarkersEnabled` | Marcadores dorados para señales detectadas de ancho de voz |
| **QRM (Signal History)** | Disabled | `SHistoryQrmEnabled` | Marcadores rojos para portadoras persistentes e interferencia |

### Deslizadores comunes

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| **Levels:** | 3 | 1–10 | `SpotsMaxLevel` | Filas de apilamiento vertical para spots |
| **Position:** | 50 | 0–100 | `SpotsStartingHeightPercentage` | Posición vertical en el panadapter |
| **Font Size:** | 16 | 8–32 | `SpotFontSize` | Tamaño del texto del spot |
| **Spot Lifetime:** | 300 | 10 s – 24 h | `DxClusterSpotLifetimeSec` | Segundos antes de que el spot se desvanezca |

### Botones Clear All y de acción

| Control | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|---------------------|------------------------|----------------|
| **Clear All** | — | — | Limpia todos los spots DX, el feed de memoria, los marcadores de Signal History y los marcadores de QRM |
| **Override Colors:** | off | `IsSpotsOverrideColorsEnabled` | Fuerza un color de texto único para todos los spots |
| **Selector de color de texto de spot** | #FFFF00 | `SpotsOverrideColor` | Abre el cuadro de diálogo de color |
| **Override Background: Enabled** | Enabled | `IsSpotsOverrideBackgroundColorsEnabled` | Habilita un fondo de spot personalizado |
| **Override Background: Auto** | Enabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Selecciona automáticamente el color de fondo para contraste |
| **Selector de color de fondo de spot** | #000000 | `SpotsOverrideBgColor` | Abre el cuadro de diálogo de color |
| **Background Opacity:** | 48 | 0–100 | `SpotsBackgroundOpacity` | Opacidad del color de fondo del spot |
| **Spot Lines:** | Enabled | `IsSpotsLinesEnabled` | Líneas verticales desde el espectro hasta las etiquetas de los spots |
| **Total Spots:** | — | — | Conteo en vivo de spots de todas las fuentes |

### DXCC Coloring (Columna izquierda)

Controles en la columna izquierda debajo del encabezado de sección divisor **DXCC Coloring**:

| Control | Valor predeterminado | Clave de configuración | Comportamiento |
|---------|---------------------|------------------------|----------------|
| **DXCC Colors:** | off | `IsDxccColoringEnabled` | Colorea los spots según el estado de DXCC trabajado/confirmado/necesario |
| **Log File (ADIF):** | — | `DxccAdifFilePath` | Carga un registro ADIF para el coloreado por DXCC. Vigila automáticamente los cambios del archivo |
| **Imported:** | (no hay registro cargado) | — | Muestra el conteo de QSO y el conteo de entidades |
| **New DXCC** | — | `DxccColorNewEntity` | Selector de color para nueva entidad |
| **New Band** | — | `DxccColorNewBand` | Selector de color para nueva banda |
| **New Mode** | — | `DxccColorNewMode` | Selector de color para nuevo modo |
| **Worked** | — | `DxccColorWorked` | Selector de color para entidades trabajadas |

### Signal History (Columna derecha)

Controles en la columna derecha debajo del encabezado de sección divisor **Signal History**:

| Control | Valor predeterminado | Rango | Clave de configuración | Comportamiento |
|---------|---------------------|-------|------------------------|----------------|
| **Marker Lifetime:** | 60 | 15–300 s | `SHistoryLifetimeS` | Cuánto tiempo persiste un marcador inactivo |
| **QRM Gate:** | 6 | 3–30 s | `SHistoryQrmGateS` | Persistencia antes de clasificar como QRM |
| **Edge Threshold:** | 3.0 | 1.0–10.0 dB | `SHistorySoftEdgeDb` | Umbral para el refinamiento de bordes |
| **Señales color** | #FFC800 | color | `SHistoryColorSignals` | Selector de color para marcadores de señales de voz |
| **QRM color** | #FF0000 | color | `SHistoryColorQrm` | Selector de color para marcadores de QRM |
| **Snap to Step:** | Disabled | on/off | `SHistorySnapToStep` | Redondea la sintonización al hacer clic al tamaño de paso más cercano |

## Marcadores de Signal History

El sistema Signal History detecta y muestra dos tipos de marcadores en el espectro:

- **Marcadores de señal (dorados, #FFC800)** — Marcadores para señales detectadas de ancho de voz. Aparecen como indicadores dorados en el panadapter.
- **Marcadores de QRM (rojos, #FF0000)** — Marcadores para portadoras estrechas persistentes e interferencia de banda ancha. Aparecen como indicadores rojos.

Ambos tipos de marcadores se muestran como marcadores en el waterfall del espectro. Al hacer clic en un marcador, se sintoniza el slice activo a esa frecuencia. Al hacer doble clic en un marcador, se abre el panel VFO para esa frecuencia.

Los conmutadores **Signals (Signal History)** y **QRM (Signal History)** en la pestaña Display comparten el mismo comportamiento que los elementos de menú **View > Signal History Markers** y **View > QRM History Markers**.

Cuando **Snap to Step** está habilitado, al hacer clic en un marcador de Signal History se redondea la frecuencia de sintonización al
