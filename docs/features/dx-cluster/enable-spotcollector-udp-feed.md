# SpotHub

El diálogo SpotHub es el centro central para conectarse a fuentes de spots de DX: cluster de DX, Reverse Beacon Network, WSJT-X, SpotCollector, POTA y FreeDV, así como para configurar cómo se muestran los spots en el panadapter.

## Abrir SpotHub

1. Abra `Settings > SpotHub...`.

## Resumen de SpotHub

El diálogo SpotHub contiene múltiples pestañas, cada una dedicada a una fuente de spots diferente, además de una pestaña **Display** para la apariencia del panadapter.

## Pestaña Cluster

Se conecta a un cluster de DX tradicional mediante telnet.

1. Haga clic en la pestaña **Cluster**.
2. Ingrese el nombre del host del cluster en **Server:**. Este valor se guarda como `ClusterHost`.
3. Ingrese el puerto telnet en **Port:**. Rango válido: 1–65535. Este valor se guarda como `ClusterPort`.
4. Ingrese su indicativo en **Callsign:**. Este valor se guarda como `ClusterCallsign`.
5. Haga clic en **Connect**.
6. Confirme que el indicador de estado cambie a **Connected**. El tráfico telnet sin procesar aparece en la **Cluster Console**.
7. Para enviar un comando, escriba en el campo de línea de comandos y haga clic en **Send**.
8. Para establecer el color del spot, haga clic en **Spot Color:** y seleccione un color. Este valor se guarda como `ClusterSpotColor`.
9. Para que el cluster se conecte automáticamente cada vez que se inicie AetherSDR, active **Auto-connect on startup**. Esto se guarda como `ClusterAutoConnect`.

### Comandos de inicio para el cluster

Haga clic en **Startup Commands…** para abrir un diálogo donde puede ingresar un comando por línea. Estos comandos se envían al servidor del cluster automáticamente después de cada inicio de sesión.

Los comandos típicos incluyen:
- `SET/NAME` — establece su nombre
- `SET/QTH` — establece su ubicación
- `ACCEPT/SPOT` — configura el filtrado de spots

Los comandos se almacenan como `DxClusterStartupCommands`.

## Pestaña RBN

Se conecta al Reverse Beacon Network mediante telnet con limitación de velocidad.

1. Haga clic en la pestaña **RBN**.
2. Ingrese el nombre del host de RBN en **Server:**. Este valor se guarda como `RbnHost`.
3. Ingrese el puerto telnet en **Port:**. Rango válido: 1–65535. Este valor se guarda como `RbnPort`.
4. Ingrese su indicativo en **Callsign:**. Este valor se guarda como `RbnCallsign`.
5. Establezca el **Rate Limit:** para limitar la cantidad de spots por segundo. Este valor se guarda como `RbnRateLimit`.
6. Haga clic en **Connect**.
7. Confirme que el indicador de estado cambie a **Connected**. El tráfico telnet sin procesar aparece en la **RBN Console**.
8. Para enviar un comando, escriba en el campo de línea de comandos y haga clic en **Send**.
9. Para establecer el color del spot, haga clic en **Spot Color:** y seleccione un color. Este valor se guarda como `RbnSpotColor`.
10. Para que RBN se conecte automáticamente cada vez que se inicie AetherSDR, active **Auto-connect on startup**. Esto se guarda como `RbnAutoConnect`.

### Comandos de inicio para RBN

Haga clic en **Startup Commands…** para abrir un diálogo donde puede ingresar un comando por línea. Estos comandos se envían al servidor de RBN automáticamente después de cada inicio de sesión.

Los comandos se almacenan como `RbnStartupCommands`.

## Pestaña WSJT-X

Escucha transmisiones UDP de WSJT-X y muestra los spots decodificados.

1. Haga clic en la pestaña **WSJT-X**.
2. Ingrese la dirección de enlace UDP en **Address:**. Este valor se guarda como `WsjtxAddress`.
3. Ingrese el puerto UDP en **Port:**. Rango válido: 1–65535. Este valor se guarda como `WsjtxPort`.
4. Haga clic en **Start**.
5. Confirme que el indicador de estado cambie a **Listening**. Las transmisiones decodificadas aparecen en la consola **WSJT-X Decodes**.
6. Para que el listener se inicie automáticamente cada vez que se inicie AetherSDR, active **Auto-start on startup**. Esto se guarda como `WsjtxAutoStart`.
7. Use las casillas de verificación de filtro para controlar qué spots se muestran:
   - **CQ** — muestra solo llamadas CQ. Se guarda como `WsjtxFilterCQ`.
   - **CQ POTA** — muestra llamadas CQ POTA. Se guarda como `WsjtxFilterPOTA`.
   - **Calling Me** — muestra solo decodificaciones dirigidas a su indicativo. Se guarda como `WsjtxFilterCallingMe`.
