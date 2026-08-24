# SpotHub

El **SpotHub** es el centro central para conectarse a fuentes de spots de DX (DX cluster, Reverse Beacon Network, WSJT-X, SpotCollector, POTA, FreeDV y N1MM) y para configurar cómo se muestran los spots en el panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Para cada fuente de spots, necesitará la dirección del servidor, el puerto y las credenciales de inicio de sesión correspondientes (cuando corresponda).

## Abrir SpotHub

1. Haga clic en `Settings > SpotHub...`.
2. El diálogo SpotHub se abre con ocho pestañas: **Cluster**, **RBN**, **WSJT-X**, **SpotCollector**, **POTA**, **FreeDV**, **N1MM**, **Spot List** y **Display**.

---

## Cluster (pestaña)

La pestaña **Cluster** proporciona una conexión telnet a un DX cluster tradicional.

1. En el campo **Server:**, ingrese el nombre de host del DX cluster (p. ej., `dxc.nc7j.com`).
2. En el campo **Port:**, ingrese el puerto telnet (predeterminado `7300`, rango 1–65535). Este ajuste se almacena en `ClusterPort`.
3. En el campo **Callsign:**, ingrese su indicativo de inicio de sesión. Este ajuste se almacena en `ClusterCallsign`.
4. Haga clic en **Connect** para iniciar la conexión telnet. El botón cambia a **Disconnect** mientras está conectado.
5. Active **Auto-connect on startup** para que AetherSDR se conecte automáticamente al cluster cuando se inicie la aplicación. Este ajuste se almacena en `ClusterAutoConnect`.
6. La **Cluster Console** muestra el tráfico telnet sin procesar (solo lectura).
7. Escriba un comando en el campo de texto junto a **Send** y haga clic en **Send** para enviarlo al cluster.
8. Haga clic en **Spot Color:** para abrir un selector de color y elegir el color de los spots recibidos de este cluster. Este ajuste se almacena en `ClusterSpotColor`.

## RBN (pestaña)

La pestaña **RBN** proporciona una conexión telnet a la Reverse Beacon Network con limitación de velocidad.

1. En el campo **Server:**, ingrese el nombre de host telnet de RBN (p. ej., `telnet.reversebeacon.net`).
2. En el campo **Port:**, ingrese el puerto telnet de RBN (p. ej., `7000`, rango 1–65535). Este ajuste se almacena en `RbnPort`.
3. En el campo **Callsign:**, ingrese su indicativo de inicio de sesión. Este ajuste se almacena en `RbnCallsign`.
4. En el campo **Rate Limit:**, establezca el número máximo de spots de RBN por segundo. Este ajuste se almacena en `RbnRateLimit`.
5. Haga clic en **Connect** para iniciar la conexión telnet a RBN. El botón cambia a **Disconnect** mientras está conectado.
6. Active **Auto-connect on startup** para que AetherSDR se conecte automáticamente a RBN al iniciar. Este ajuste se almacena en `RbnAutoConnect`.
7. La **RBN Console** muestra el tráfico de RBN sin procesar (solo lectura).
8. Escriba un comando y haga clic en **Send** para enviarlo a RBN.
9. Haga clic en **Spot Color:** para abrir un selector de color para los spots de RBN. Este ajuste se almacena en `RbnSpotColor`.

## WSJT-X (pestaña)

La pestaña **WSJT-X** escucha decodificaciones UDP de WSJT-X.

1. En el campo **Address:**, ingrese la dirección de enlace UDP para los mensajes de WSJT-X. Este ajuste se almacena en `WsjtxAddress`.
2. En el campo **Port:**, ingrese el puerto UDP (rango 1–65535). Este ajuste se almacena en `WsjtxPort`.
3. Haga clic en **Start** para comenzar a escuchar mensajes UDP de WSJT-X. El botón cambia a **Stop** mientras está escuchando.
4. Active **Auto-start on startup** para que el listener se inicie automáticamente al abrir la aplicación. Este ajuste se almacena en `WsjtxAutoStart`.
5. Use la casilla **CQ** para mostrar solo llamadas CQ de WSJT-X. Este ajuste se almacena en `WsjtxFilterCQ`.
6. Use la casilla **CQ POTA** para mostrar solo llamadas CQ POTA. Este ajuste se almacena en `WsjtxFilterPOTA`.
7. Use la casilla **Calling Me** para mostrar solo decodificaciones dirigidas a su indicativo. Este ajuste se almacena en `WsjtxFilterCallingMe`.
8. Haga clic en los botones de color para establecer los colores de cada categoría: **CQ color**, **POTA color**, **Calling Me color** y **Default color**. Estos se almacenan en `WsjtxColorCQ`, `WsjtxColorPOTA`, `WsjtxColorCallingMe` y `WsjtxColorDefault`.
9. La consola **WSJT-X Decodes** muestra las transmisiones decodificadas (solo lectura).
10. Use **Spot Life:** para establecer cuántos segundos permanecen los spots de WSJT-X en el panadapter. Este ajuste se almacena en `WsjtxSpotLife`.

