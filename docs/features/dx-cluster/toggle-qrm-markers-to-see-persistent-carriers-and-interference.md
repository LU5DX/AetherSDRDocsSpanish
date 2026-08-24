# SpotHub (Diálogo de DX Cluster)

El diálogo SpotHub es el centro principal para conectarse a fuentes de spots DX — DX cluster, Reverse Beacon Network, WSJT-X, SpotCollector, POTA y FreeDV — y para configurar cómo se muestran los spots en el panadapter.

## Abrir SpotHub

1. Haga clic en **Settings > SpotHub...** en el menú principal.
2. El diálogo SpotHub se abre con pestañas para cada fuente de spots y una pestaña **Display** para la configuración de visualización.

---

## Fuentes de Spots

### Cluster (Pestaña)

Conéctese a un DX cluster tradicional mediante telnet.

| Control | Clave de ajuste | Comportamiento |
|---------|-------------|----------|
| **Server:** | `ClusterHost` | Nombre de host del DX cluster al que conectarse. |
| **Port:** | `ClusterPort` | Puerto telnet del DX cluster. Rango: 1–65535. |
| **Callsign:** | `ClusterCallsign` | Indicativo de inicio de sesión enviado al cluster. |
| **Connect / Disconnect** | — | Alterna la conexión telnet al cluster. |
| **Auto-connect on startup** | `ClusterAutoConnect` | Conecta automáticamente al cluster al iniciar. |
| **Cluster Console** | — | Consola telnet de solo lectura con el tráfico crudo del cluster. |
| **Send** | — | Envía un comando escrito al cluster. |
| **Spot Color:** | `ClusterSpotColor` | Abre un selector de color para los spots del cluster. |

### RBN (Pestaña)

Conéctese a la fuente telnet de Reverse Beacon Network con limitación de velocidad.

| Control | Clave de ajuste | Comportamiento |
|---------|-------------|----------|
| **Server:** | `RbnHost` | Nombre de host telnet de RBN. |
| **Port:** | `RbnPort` | Puerto telnet de RBN. Rango: 1–65535. |
| **Callsign:** | `RbnCallsign` | Indicativo de inicio de sesión en RBN. |
| **Rate Limit:** | `RbnRateLimit` | Limita los spots RBN por segundo. |
| **Connect / Disconnect (RBN)** | — | Alterna la conexión RBN. |
| **Auto-connect on startup (RBN)** | `RbnAutoConnect` | Inicia RBN automáticamente. |
| **RBN Console** | — | Consola de solo lectura del tráfico RBN. |
| **Send (RBN)** | — | Envía un comando a RBN. |
| **Spot Color: (RBN)** | `RbnSpotColor` | Selector de color para los spots RBN. |

### WSJT-X (Pestaña)

Escuche las transmisiones UDP de WSJT-X con filtros y colores.

| Control | Clave de ajuste | Comportamiento |
|---------|-------------|----------|
| **Address:** | `WsjtxAddress` | Dirección de enlace UDP para mensajes WSJT-X. |
| **Port:** | `WsjtxPort` | Puerto UDP para WSJT-X. Rango: 1–65535. |
| **Start / Stop** | — | Inicia o detiene el listener UDP. |
| **Auto-start on startup (WSJT-X)** | `WsjtxAutoStart` | Inicia automáticamente el listener al arrancar. |
| **CQ** | `WsjtxFilterCQ` | Muestra solo llamadas CQ de WSJT-X. |
| **CQ POTA** | `WsjtxFilterPOTA` | Muestra llamadas CQ POTA. |
| **Calling Me** | `WsjtxFilterCallingMe` | Muestra solo decodificaciones dirigidas a su indicativo. |
| **CQ color** | `WsjtxColorCQ` | Selector de color para spots CQ. |
| **POTA color** | `WsjtxColorPOTA` | Selector de color para spots POTA. |
| **Calling Me color** | `WsjtxColorCallingMe` | Selector de color para spots Calling Me. |
| **Default color** | `WsjtxColorDefault` | Selector de color para otros spots WSJT-X. |
| **WSJT-X Decodes** | — | Consola de transmisiones decodificadas. |
| **Spot Life:** | `WsjtxSpotLife` | Segundos que los spots WSJT-X permanecen en el panadapter. |

### SpotCollector (Pestaña)

Escuche las transmisiones UDP de Ham Radio Deluxe SpotCollector.

| Control | Clave de ajuste | Comportamiento |
|---------|-------------|----------|
| **UDP Port:** | `SpotCollectorPort` | Puerto UDP en el que SpotCollector transmite. Rango: 1–65535. |
| **Start / Stop (SpotCollector)** | — | Inicia o detiene el listener UDP. |
| **Auto-start on startup (SpotCollector)** | `SpotCollectorAutoStart` | Inicia automáticamente el listener al arrancar. |
| **SpotCollector Spots** | — | Consola de spots SpotCollector recibidos. |

