# SpotHub

El cuadro de diálogo SpotHub es el centro principal para conectarse a fuentes de spots DX (DX cluster, Reverse Beacon Network, WSJT-X, SpotCollector, POTA y FreeDV) y para configurar cómo se muestran los spots en el panadapter.

## Abrir SpotHub

1. Abra `Settings > SpotHub...`.

## Resumen de SpotHub

El cuadro de diálogo SpotHub contiene varias pestañas, cada una dedicada a una fuente de spots diferente, además de una pestaña **Display** para la apariencia del panadapter.

## Pestaña Cluster

Se conecta a un DX cluster tradicional mediante telnet.

1. Haga clic en la pestaña **Cluster**.
2. Introduzca el nombre de host del cluster en **Server:**. Este valor se guarda como `ClusterHost`.
3. Introduzca el puerto telnet en **Port:**. Rango válido: 1–65535. Este valor se guarda como `ClusterPort`.
4. Introduzca su indicativo en **Callsign:**. Este valor se guarda como `ClusterCallsign`.
5. Haga clic en **Connect**.
6. Confirme que el indicador de estado cambia a **Connected**. El tráfico telnet sin procesar aparece en la **Cluster Console**.
7. Para enviar un comando, escriba en el campo de línea de comandos y haga clic en **Send**.
8. Para establecer el color de los spots, haga clic en **Spot Color:** y elija un color. Este valor se guarda como `ClusterSpotColor`.
9. Para que el cluster se conecte automáticamente cada vez que se inicie AetherSDR, active **Auto-connect on startup**. Esto se guarda como `ClusterAutoConnect`.

### Comandos de inicio para el cluster

Haga clic en **Startup Commands…** para abrir un cuadro de diálogo donde puede ingresar un comando por línea. Estos comandos se envían al servidor del cluster automáticamente después de cada inicio de sesión.

Los comandos típicos incluyen:
- `SET/NAME` — establece su nombre
- `SET/QTH` — establece su ubicación
- `ACCEPT/SPOT` — configura el filtrado de spots

Los comandos se almacenan como `DxClusterStartupCommands`.

## Pestaña RBN

Se conecta al Reverse Beacon Network mediante telnet con limitación de velocidad.

1. Haga clic en la pestaña **RBN**.
2. Introduzca el nombre de host de RBN en **Server:**. Este valor se guarda como `RbnHost`.
3. Introduzca el puerto telnet en **Port:**. Rango válido: 1–65535. Este valor se guarda como `RbnPort`.
4. Introduzca su indicativo en **Callsign:**. Este valor se guarda como `RbnCallsign`.
5. Establezca **Rate Limit:** para limitar el número de spots por segundo. Este valor se guarda como `RbnRateLimit`.
6. Haga clic en **Connect**.
7. Confirme que el indicador de estado cambia a **Connected**. El tráfico telnet sin procesar aparece en la **RBN Console**.
8. Para enviar un comando, escriba en el campo de línea de comandos y haga clic en **Send**.
9. Para establecer el color de los spots, haga clic en **Spot Color:** y elija un color. Este valor se guarda como `RbnSpotColor`.
10. Para que RBN se conecte automáticamente cada vez que se inicie AetherSDR, active **Auto-connect on startup**. Esto se guarda como `RbnAutoConnect`.

### Comandos de inicio para RBN

Haga clic en **Startup Commands…** para abrir un cuadro de diálogo donde puede ingresar un comando por línea. Estos comandos se envían al servidor RBN automáticamente después de cada inicio de sesión.

Los comandos se almacenan como `RbnStartupCommands`.

## Pestaña WSJT-X

Escucha transmisiones UDP de WSJT-X y muestra los spots decodificados.

1. Haga clic en la pestaña **WSJT-X**.
2. Introduzca la dirección de enlace UDP en **Address:**. Este valor se guarda como `WsjtxAddress`.
3. Introduzca el puerto UDP en **Port:**. Rango válido: 1–65535. Este valor se guarda como `WsjtxPort`.
4. Haga clic en **Start**.
5. Confirme que el indicador de estado cambia a **Listening**. Las transmisiones decodificadas aparecen en la consola **WSJT-X Decodes**.
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
9. Establezca **Spot Life:** para controlar cuántos segundos permanecen los spots de WSJT-X en el panadapter. Este valor se guarda como `WsjtxSpotLife`.

## Pestaña SpotCollector

Recibe spots DX transmitidos por SpotCollector de Ham Radio Deluxe mediante UDP.