## SpotCollector (pestaña)

La pestaña **SpotCollector** escucha las transmisiones UDP de Ham Radio Deluxe SpotCollector.

1. En el campo **UDP Port:**, ingrese el puerto en el que SpotCollector transmite (rango 1–65535). Este ajuste se almacena en `SpotCollectorPort`.
2. Haga clic en **Start** para comenzar a escuchar. El botón cambia a **Stop** mientras está escuchando.
3. Active **Auto-start on startup** para que el listener se inicie automáticamente al abrir la aplicación. Este ajuste se almacena en `SpotCollectorAutoStart`.
4. La consola **SpotCollector Spots** muestra los spots recibidos (solo lectura).

## POTA (pestaña)

La pestaña **POTA** consulta `api.pota.app` para obtener las activaciones actuales de Parks On The Air.

1. El indicador **Server:** muestra el endpoint fijo `api.pota.app (HTTP polling)`.
2. Establezca el **Poll Interval:** en segundos entre consultas a POTA. Este ajuste se almacena en `PotaPollInterval`.
3. Haga clic en **Start** para comenzar la consulta. El botón cambia a **Stop** mientras está consultando.
4. Active **Auto-start on startup** para que la consulta se inicie automáticamente al abrir la aplicación. Este ajuste se almacena en `PotaAutoStart`.
5. La consola **POTA Activations** muestra el flujo de activaciones (solo lectura).
6. Haga clic en **Spot Color:** para abrir un selector de color para los spots de POTA. Este ajuste se almacena en `PotaSpotColor`.

## FreeDV (pestaña)

La pestaña **FreeDV** se conecta mediante WebSocket al reportero de QSO de FreeDV (restringido por compilación mediante `HAVE_WEBSOCKETS`).

1. El indicador **Server:** muestra el endpoint fijo `qso.freedv.org (WebSocket)`.
2. Haga clic en **Start** para conectar el WebSocket. El botón cambia a **Stop** mientras está conectado.
3. Active **Auto-start on startup** para que la conexión se inicie automáticamente al abrir la aplicación. Este ajuste se almacena en `FreeDvAutoStart`.
4. La consola **FreeDV Spots** muestra la actividad de FreeDV (solo lectura).
5. Haga clic en **Spot Color:** para abrir un selector de color para los spots de FreeDV. Este ajuste se almacena en `FreeDvSpotColor`.

## N1MM (pestaña)

La pestaña **N1MM** escucha las transmisiones UDP de spots de N1MM Logger+.

1. En el campo **UDP Port:**, ingrese el puerto en el que N1MM Logger+ transmite spots (rango 1–65535). Este ajuste se almacena en `N1MMSpotPort`.
2. Haga clic en **Start** para comenzar a escuchar. El botón cambia a **Stop** mientras está escuchando.
3. Active **Auto-start on startup** para que el listener se inicie automáticamente al abrir la aplicación. Este ajuste se almacena en `N1MMSpotAutoStart`.
4. La consola **N1MM Spots** muestra los spots recibidos (solo lectura).
5. Haga clic en **Spot Color:** para abrir un selector de color para los spots de N1MM. Este ajuste se almacena en `N1MMSpotColor`.
6. En el campo **My Message:**, ingrese el mensaje que se enviará a N1MM cuando haga doble clic en un spot. Este ajuste se almacena en `N1MMMyMessage`.
7. Haga clic en **Start / Stop (N1MM)** para iniciar o detener el listener UDP de N1MM.
8. Active **Auto-start on startup (N1MM)** para que el listener se inicie automáticamente al abrir la aplicación. Este ajuste se almacena en `N1MMAutoStart`.

## Spot List (pestaña)

La pestaña **Spot List** proporciona una tabla unificada y buscable de todos los spots en vivo de todas las fuentes.

1. Use las casillas **Bands:** para alternar la visibilidad de los spots por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.).
2. Haga clic en **Clear** para vaciar la lista actual de spots.
3. La **Spot table** muestra los spots con las columnas: **Time**, **Freq**, **DX Call**, **Comment**, **Spotter**, **Band**, **Mode**, **Source**. Haga doble clic en una fila para sintonizar la radio a esa frecuencia.

## Display (pestaña)

La pestaña **Display** controla la visualización de spots en el panadapter, el coloreado por DXCC y los parámetros de ajuste de Signal History. La pestaña está organizada de la siguiente manera:

