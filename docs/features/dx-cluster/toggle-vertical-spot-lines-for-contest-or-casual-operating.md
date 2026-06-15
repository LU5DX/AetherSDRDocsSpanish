# SpotHub

El **SpotHub** es el concentrador central para conectarse a fuentes de spots de DX — DX cluster, Reverse Beacon Network, WSJT-X, SpotCollector, POTA y FreeDV — y configurar cómo se muestran los spots en el panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Para cada fuente de spots, necesitará la dirección del servidor, el puerto y las credenciales de inicio de sesión correspondientes (cuando aplique).

## Abrir SpotHub

1. Haga clic en `Settings > SpotHub...`.
2. Se abre el cuadro de diálogo SpotHub con siete pestañas: **Cluster**, **RBN**, **WSJT-X**, **SpotCollector**, **POTA**, **FreeDV**, **Spot List** y **Display**.

---

## Cluster (pestaña)

La pestaña **Cluster** proporciona una conexión telnet a un cluster de DX tradicional.

1. En el campo **Server:**, introduzca el nombre de host del cluster de DX (p. ej., `dxc.nc7j.com`).
2. En el campo **Port:**, introduzca el puerto telnet (por defecto `7300`, rango 1–65535). Esta configuración se almacena en `ClusterPort`.
3. En el campo **Callsign:**, introduzca su indicativo de inicio de sesión. Esta configuración se almacena en `ClusterCallsign`.
4. Haga clic en **Connect** para iniciar la conexión telnet. El botón cambia a **Disconnect** mientras está conectado.
5. Active **Auto-connect on startup** para que AetherSDR se conecte automáticamente al cluster al iniciar la aplicación. Esta configuración se almacena en `ClusterAutoConnect`.
6. La **Cluster Console** muestra el tráfico telnet sin procesar (solo lectura).
7. Escriba un comando en el campo de texto junto a **Send** y haga clic en **Send** para enviarlo al cluster.
8. Haga clic en **Spot Color:** para abrir un selector de color y elegir el color de los spots recibidos de este cluster. Esta configuración se almacena en `ClusterSpotColor`.

## RBN (pestaña)

La pestaña **RBN** proporciona una conexión telnet a la Reverse Beacon Network con limitación de velocidad.

1. En el campo **Server:**, introduzca el nombre de host telnet de RBN (p. ej., `telnet.reversebeacon.net`).
2. En el campo **Port:**, introduzca el puerto telnet de RBN (p. ej., `7000`, rango 1–65535). Esta configuración se almacena en `RbnPort`.
3. En el campo **Callsign:**, introduzca su indicativo de inicio de sesión. Esta configuración se almacena en `RbnCallsign`.
4. En el campo **Rate Limit:**, establezca el número máximo de spots de RBN por segundo. Esta configuración se almacena en `RbnRateLimit`.
5. Haga clic en **Connect** para iniciar la conexión telnet RBN. El botón cambia a **Disconnect** mientras está conectado.
6. Active **Auto-connect on startup** para que AetherSDR se conecte automáticamente a RBN al iniciar. Esta configuración se almacena en `RbnAutoConnect`.
7. La **RBN Console** muestra el tráfico RBN sin procesar (solo lectura).
8. Escriba un comando y haga clic en **Send** para enviarlo a RBN.
9. Haga clic en **Spot Color:** para abrir un selector de color para los spots de RBN. Esta configuración se almacena en `RbnSpotColor`.

## WSJT-X (pestaña)

La pestaña **WSJT-X** escucha decodificaciones UDP de WSJT-X.

1. En el campo **Address:**, introduzca la dirección de enlace UDP para los mensajes de WSJT-X. Esta configuración se almacena en `WsjtxAddress`.
2. En el campo **Port:**, introduzca el puerto UDP (rango 1–65535). Esta configuración se almacena en `WsjtxPort`.
3. Haga clic en **Start** para comenzar a escuchar mensajes UDP de WSJT-X. El botón cambia a **Stop** mientras escucha.
4. Active **Auto-start on startup** para que el receptor se inicie automáticamente al abrir la aplicación. Esta configuración se almacena en `WsjtxAutoStart`.
5. Use la casilla **CQ** para mostrar solo las llamadas CQ de WSJT-X. Esta configuración se almacena en `WsjtxFilterCQ`.
6. Use la casilla **CQ POTA** para mostrar solo las llamadas CQ POTA. Esta configuración se almacena en `WsjtxFilterPOTA`.
7. Use la casilla **Calling Me** para mostrar solo las decodificaciones dirigidas a su indicativo. Esta configuración se almacena en `WsjtxFilterCallingMe`.
8. Haga clic en los botones de color para establecer colores para cada categoría: **CQ color**, **POTA color**, **Calling Me color** y **Default color**. Estos se almacenan en `WsjtxColorCQ`, `WsjtxColorPOTA`, `WsjtxColorCallingMe` y `WsjtxColorDefault`.
9. La consola **WSJT-X Decodes** muestra las transmisiones decodificadas (solo lectura).
10. Use **Spot Life:** para establecer cuántos segundos permanecen los spots de WSJT-X en el panadapter. Esta configuración se almacena en `WsjtxSpotLife`.