1. Haga clic en la pestaña **SpotCollector**.
2. Establezca **UDP Port:** al puerto en el que SpotCollector está transmitiendo. Rango válido: 1–65535. Este valor se guarda como `SpotCollectorPort`.
3. Haga clic en **Start**.
4. Confirme que el indicador de estado cambia a **Listening**. Los spots entrantes aparecen en la consola **SpotCollector Spots** a medida que llegan.
5. Para que el listener se inicie automáticamente cada vez que se inicie AetherSDR, active **Auto-start on startup**. Esto se guarda como `SpotCollectorAutoStart`.

## Pestaña POTA

Consulta api.pota.app para obtener las activaciones actuales de Parks on the Air.

1. Haga clic en la pestaña **POTA**.
2. El indicador **Server:** muestra `api.pota.app (HTTP polling)`.
3. Establezca **Poll Interval:** para controlar cuántos segundos transcurren entre consultas. Este valor se guarda como `PotaPollInterval`.
4. Haga clic en **Start**.
5. Confirme que el indicador de estado cambia a **Polling**. La fuente de activaciones aparece en la consola **POTA Activations**.
6. Para establecer el color de los spots, haga clic en **Spot Color:** y elija un color. Este valor se guarda como `PotaSpotColor`.
7. Para que la consulta se inicie automáticamente cada vez que se inicie AetherSDR, active **Auto-start on startup**. Esto se guarda como `PotaAutoStart`.

## Pestaña FreeDV

Se conecta a una fuente WebSocket de spots del reportero QSO de FreeDV.

1. Haga clic en la pestaña **FreeDV**.
2. El indicador **Server:** muestra `qso.freedv.org (WebSocket)`.
3. Haga clic en **Start**.
4. Confirme que el indicador de estado cambia a **Connected**. La actividad de FreeDV aparece en la consola **FreeDV Spots**.
5. Para establecer el color de los spots, haga clic en **Spot Color:** y elija un color. Este valor se guarda como `FreeDvSpotColor`.
6. Para que la conexión se inicie automáticamente cada vez que se inicie AetherSDR, active **Auto-start on startup**. Esto se guarda como `FreeDvAutoStart`.

### Reporte del reportero FreeDV

La pestaña **FreeDV** también contiene controles de reporte de estación que transmiten su actividad al mapa público del reportero FreeDV.

#### Requisitos antes de habilitar

- Debe estar disponible un indicativo válido, ya sea desde la radio (cuando **Use radio** está marcado) o escrito en el campo **Callsign:**.
- Debe estar disponible un cuadrado de cuadrícula Maidenhead válido, ya sea desde el módulo GPS de la radio (cuando **Use GPS** está marcado, en hardware compatible) o escrito en el campo **Grid Square:**.

Si falta alguno de estos valores al intentar habilitar el reporte, AetherSDR muestra una advertencia y deja la casilla sin marcar.

#### Pasos para habilitar el reporte

1. Haga clic en la pestaña **FreeDV**.
2. En la sección de reporte de estación, confirme que el campo **Callsign:** muestra su indicativo.
   - Si **Use radio** está marcado, el campo se completa automáticamente con el indicativo configurado en la radio y es de solo lectura. Desmarque **Use radio** para ingresar un indicativo manualmente.
3. Confirme que el campo **Grid Square:** muestra su localizador Maidenhead.
   - En radios con hardware GPS, marque **Use GPS** para completarlo automáticamente. Desmarque **Use GPS** para escribir un cuadrado de cuadrícula manualmente.
4. Opcionalmente, ingrese un mensaje corto en **Station Msg:** — aparecerá junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si el indicativo o el cuadrado de cuadrícula está vacío, aparece un cuadro de diálogo de advertencia. Complete el valor faltante e intente nuevamente.
6. El reporte ahora está activo siempre que el módem RADE esté en funcionamiento.

## Pestaña Spot List

Muestra una tabla unificada y buscable de todos los spots en vivo de todas las fuentes.

1. Haga clic en la pestaña **Spot List**.
2. Use las casillas de verificación **Bands:** para alternar la visibilidad en la tabla. Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). Estas casillas usan un diseño de flujo que se envuelve a una nueva fila cuando el cuadro de diálogo es estrecho, manteniendo el texto de la etiqueta legible.
3. Haga clic en **Clear** para vaciar la lista de spots actual.
4. La **Spot table** muestra todos los spots con las columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. Haga doble clic en cualquier fila para sintonizar el slice activo a esa frecuencia. AetherSDR lee la sugerencia de modo del comentario del spot y cambia el slice al modo correcto al mismo tiempo.