### Fila superior de alternancia

| Control                      | Predeterminado                                                                                                 | Comportamiento                                                                                                               |
|------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| **Spots:**                   | Habilitado                                                                                                 | Alternancia principal para la superposición de spots de DX. El botón muestra **Enabled** cuando está activo y **Disabled** cuando está inactivo.            |
| **Memories:**                | Deshabilitado                                                                                                | Alterna la superposición de canales de memoria en el panadapter. El botón muestra **Enabled** cuando está activo y **Disabled** cuando está inactivo. |
| **Auto:**                    | Habilitado                                                                                                 | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (p. ej., CW, FT8, RTTY)                      |
| **Signals (Signal History)** | Deshabilitado                                                                                                | Marcadores dorados para señales detectadas de ancho de voz en el panadapter                                                        |
| **QRM (Signal History)**     | Deshabilitado                                                                                                | Marcadores rojos para portadoras persistentes e interferencia de banda ancha                                                          |
| **Clear All**                | —                                                                                                       | Borra todos los spots de DX, el flujo de memorias, los marcadores de Signal History y los marcadores de QRM del espectro                             |

### Controles deslizantes comunes

| Control | Predeterminado | Rango | Comportamiento | Clave de ajuste |
|---------|---------|-------|----------|-------------|
| **Levels:** | 3 | 1–10 | Número de filas de apilamiento vertical para spots | `SpotsMaxLevel` |
| **Position:** | 50 | 0–100 | Posición vertical en el panadapter | `SpotsStartingHeightPercentage` |
| **Font Size:** | 16 | 8–32 | Tamaño del texto de los spots | `SpotFontSize` |
| **Spot Lifetime:** | Varía | 10 seg – 24 hrs (pasos no lineales) | Segundos antes de que un spot se desvanezca | `DxClusterSpotLifetimeSec` |

### Sección Override Colors

| Control | Predeterminado | Comportamiento | Clave de ajuste |
|---------|---------|----------|-------------|
| **Override Colors:** | Deshabilitado | Fuerza un único color de texto para todos los spots. El botón muestra **Enabled** cuando está activo y **Disabled** cuando está inactivo. | `IsSpotsOverrideColorsEnabled` |
| **Selector de color de texto de spots** | #FFFF00 | Abre QColorDialog para elegir el color del texto de los spots | `SpotsOverrideColor` |
| **Override Background:** | Habilitado | Habilita un color de fondo personalizado para los spots. El botón muestra **Enabled** cuando está activo y **Disabled** cuando está inactivo. | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Habilitado | Selecciona automáticamente el color de fondo para el contraste. El botón muestra **Auto** cuando está activo. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| **Selector de color de fondo de spots** | #000000 | Abre QColorDialog para el color de fondo de los spots | `SpotsOverrideBgColor` |
| **Background Opacity:** | 48 | 0–100 | Opacidad del color de fondo de los spots | `SpotsBackgroundOpacity` |
| **Spot Lines:** | Habilitado | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactívelas durante concursos para reducir el desorden visual. El botón muestra **Enabled** cuando está activo y **Disabled** cuando está inactivo. | `IsSpotsLinesEnabled` |
| **Clear All Spots** | — | Borra todos los spots del panadapter | (sin clave) |
| **Total Spots:** | — | Conteo en vivo de spots actualmente rastreados en todas las fuentes | (indicador) |

### DXCC Coloring (sección)

La columna izquierda debajo del divisor contiene los controles de coloreado por DXCC.

| Control | Predeterminado | Comportamiento | Clave de ajuste |
|---------|---------|----------|-------------|
| **DXCC Colors:** | Deshabilitado | Colorea los spots según el estado de DXCC trabajado/confirmado/necesario. El botón muestra **Enabled** cuando está activo y **Disabled** cuando está inactivo. | `IsDxccColoringEnabled` |
| **Log File (ADIF):** | — | Carga un archivo de registro ADIF para impulsar el coloreado por DXCC. Vigila automáticamente el archivo para detectar cambios después de la selección. | `DxccAdifFilePath` |
| **Imported: (estadísticas DXCC)** | (sin registro cargado) | Muestra el conteo de QSO y el conteo de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities` | (indicador) |
| **Muestras de color DXCC (New DXCC / New Band / New Mode / Worked)** | — | Abre un selector de color para cada categoría de estado DXCC | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` |

### Signal History (sección)

La columna derecha debajo del divisor contiene los parámetros de ajuste de Signal History.

| Control | Predeterminado | Rango | Comportamiento | Clave de ajuste |
|---------|---------|-------|----------|-------------|
| **Marker Lifetime
