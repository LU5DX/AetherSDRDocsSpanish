# SpotHub

El diálogo de SpotHub (`Settings > SpotHub...`) es el centro central para conectarse a fuentes de spots DX y configurar cómo se muestran los spots en el panadapter.

## Abrir SpotHub

1. Abra `Settings > SpotHub...`.

El diálogo recuerda su tamaño y posición entre sesiones.

## Pestañas de fuentes

### Cluster (pestaña)

La pestaña Cluster proporciona una conexión telnet a un cluster DX.

1. En el campo `Server:`, ingrese el nombre del host del cluster DX.
2. En el campo `Port:`, ingrese el puerto telnet (1-65535).
3. En el campo `Callsign:`, ingrese su indicativo de inicio de sesión.
4. Haga clic en `Connect` para establecer la conexión telnet. La etiqueta del botón cambia a `Disconnect` mientras está conectado.
5. Opcionalmente, active `Auto-connect on startup` para conectarse automáticamente al iniciar.

La `Cluster Console` muestra el tráfico telnet sin procesar. Escriba comandos en el campo de entrada y haga clic en `Send` para enviarlos al cluster.

Haga clic en `Spot Color:` para abrir un selector de color para los spots del cluster.

Haga clic en `Startup Commands…` para editar los comandos enviados automáticamente después de cada inicio de sesión. Un comando por línea, por ejemplo:
- `SET/NAME`
- `SET/QTH`
- `ACCEPT/SPOT`

### RBN (pestaña)

La pestaña RBN se conecta al Reverse Beacon Network a través de telnet con limitación de velocidad.

1. En el campo `Server:`, ingrese el nombre del host telnet de RBN.
2. En el campo `Port:`, ingrese el puerto telnet.
3. En el campo `Callsign:`, ingrese su indicativo de inicio de sesión.
4. En el campo `Rate Limit:`, establezca el máximo de spots por segundo.
5. Haga clic en `Connect` para establecer la conexión telnet.
6. Opcionalmente, active `Auto-connect on startup` para conectarse automáticamente al iniciar.

La `RBN Console` muestra el tráfico telnet sin procesar. Escriba comandos en el campo de entrada y haga clic en `Send` para enviarlos al servidor RBN.

Haga clic en `Spot Color:` para abrir un selector de color para los spots de RBN.

Haga clic en `Startup Commands…` para editar los comandos enviados automáticamente después de cada inicio de sesión (independiente de los comandos de la pestaña Cluster). Un comando por línea.

### WSJT-X (pestaña)

La pestaña WSJT-X escucha transmisiones UDP de WSJT-X.

1. En el campo `Address:`, ingrese la dirección de enlace UDP para los mensajes de WSJT-X.
2. En el campo `Port:`, ingrese el puerto UDP.
3. Haga clic en `Start` para comenzar a escuchar. La etiqueta del botón cambia a `Stop` mientras escucha.
4. Opcionalmente, active `Auto-start on startup` para iniciar el listener automáticamente al iniciar.

Use las casillas de verificación de filtro para controlar qué decodificaciones aparecen:
- **CQ** — Mostrar solo llamadas CQ.
- **CQ POTA** — Mostrar solo llamadas CQ POTA.
- **Calling Me** — Mostrar solo decodificaciones dirigidas a su indicativo.

Haga clic en una muestra de color para abrir un selector de color para cada categoría de spot de WSJT-X (color CQ, color POTA, color Calling Me, color Predeterminado).

Establezca `Spot Life:` para controlar cuántos segundos permanecen los spots de WSJT-X en el panadapter.

### SpotCollector (pestaña)

La pestaña SpotCollector escucha transmisiones UDP de Ham Radio Deluxe SpotCollector.

1. En el campo `UDP Port:`, ingrese el puerto en el que transmite SpotCollector.
2. Haga clic en `Start` para comenzar a escuchar. La etiqueta del botón cambia a `Stop` mientras escucha.
3. Opcionalmente, active `Auto-start on startup` para iniciar el listener automáticamente al iniciar.

### POTA (pestaña)

La pestaña POTA consulta api.pota.app en busca de activaciones actuales.

1. En el campo `Poll Interval:`, establezca los segundos entre consultas.
2. Haga clic en `Start` para comenzar a consultar. La etiqueta del botón cambia a `Stop` mientras consulta.
3. Opcionalmente, active `Auto-start on startup` para iniciar la consulta automáticamente al iniciar.

Haga clic en `Spot Color:` para abrir un selector de color para los spots de POTA.

### FreeDV (pestaña)