### POTA (Pestaña)

Consulte api.pota.app para obtener activaciones actuales de Parks on the Air.

| Control | Clave de ajuste | Comportamiento |
|---------|-------------|----------|
| **Server:** | — | Endpoint fijo: api.pota.app (sondeo HTTP). |
| **Poll Interval:** | `PotaPollInterval` | Segundos entre sondeos POTA. |
| **Start / Stop (POTA)** | — | Inicia o detiene el sondeo POTA. |
| **Auto-start on startup (POTA)** | `PotaAutoStart` | Inicia automáticamente POTA al arrancar. |
| **POTA Activations** | — | Consola del flujo de activaciones. |
| **Spot Color: (POTA)** | `PotaSpotColor` | Selector de color para spots POTA. |

### FreeDV (Pestaña)

Conéctese al flujo WebSocket del reportero QSO de FreeDV.

| Control | Clave de ajuste | Comportamiento |
|---------|-------------|----------|
| **Server:** | — | Endpoint fijo: qso.freedv.org (WebSocket). |
| **Start / Stop (FreeDV)** | — | Conecta o desconecta el WebSocket de FreeDV. |
| **Auto-start on startup (FreeDV)** | `FreeDvAutoStart` | Inicia automáticamente FreeDV al arrancar. |
| **FreeDV Spots** | — | Consola de actividad FreeDV. |
| **Spot Color: (FreeDV)** | `FreeDvSpotColor` | Selector de color para spots FreeDV. |

### Spot List (Pestaña)

Tabla unificada y buscable de todos los spots activos de todas las fuentes.

| Control | Comportamiento |
|---------|----------|
| **Bands:** | Las casillas de verificación por banda alternan la visibilidad en la tabla. Las casillas se organizan en un diseño de flujo que se envuelve a nuevas filas cuando el diálogo es estrecho, manteniendo las etiquetas legibles. |
| **Clear** | Vacía la lista de spots actual. |
| **Spot table** | Tabla de spots ordenable. Haga doble clic en una fila para sintonizar esa frecuencia. Columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. Haga clic derecho en la fila de encabezado para mostrar u ocultar columnas — las acciones marcables alternan la visibilidad de columnas sin cerrar el menú, permitiendo ajustar varias columnas de una sola vez. |

---

## Display (Pestaña)

Configure cómo aparecen los spots en el panadapter.

### Interruptores Principales

| Control | Clave de ajuste | Predeterminado | Comportamiento |
|---------|-------------|---------|----------|
| **Spots:** | `IsSpotsEnabled` | Habilitado | Interruptor principal para la superposición de spots DX. |
| **Memories:** | `IsMemorySpotsEnabled` | Deshabilitado | Alterna la superposición de canales de memoria en el panadapter. |
| **Auto:** | `SpotAutoSwitchMode` | Habilitado | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (p. ej., CW, FT8, RTTY). |
| **Signals (Signal History)** | `SHistoryMarkersEnabled` | Deshabilitado | Marcadores dorados para señales detectadas de ancho de voz en el panadapter. |
| **QRM (Signal History)** | `SHistoryQrmEnabled` | Deshabilitado | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. |

### Controles de Posición y Borrado

| Control | Clave de ajuste | Rango | Comportamiento |
|---------|-------------|-------|----------|
| **Clear All** | — | — | Borra todos los spots DX, el flujo de memorias, los marcadores de Signal History y los marcadores QRM del espectro. |
| **Levels:** | `SpotsMaxLevel` | 1–10 (predeterminado: 3) | Número de filas de apilamiento vertical para spots. |
| **Position:** | `SpotsStartingHeightPercentage` | 0–100 (predeterminado: 50) | Posición vertical en el panadapter. |
| **Font Size:** | `SpotFontSize` | 8–32 (predeterminado: 16) | Tamaño del texto de los spots. |
| **Spot Lifetime:** | `DxClusterSpotLifetimeSec` | 10 seg – 24 hrs | Segundos antes de que un spot se desvanezca. Pasos no lineales. |

### Anulaciones de Color