## SpotCollector (pestaña)

La pestaña **SpotCollector** escucha las transmisiones UDP de Ham Radio Deluxe SpotCollector.

1. En el campo **UDP Port:**, introduzca el puerto en el que SpotCollector transmite (rango 1–65535). Esta configuración se almacena en `SpotCollectorPort`.
2. Haga clic en **Start** para comenzar a escuchar. El botón cambia a **Stop** mientras escucha.
3. Active **Auto-start on startup** para que el receptor se inicie automáticamente al abrir la aplicación. Esta configuración se almacena en `SpotCollectorAutoStart`.
4. La consola **SpotCollector Spots** muestra los spots recibidos (solo lectura).

## POTA (pestaña)

La pestaña **POTA** consulta `api.pota.app` para obtener activaciones actuales de Parks On The Air.

1. El indicador **Server:** muestra el endpoint fijo `api.pota.app (HTTP polling)`.
2. Establezca el **Poll Interval:** en segundos entre consultas POTA. Esta configuración se almacena en `PotaPollInterval`.
3. Haga clic en **Start** para comenzar la consulta. El botón cambia a **Stop** mientras consulta.
4. Active **Auto-start on startup** para que la consulta se inicie automáticamente al abrir la aplicación. Esta configuración se almacena en `PotaAutoStart`.
5. La consola **POTA Activations** muestra el flujo de activaciones (solo lectura).
6. Haga clic en **Spot Color:** para abrir un selector de color para los spots de POTA. Esta configuración se almacena en `PotaSpotColor`.

## FreeDV (pestaña)

La pestaña **FreeDV** se conecta a través de WebSocket al reportero de QSO de FreeDV (compilación condicionada por `HAVE_WEBSOCKETS`).

1. El indicador **Server:** muestra el endpoint fijo `qso.freedv.org (WebSocket)`.
2. Haga clic en **Start** para conectar el WebSocket. El botón cambia a **Stop** mientras está conectado.
3. Active **Auto-start on startup** para que la conexión se inicie automáticamente al abrir la aplicación. Esta configuración se almacena en `FreeDvAutoStart`.
4. La consola **FreeDV Spots** muestra la actividad de FreeDV (solo lectura).
5. Haga clic en **Spot Color:** para abrir un selector de color para los spots de FreeDV. Esta configuración se almacena en `FreeDvSpotColor`.

## Spot List (pestaña)

La pestaña **Spot List** proporciona una tabla de búsqueda unificada de todos los spots activos de todas las fuentes.

1. Use las casillas **Bands:** para activar o desactivar la visibilidad de los spots por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.).
2. Haga clic en **Clear** para vaciar la lista de spots actual.
3. La **Spot table** muestra spots con las columnas: **Time**, **Freq**, **DX Call**, **Comment**, **Spotter**, **Band**, **Mode**, **Source**. Haga doble clic en una fila para sintonizar la radio en esa frecuencia.

## Display (pestaña)

La pestaña **Display** controla la visualización de spots en el panadapter, la coloración por DXCC y los parámetros ajustables de Signal History. La pestaña está organizada de la siguiente manera:

### Fila superior de conmutadores

| Control | Valor por defecto | Comportamiento | Clave de configuración |
|---------|---------|----------|-------------|
| **Spots:** | Habilitado | Conmutador maestro para la superposición de spots DX | `IsSpotsEnabled` |
| **Memories:** | Deshabilitado | Activa o desactiva la superposición de canales de memoria en el panadapter | `IsMemorySpotsEnabled` |
| **Auto:** | Habilitado | Cambia automáticamente el modo de la slice al hacer clic en un spot que incluya información de modo (p. ej., CW, FT8, RTTY) | `SpotAutoSwitchMode` |
| **Signals (Signal History)** | Deshabilitado | Marcadores dorados para señales de ancho de voz detectadas en el panadapter | `SHistoryMarkersEnabled` |
| **QRM (Signal History)** | Deshabilitado | Marcadores rojos para portadoras persistentes e interferencias de banda ancha | `SHistoryQrmEnabled` |
| **Clear All** | — | Elimina todos los spots DX, el feed de memoria, los marcadores de Signal History y los marcadores de QRM del espectro | (sin clave) |