La pestaña FreeDV se conecta al feed WebSocket del reportero de QSO de FreeDV en qso.freedv.org. Esta pestaña solo está disponible cuando la compilación incluye soporte para WebSocket.

1. Haga clic en `Start` para conectarse al WebSocket de FreeDV. La etiqueta del botón cambia a `Stop` mientras está conectado.
2. Opcionalmente, active `Auto-start on startup` para conectarse automáticamente al iniciar.

Haga clic en `Spot Color:` para abrir un selector de color para los spots de FreeDV.

### Station Reporting

El grupo **Station Reporting** dentro de la pestaña FreeDV permite que AetherSDR transmita la actividad de su estación al mapa público del Reportero FreeDV en qso.freedv.org siempre que el módem RADE esté activo.

#### Requisitos

- La compilación debe incluir soporte para WebSocket (`HAVE_WEBSOCKETS`). En Windows, también se requiere `HAVE_RADE`.
- Tanto un indicativo como un locator deben resolverse a valores no vacíos antes de que se pueda activar la casilla de verificación `Enable FreeDV Reporter reporting when RADE is active`.

#### Cómo se resuelven el indicativo y el locator

Cuando habilita la notificación, AetherSDR resuelve el indicativo y el locator en el siguiente orden:

**Indicativo**
1. Si `Use radio` está marcada y la radio tiene un indicativo configurado, se usa ese indicativo.
2. De lo contrario, se usa el valor escrito en `Callsign:`.

**Locator**
1. Si `Use GPS` está marcada, la radio tiene hardware GPS y hay un locator derivado del GPS disponible, se usa ese locator.
2. De lo contrario, se usa el valor escrito en `Grid Square:`.

Si alguno de los valores está vacío después de la resolución, aparece un diálogo de advertencia y la casilla de verificación vuelve al estado desmarcado. Esto evita que se transmitan valores en blanco o de marcador de posición (como `N0CALL` o `AA00`) al mapa público compartido.

#### Configuración de la notificación

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `FreeDV`.
3. En el grupo **Station Reporting**, confirme que el campo de indicativo muestre el indicativo correcto.
   - Si `Use radio` está marcada, el campo se completa desde el indicativo configurado en la radio y es de solo lectura. Desmarque `Use radio` para ingresar un indicativo manualmente.
4. Confirme que el campo de locator muestre un locator Maidenhead válido.
   - Si `Use GPS` está marcada (visible solo en radios con hardware GPS), el campo se completa desde el módulo GPS y es de solo lectura. Desmarque `Use GPS` para ingresar un locator manualmente.
5. Opcionalmente, ingrese un mensaje corto en `Station Msg:`. Este texto aparece junto a su indicativo en el mapa público.
6. Marque `Enable FreeDV Reporter reporting when RADE is active`.
   - Si el indicativo o el locator están vacíos, aparece una advertencia y la casilla de verificación permanece desmarcada. Complete el campo faltante e intente nuevamente.

AetherSDR guarda la configuración en `FreeDvAutoReport` y comienza a informar a qso.freedv.org siempre que el módem RADE esté activo.

### Spot List (pestaña)

La pestaña Spot List muestra una tabla unificada y buscable de todos los spots activos.

1. Use las casillas de verificación por banda para alternar la visibilidad de los spots en cada banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.).
2. Haga clic en `Clear` para vaciar la lista de spots actual.
3. Haga doble clic en una fila de la tabla para sintonizar el slice activo a la frecuencia del spot. Si hay información de modo presente en el comentario del spot y `Auto:` está habilitado en la pestaña Display, el slice cambia a ese modo automáticamente.

Las columnas de la tabla son: Hora, Freq, DX Call, Comentario, Spotter, Banda, Modo, Fuente.

### Display (pestaña)

La pestaña Display controla la visualización de spots en el panadapter, los parámetros de Signal History y el coloreado por DXCC.

#### Alternancias maestras

| Control | Descripción | Clave de configuración |
|---------|-------------|-------------|
| `Spots:` | Alternancia maestra para la superposición de spots DX. | `IsSpotsEnabled` |
| `Memories:` | Alterna la superposición de canales de memoria en el panadapter. | `IsMemorySpotsEnabled` |
| `Auto:` | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (ej. CW, FT8, RTTY). | `SpotAutoSwitchMode` |
| `Signals` (Signal History) | Marcadores dorados para señales de ancho de voz detectadas en el panadapter. | `SHistoryMarkersEnabled` |
| `QRM` (Signal History) | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. | `SHistoryQrmEnabled` |
| `Clear All` | Borra todos los spots DX, el feed de memoria, los marcadores de Signal History y los marcadores de QRM del espectro. | — |

#### Apariencia de los spots