| Control | Clave de ajuste | Predeterminado | Comportamiento |
|---------|-------------|---------|----------|
| **Override Colors:** | `IsSpotsOverrideColorsEnabled` | — | Fuerza un solo color de texto para todos los spots. |
| **Spot text color picker** | `SpotsOverrideColor` | #FFFF00 | Abre el selector de color para elegir el color del texto de los spots. |
| **Override Background: Enabled** | `IsSpotsOverrideBackgroundColorsEnabled` | Habilitado | Habilita un color de fondo personalizado para los spots. |
| **Override Background: Auto** | `IsSpotsOverrideToAutoBackgroundColorEnabled` | Habilitado | Selecciona automáticamente el color de fondo para contraste. |
| **Spot background color picker** | `SpotsOverrideBgColor` | #000000 | Abre el selector de color para el color de fondo de los spots. |
| **Background Opacity:** | `SpotsBackgroundOpacity` | 0–100 (predeterminado: 48) | Opacidad del color de fondo de los spots. |
| **Spot Lines:** | `IsSpotsLinesEnabled` | Habilitado | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Deshabilítelas durante concursos para reducir el desorden visual. |

### Indicadores de Estado

| Indicador | Comportamiento |
|-----------|----------|
| **Total Spots:** | Conteo en vivo de spots actualmente rastreados en todas las fuentes. |

### Coloración DXCC (Sección)

| Control | Clave de ajuste | Comportamiento |
|---------|-------------|----------|
| **DXCC Colors:** | `IsDxccColoringEnabled` | Colorea los spots según el estado DXCC trabajado/confirmado/necesario. |
| **Log File (ADIF):** | `DxccAdifFilePath` | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Supervisa automáticamente el archivo para detectar cambios después de la selección. |
| **Imported:** | — | Muestra el conteo de QSO y el conteo de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`. |
| **New DXCC color** | `DxccColorNewEntity` | Selector de color para entidades no trabajadas. |
| **New Band color** | `DxccColorNewBand` | Selector de color para contactos en banda nueva. |
| **New Mode color** | `DxccColorNewMode` | Selector de color para contactos en modo nuevo. |
| **Worked color** | `DxccColorWorked` | Selector de color para entidades ya trabajadas. |

### Signal History (Sección)

| Control | Clave de ajuste | Predeterminado | Rango | Comportamiento |
|---------|-------------|---------|-------|----------|
| **Marker Lifetime:** | `SHistoryLifetimeS` | 60 | 15–300 s | Cuánto tiempo persiste un marcador de Signal History inactivo antes de eliminarse. Haga doble clic en la perilla para restablecer a 60 s. |
| **QRM Gate:** | `SHistoryQrmGateS` | 6 | 3–30 s | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM. Haga doble clic en la perilla para restablecer a 6 s. |
| **Edge Threshold:** | `SHistorySoftEdgeDb` | 3.0 | 1.0–10.0 dB | Umbral por encima del piso de ruido para el recorrido de borde de pendiente que refina el borde del lado de la portadora de S-History. Haga doble clic en la perilla para restablecer a 3.0 dB. |
| **Signals color** | `SHistoryColorSignals` | #FFC800 | — | Abre el selector de color para los marcadores dorados de señales de voz. |
| **QRM color** | `SHistoryColorQrm` | #FF0000 | — | Abre el selector de color para los marcadores QRM rojos. |
| **Snap to Step:** | `SHistorySnapToStep` | Deshabilitado | — | Redondea el clic-para-sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. |

---

## Retroalimentación Visual

- Las etiquetas de estado de cada fuente muestran el estado actual de la conexión: Disconnected, Connected, Stopped, Listening o Polling.
- El diálogo SpotHub usa colores conscientes del tema: color de acento cuando está conectado, color de etiqueta cuando está desconectado y color de peligro en caso de error.
- Los botones de alternancia muestran su texto predeterminado ("Enabled" o "Disabled") — el estado de alternancia se indica por el estado presionado del botón y el estilo de fondo, no por el texto de la etiqueta.

## Consejos

- Los marcadores QRM son independientes de los marcadores de voz de Signal History. Habilite uno, ambos o ninguno.
- Use el control deslizante **QRM Gate** para ignorar transmisiones breves y marcar solo señales que persisten lo suficiente como para ser interferencia.
- Haga doble clic en cualquier perilla deslizante de la sección Signal History para restablecerla instantáneamente a su valor predeterminado de fábrica.
- La pestaña **Spot List** usa un diseño de flujo para las casillas de verificación de banda, de modo que se envuelven a nuevas filas cuando el diálogo es estrecho en lugar de comprimirse.
- Haga clic derecho en el encabezado de la tabla de spots para mostrar u ocultar columnas — el menú de visibilidad de columnas permanece abierto mientras alterna varias casillas.
- Haga clic en el encabezado de la columna **Time** en la tabla de Spot List para restaurar el orden más reciente primero después de ordenar por otra columna.

## Relacionados

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm-gate-and-edge-threshold)
- [Pick custom colors for