8. Haga clic en cada muestra de color para establecer el color de esa categoría:
   - **CQ color** — `WsjtxColorCQ`
   - **POTA color** — `WsjtxColorPOTA`
   - **Calling Me color** — `WsjtxColorCallingMe`
   - **Default color** — `WsjtxColorDefault`
9. Establezca **Spot Life:** para controlar cuántos segundos los spots de WSJT-X permanecen en el panadapter. Este valor se guarda como `WsjtxSpotLife`.

## Pestaña SpotCollector

Recibe spots de DX transmitidos por SpotCollector de Ham Radio Deluxe a través de UDP.

1. Haga clic en la pestaña **SpotCollector**.
2. Establezca **UDP Port:** en el puerto en el que SpotCollector está transmitiendo. Rango válido: 1–65535. Este valor se guarda como `SpotCollectorPort`.
3. Haga clic en **Start**.
4. Confirme que el indicador de estado cambie a **Listening**. Los spots entrantes aparecen en la consola **SpotCollector Spots** a medida que llegan.
5. Para que el listener se inicie automáticamente cada vez que se inicie AetherSDR, active **Auto-start on startup**. Esto se guarda como `SpotCollectorAutoStart`.

## Pestaña POTA

Consulta api.pota.app para obtener activaciones actuales de Parks on the Air.

1. Haga clic en la pestaña **POTA**.
2. El indicador **Server:** muestra `api.pota.app (HTTP polling)`.
3. Establezca **Poll Interval:** para controlar cuántos segundos entre consultas. Este valor se guarda como `PotaPollInterval`.
4. Haga clic en **Start**.
5. Confirme que el indicador de estado cambie a **Polling**. El feed de activaciones aparece en la consola **POTA Activations**.
6. Para establecer el color del spot, haga clic en **Spot Color:** y seleccione un color. Este valor se guarda como `PotaSpotColor`.
7. Para que la consulta se inicie automáticamente cada vez que se inicie AetherSDR, active **Auto-start on startup**. Esto se guarda como `PotaAutoStart`.

## Pestaña FreeDV

Se conecta a un feed WebSocket de spots del reporteador de QSO de FreeDV.

1. Haga clic en la pestaña **FreeDV**.
2. El indicador **Server:** muestra `qso.freedv.org (WebSocket)`.
3. Haga clic en **Start**.
4. Confirme que el indicador de estado cambie a **Connected**. La actividad de FreeDV aparece en la consola **FreeDV Spots**.
5. Para establecer el color del spot, haga clic en **Spot Color:** y seleccione un color. Este valor se guarda como `FreeDvSpotColor`.
6. Para que la conexión se inicie automáticamente cada vez que se inicie AetherSDR, active **Auto-start on startup**. Esto se guarda como `FreeDvAutoStart`.

### Reportes de FreeDV Reporter

La pestaña **FreeDV** también contiene controles de reporte de estación que transmiten su actividad al mapa público de FreeDV Reporter.

#### Requisitos antes de activar

- Debe estar disponible un indicativo válido, ya sea desde la radio (cuando **Use radio** está marcado) o escrito en el campo **Callsign:**.
- Debe estar disponible un cuadrado de cuadrícula Maidenhead válido, ya sea desde el módulo GPS de la radio (cuando **Use GPS** está marcado, en hardware compatible) o escrito en el campo **Grid Square:**.

Si falta alguno de estos valores al intentar activar los reportes, AetherSDR muestra una advertencia y deja la casilla sin marcar.

#### Pasos para activar los reportes

1. Haga clic en la pestaña **FreeDV**.
2. En la sección de reportes de la estación, confirme que el campo **Callsign:** muestre su indicativo.
   - Si **Use radio** está marcado, el campo se completa automáticamente desde el indicativo configurado en la radio y es de solo lectura. Desmarque **Use radio** para ingresar un indicativo manualmente.
3. Confirme que el campo **Grid Square:** muestre su localizador Maidenhead.
   - En radios con hardware GPS, marque **Use GPS** para completarlo automáticamente. Desmarque **Use GPS** para escribir un cuadrado de cuadrícula manualmente.
4. Opcionalmente, ingrese un mensaje corto en **Station Msg:** — aparece junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o el cuadrado de cuadrícula están en blanco, aparece un diálogo de advertencia. Complete el valor faltante e intente nuevamente.
6. La generación de reportes ahora está activa siempre que el módem RADE esté funcionando.

## Pestaña Spot List

Muestra una tabla unificada y buscable de todos los spots activos de todas las fuentes.