### Ordenar la tabla de spots

Haga clic en cualquier encabezado de columna para ordenar la tabla por esa columna. Hacer clic en **Time** ordena por hora UTC, y hacer clic en **Freq** ordena por frecuencia. Hacer clic nuevamente en un encabezado de columna invierte el orden de clasificación — esta es la forma de volver al orden más reciente primero después de ordenar por otra columna.

## Pestaña Display

Controla cómo aparecen los spots en el panadapter, además de los marcadores de historial de señales y el coloreado DXCC.

1. Haga clic en la pestaña **Display**.

### Fila superior de alternadores

| Alternador | Descripción | Clave de configuración |
|--------|-------------|-------------|
| **Spots:** | Alternador principal para la superposición de spots DX. El valor predeterminado es **Enabled**. | `IsSpotsEnabled` |
| **Memories:** | Alterna la superposición de canales de memoria en el panadapter. El valor predeterminado es **Disabled**. | `IsMemorySpotsEnabled` |
| **Auto:** | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (p. ej., CW, FT8, RTTY). El valor predeterminado es **Enabled**. | `SpotAutoSwitchMode` |
| **Signals** | Marcadores dorados para señales detectadas de ancho de voz en el panadapter. El valor predeterminado es **Disabled**. Mismo alternador que View > Signal History Markers. | `SHistoryMarkersEnabled` |
| **QRM** | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. El valor predeterminado es **Disabled**. Mismo alternador que View > QRM History Markers. | `SHistoryQrmEnabled` |
| **Clear All** | Borra todos los spots DX, la fuente de memoria, los marcadores de historial de señales y los marcadores QRM del espectro. | — |

### Controles deslizantes comunes

| Control deslizante | Descripción | Clave de configuración |
|--------|-------------|-------------|
| **Levels:** | Número de filas de apilamiento vertical para spots. Rango 1–10, predeterminado 3. | `SpotsMaxLevel` |
| **Position:** | Posición vertical en el panadapter. Rango 0–100, predeterminado 50. | `SpotsStartingHeightPercentage` |
| **Font Size:** | Tamaño del texto de los spots. Rango 8–32, predeterminado 16. | `SpotFontSize` |
| **Spot Lifetime:** | Segundos antes de que un spot se desvanezca. Pasos no lineales de 10 segundos a 24 horas. | `DxClusterSpotLifetimeSec` |

### Sección de colores de anulación

| Control | Descripción | Clave de configuración |
|---------|-------------|-------------|
| **Override Colors:** | Fuerza un solo color de texto para todos los spots. | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto de spot | Abre QColorDialog para elegir el color del texto de los spots. Predeterminado #FFFF00. | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilita un color de fondo personalizado para los spots. Predeterminado **Enabled**. | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Selecciona automáticamente el color de fondo para contraste. Predeterminado **Enabled**. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo de spot | Abre QColorDialog para el color de fondo de los spots. Predeterminado #000000. | `SpotsOverrideBgColor` |
| **Background Opacity:** | Opacidad del color de fondo de los spots. Rango 0–100, predeterminado 48. | `SpotsBackgroundOpacity` |
| **Spot Lines:** | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactive durante concursos para reducir el desorden visual. Predeterminado **Enabled**. | `IsSpotsLinesEnabled` |
| **Total Spots:** | Conteo en vivo de spots actualmente rastreados en todas las fuentes. | — |

### Sección de coloreado DXCC

Controles en la columna izquierda debajo del divisor.

| Control | Descripción | Clave de configuración |
|---------|-------------|-------------|
| **DXCC Colors:** | Colorea los spots según el estado DXCC trabajado/confirmado/necesario. | `IsDxccColoringEnabled` |
| **Log File (ADIF):** | Carga un archivo de registro ADIF para impulsar el coloreado DXCC. Vigila automáticamente el archivo para detectar cambios después de la selección. La recarga automática está siempre habilitada cuando se selecciona un archivo. | `DxccAdifFilePath` |
| **Imported:** | Muestra el conteo de QSO y el conteo de entidades cuando se carga un registro. Formato: '<N> QSOs / <M> entities'. | — |
| **Muestras de color DXCC (New DXCC / New Band / New Mode / Worked)** | Abre un selector de color para cada categoría de estado DXCC. |