### Controles deslizantes comunes

| Control | Valor por defecto | Rango | Comportamiento | Clave de configuración |
|---------|---------|-------|----------|-------------|
| **Levels:** | 3 | 1–10 | Número de filas de apilamiento vertical para spots | `SpotsMaxLevel` |
| **Position:** | 50 | 0–100 | Posición vertical en el panadapter | `SpotsStartingHeightPercentage` |
| **Font Size:** | 16 | 8–32 | Tamaño del texto de los spots | `SpotFontSize` |
| **Spot Lifetime:** | Varía | 10 seg – 24 h (pasos no lineales) | Segundos antes de que un spot se desvanezca | `DxClusterSpotLifetimeSec` |

### Sección Override Colors

| Control | Valor por defecto | Comportamiento | Clave de configuración |
|---------|---------|----------|-------------|
| **Override Colors:** | Deshabilitado | Fuerza un solo color de texto para todos los spots. El botón siempre muestra **Enabled** cuando el conmutador está activo. | `IsSpotsOverrideColorsEnabled` |
| **Selector de color de texto de spots** | #FFFF00 | Abre QColorDialog para elegir el color del texto de los spots | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilitado | Activa el color de fondo personalizado para los spots | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Habilitado | Selecciona automáticamente el color de fondo para contraste | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| **Selector de color de fondo de spots** | #000000 | Abre QColorDialog para el color de fondo de los spots | `SpotsOverrideBgColor` |
| **Background Opacity:** | 48 | 0–100 | Opacidad del color de fondo de los spots | `SpotsBackgroundOpacity` |
| **Spot Lines:** | Habilitado | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactive durante concursos para reducir el desorden visual. El botón siempre muestra **Enabled** cuando el conmutador está activo. | `IsSpotsLinesEnabled` |
| **Total Spots:** | — | Recuento en vivo de spots actualmente rastreados de todas las fuentes | (indicador) |

### DXCC Coloring (sección)

La columna izquierda debajo del divisor contiene los controles de coloración por DXCC.

| Control | Valor por defecto | Comportamiento | Clave de configuración |
|---------|---------|----------|-------------|
| **DXCC Colors:** | Deshabilitado | Colorea los spots según el estado de DXCC trabajado/confirmado/necesitado. El botón siempre muestra **Enabled** cuando el conmutador está activo. | `IsDxccColoringEnabled` |
| **Log File (ADIF):** | — | Carga un archivo de registro ADIF para impulsar la coloración por DXCC. Vigila automáticamente el archivo por cambios después de la selección. | `DxccAdifFilePath` |
| **Imported: (estadísticas DXCC)** | (sin registro cargado) | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities` | (indicador) |
| **Muestras de color DXCC (New DXCC / New Band / New Mode / Worked)** | — | Abre un selector de color para cada categoría de estado DXCC | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` |

### Signal History (sección)

La columna derecha debajo del divisor contiene los parámetros ajustables de Signal History.

| Control | Valor por defecto | Rango | Comportamiento | Clave de configuración |
|---------|---------|-------|----------|-------------|
| **Marker Lifetime:** | 60 | 15–300 seg | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado | `SHistoryLifetimeS` |
| **QRM Gate:** | 6 | 3–30 seg | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de ser clasificada como QRM | `SHistoryQrmGateS` |
| **Edge Threshold:** | 3.0 | 1.0–10.0 dB | Umbral por encima del piso de ruido para la búsqueda de bordes de pendiente que refina el borde del lado de la portadora de S-History | `SHistorySoftEdgeDb` |
| **Muestras de color de Signal History (Signals / QRM)** | #FFC800 / #FF0000 | — | Abre un selector de color para los marcadores de señal de voz (dorados) y los marcadores de QRM (rojos) | `SHistoryColorSignals`, `SHistoryColorQrm` |
| **Snap to Step:** | Deshabilitado | — | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso de la slice activa, ocultando el pequeño desplazamiento de portadora. El botón siempre muestra **Enabled** cuando el conmutador está activo. | `SHistorySnapToStep` |

---

## Activar o desactivar líneas verticales de spots para concursos o uso casual

De forma predeterminada, AetherSDR dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot en el panadapter. Esta sección explica cómo desactivar esas líneas —útil durante concursos cuando la pantalla se satura— y cómo volver a activarlas para uso casual.

### Antes de comenzar

- Al menos una fuente de spots (DX cluster, RBN, WSJT-X, POTA, SpotCollector, o