1. Haga clic en la pestaña **Spot List**.
2. Use las casillas de verificación **Bands:** para alternar la visibilidad en la tabla. Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). Estas casillas usan un diseño de flujo que se ajusta a una nueva fila cuando el diálogo es estrecho, manteniendo la etiqueta de texto legible.
3. Haga clic en **Clear** para vaciar la lista de spots actual.
4. La **Spot table** muestra todos los spots con columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. Haga doble clic en cualquier fila para sintonizar el slice activo a esa frecuencia. AetherSDR lee la pista de modo del comentario del spot y cambia el slice al modo correcto al mismo tiempo.

## Pestaña Display

Controla cómo aparecen los spots en el panadapter, además de los marcadores de Signal History y el coloreado de DXCC.

1. Haga clic en la pestaña **Display**.

### Fila superior de alternancia

| Alternancia | Descripción | Clave de configuración |
|-------------|-------------|------------------------|
| **Spots:** | Alternancia maestra para la superposición de spots de DX. Por defecto está **Enabled**. | `IsSpotsEnabled` |
| **Memories:** | Alterna la superposición de canales de memoria en el panadapter. Por defecto está **Disabled**. | `IsMemorySpotsEnabled` |
| **Auto:** | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (p. ej., CW, FT8, RTTY). Por defecto está **Enabled**. | `SpotAutoSwitchMode` |
| **Signals** | Marcadores dorados para señales detectadas de ancho de voz en el panadapter. Por defecto está **Disabled**. Misma alternancia que View > Signal History Markers. | `SHistoryMarkersEnabled` |
| **QRM** | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Por defecto está **Disabled**. Misma alternancia que View > QRM History Markers. | `SHistoryQrmEnabled` |
| **Clear All** | Limpia todos los spots de DX, el feed de memoria, los marcadores de Signal History y los marcadores QRM del espectro. | — |

### Controles deslizantes comunes

| Control deslizante | Descripción | Clave de configuración |
|--------------------|-------------|------------------------|
| **Levels:** | Número de filas de apilamiento vertical para spots. Rango 1–10, valor predeterminado 3. | `SpotsMaxLevel` |
| **Position:** | Posición vertical en el panadapter. Rango 0–100, valor predeterminado 50. | `SpotsStartingHeightPercentage` |
| **Font Size:** | Tamaño del texto del spot. Rango 8–32, valor predeterminado 16. | `SpotFontSize` |
| **Spot Lifetime:** | Segundos antes de que un spot se desvanezca. Pasos no lineales desde 10 segundos hasta 24 horas. | `DxClusterSpotLifetimeSec` |

### Sección de colores de anulación

| Control | Descripción | Clave de configuración |
|---------|-------------|------------------------|
| **Override Colors:** | Fuerza un solo color de texto para todos los spots. | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto del spot | Abre QColorDialog para elegir el color del texto del spot. Valor predeterminado #FFFF00. | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilita un color de fondo de spot personalizado. Valor predeterminado **Enabled**. | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Selecciona automáticamente el color de fondo para contraste. Valor predeterminado **Enabled**. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo del spot | Abre QColorDialog para el color de fondo del spot. Valor predeterminado #000000. | `SpotsOverrideBgColor` |
| **Background Opacity:** | Opacidad del color de fondo del spot. Rango 0–100, valor predeterminado 48. | `SpotsBackgroundOpacity` |
| **Spot Lines:** | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactive durante concursos para reducir el desorden visual. Valor predeterminado **Enabled**. | `IsSpotsLinesEnabled` |
| **Total Spots:** | Conteo en vivo de spots actualmente rastreados de todas las fuentes. | — |

### Sección de coloreado DXCC

Controles en la columna izquierda debajo del divisor.

| Control | Descripción | Clave de configuración |
|---------|-------------|------------------------|
| **DXCC Colors:** | Colorea los spots según el estado trabajado/confirmado/necesitado de DXCC. | `IsDxccColoringEnabled` |
| **Log File (ADIF):** | Carga un archivo de registro ADIF para impulsar el coloreado DXCC. Supervisa automáticamente el archivo en busca de cambios después de la selección. La recarga automática está siempre habilitada cuando se selecciona un archivo. | `DxccAdifFilePath` |
| **Imported:** | Muestra el conteo de QSO y el conteo de entidades cuando se carga un registro. Formato: '<N> QSOs / <M> entities'. | — |
| **Muestras de color DXCC (New DXCC / New Band / New Mode / Worked)** | Abre un selector de color para cada categoría de estado DXCC. | `DxccColorNewEntity` / `DxccColorNewBand` / `DxccColorNewMode` / `DxccColorWorked` |

### Sección Signal History

Controles en la columna derecha debajo del divisor.

| Control | Descripción | Clave de configuración |
|---------|-------------|------------------------|