| Control | Descripción | Clave de configuración |
|---------|-------------|-------------|
| `Levels:` | Número de filas de apilamiento vertical para spots (1-10). | `SpotsMaxLevel` |
| `Position:` | Posición vertical en el panadapter (0-100). | `SpotsStartingHeightPercentage` |
| `Font Size:` | Tamaño del texto del spot (8-32). | `SpotFontSize` |
| `Spot Lifetime:` | Segundos antes de que un spot se desvanezca (10 seg – 24 hrs, pasos no lineales). | `DxClusterSpotLifetimeSec` |

#### Anulaciones de color

| Control | Descripción | Clave de configuración |
|---------|-------------|-------------|
| `Override Colors:` | Fuerza un solo color de texto para todos los spots. | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto del spot | Abre QColorDialog para elegir el color del texto del spot. | `SpotsOverrideColor` |
| `Override Background: Enabled` | Habilita un color de fondo personalizado para spots. | `IsSpotsOverrideBackgroundColorsEnabled` |
| `Override Background: Auto` | Selecciona automáticamente el color de fondo para contraste. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo del spot | Abre QColorDialog para el color de fondo del spot. | `SpotsOverrideBgColor` |
| `Background Opacity:` | Opacidad del color de fondo del spot (0-100). | `SpotsBackgroundOpacity` |
| `Spot Lines:` | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactive durante concursos para reducir el desorden visual. | `IsSpotsLinesEnabled` |

#### DXCC Coloring (sección)

La columna izquierda debajo del divisor.

| Control | Descripción | Clave de configuración |
|---------|-------------|-------------|
| `DXCC Colors:` | Colorea los spots por estado de DXCC trabajado/confirmado/necesitado. | `IsDxccColoringEnabled` |
| `Log File (ADIF):` | Carga un archivo de registro ADIF para impulsar el coloreado DXCC. Observa automáticamente el archivo en busca de cambios después de la selección. | `DxccAdifFilePath` |
| `Imported:` | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entidades`. | — |
| Muestras de color DXCC (New DXCC / New Band / New Mode / Worked) | Abre un selector de color para cada categoría de estado DXCC. | `DxccColorNewEntity / DxccColorNewBand / DxccColorNewMode / DxccColorWorked` |

#### Signal History (sección)

La columna derecha debajo del divisor.

| Control | Descripción | Clave de configuración |
|---------|-------------|-------------|
| `Marker Lifetime:` | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado (15-300 seg). Valor predeterminado 60 s. | `SHistoryLifetimeS` |
| `QRM Gate:` | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM (3-30 seg). Valor predeterminado 6 s. | `SHistoryQrmGateS` |
| `Edge Threshold:` | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde lateral de la portadora de S-History (1.0-10.0 dB). Valor predeterminado 3.0 dB. | `SHistorySoftEdgeDb` |
| Muestras de color de Signal History (Signals / QRM) | Abre un selector de color para los marcadores de señal de voz (dorados) y los marcadores de QRM (rojos). Valores predeterminados: #FFC800 / #FF0000. | `SHistoryColorSignals / SHistoryColorQrm` |
| `Snap to Step:` | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de portadora. Valor predeterminado Deshabilitado. | `SHistorySnapToStep` |

#### Indicador

`Total Spots:` muestra el recuento en vivo de spots actualmente rastreados de todas las fuentes.

## Recarga automática del registro ADIF cuando es actualizado por un registrador

Cuando el coloreado DXCC está habilitado, AetherSDR lee su registro ADIF una vez al inicio. La recarga automática le indica a AetherSDR que vuelva a leer el archivo cada vez que su software de registro lo actualice, para que el coloreado de trabajado/confirmado/necesitado en el panadapter se mantenga actualizado sin intervención manual.

### Antes de comenzar

- El coloreado DXCC debe estar habilitado y ya debe haberse cargado un archivo de registro ADIF. Consulte [Habilitar coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md).
- Su software de registro debe escribir las actualizaciones en la misma ruta de archivo ADIF almacenada en `DxccAdifFilePath`.

### Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `Display`.
3. Confirme que `DXCC Colors:` esté habilitado (la alternancia muestra su estado activo).
4. Confirme que `Log File (ADIF):` muestre la ruta de archivo correcta.

La recarga automática siempre está habilitada cuando se selecciona un archivo. AetherSDR observa el archivo en `DxccAdifFilePath` en busca de cambios. Cada vez que su registrador escribe un nuevo QSO, AetherSDR vuelve a leer el archivo y actualiza el coloreado de los spots en el panadapter.

## Consejos

- Si su registrador escribe un archivo temporal
