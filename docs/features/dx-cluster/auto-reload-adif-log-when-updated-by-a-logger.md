# SpotHub

El cuadro de diálogo SpotHub (`Settings > SpotHub...`) es el centro central para conectarse a fuentes de spots DX y configurar cómo se muestran los spots en el panadapter.

## Abrir SpotHub

1. Abra `Settings > SpotHub...`.

El cuadro de diálogo recuerda su tamaño y posición entre sesiones. El cuadro de diálogo tiene un ancho mínimo de 360 píxeles, por lo que se puede reducir hasta el ancho de la columna visible de la pestaña Spot List una vez que se ocultan las columnas.

## Pestañas de fuente

### Cluster (pestaña)

La pestaña Cluster proporciona una conexión telnet a un clúster DX.

1. En el campo `Server:`, introduzca el nombre de host del clúster DX.
2. En el campo `Port:`, introduzca el puerto telnet (1-65535).
3. En el campo `Callsign:`, introduzca su indicativo de inicio de sesión.
4. Haga clic en `Connect` para establecer la conexión telnet. La etiqueta del botón cambia a `Disconnect` mientras está conectado.
5. Opcionalmente, active `Auto-connect on startup` para conectarse automáticamente al inicio.

La `Cluster Console` muestra el tráfico telnet sin procesar. Escriba comandos en el campo de entrada y haga clic en `Send` para enviarlos al clúster.

Haga clic en `Spot Color:` para abrir un selector de color para los spots del clúster.

Haga clic en `Startup Commands…` para editar los comandos enviados automáticamente después de cada inicio de sesión. Un comando por línea, por ejemplo:
- `SET/NAME`
- `SET/QTH`
- `ACCEPT/SPOT`

### RBN (pestaña)

La pestaña RBN se conecta a la Reverse Beacon Network a través de telnet con limitación de velocidad.

1. En el campo `Server:`, introduzca el nombre de host telnet de RBN.
2. En el campo `Port:`, introduzca el puerto telnet.
3. En el campo `Callsign:`, introduzca su indicativo de inicio de sesión.
4. En el campo `Rate Limit:`, establezca el máximo de spots por segundo.
5. Haga clic en `Connect` para establecer la conexión telnet.
6. Opcionalmente, active `Auto-connect on startup` para conectarse automáticamente al inicio.

La `RBN Console` muestra el tráfico telnet sin procesar. Escriba comandos en el campo de entrada y haga clic en `Send` para enviarlos al servidor RBN.

Haga clic en `Spot Color:` para abrir un selector de color para los spots de RBN.

Haga clic en `Startup Commands…` para editar los comandos enviados automáticamente después de cada inicio de sesión (independiente de los comandos de la pestaña Cluster). Un comando por línea.

### WSJT-X (pestaña)

La pestaña WSJT-X escucha las transmisiones UDP de WSJT-X.

1. En el campo `Address:`, introduzca la dirección de enlace UDP para los mensajes de WSJT-X.
2. En el campo `Port:`, introduzca el puerto UDP.
3. Haga clic en `Start` para comenzar a escuchar. La etiqueta del botón cambia a `Stop` mientras está escuchando.
4. Opcionalmente, active `Auto-start on startup` para iniciar el receptor automáticamente al inicio.

Use las casillas de verificación de filtro para controlar qué decodificaciones aparecen:
- **CQ** — Muestra solo llamadas CQ.
- **CQ POTA** — Muestra solo llamadas CQ POTA.
- **Calling Me** — Muestra solo decodificaciones dirigidas a su indicativo.

Haga clic en una muestra de color para abrir un selector de color para cada categoría de spot de WSJT-X (CQ color, POTA color, Calling Me color, Default color).

Establezca `Spot Life:` para controlar cuántos segundos permanecen los spots de WSJT-X en el panadapter.

### SpotCollector (pestaña)

La pestaña SpotCollector escucha las transmisiones UDP de Ham Radio Deluxe SpotCollector.

1. En el campo `UDP Port:`, introduzca el puerto en el que SpotCollector transmite.
2. Haga clic en `Start` para comenzar a escuchar. La etiqueta del botón cambia a `Stop` mientras está escuchando.
3. Opcionalmente, active `Auto-start on startup` para iniciar el receptor automáticamente al inicio.

### POTA (pestaña)

La pestaña POTA consulta api.pota.app para obtener activaciones actuales.

1. En el campo `Poll Interval:`, establezca los segundos entre consultas.
2. Haga clic en `Start` para comenzar a consultar. La etiqueta del botón cambia a `Stop` mientras consulta.
3. Opcionalmente, active `Auto-start on startup` para iniciar la consulta automáticamente al inicio.

Haga clic en `Spot Color:` para abrir un selector de color para los spots de POTA.

### FreeDV (pestaña)

La pestaña FreeDV se conecta al feed WebSocket del reportero QSO de FreeDV en qso.freedv.org. Esta pestaña solo está disponible cuando la compilación incluye soporte WebSocket.

1. Haga clic en `Start` para conectarse al WebSocket de FreeDV. La etiqueta del botón cambia a `Stop` mientras está conectado.
2. Opcionalmente, active `Auto-start on startup` para conectarse automáticamente al inicio.

Haga clic en `Spot Color:` para abrir un selector de color para los spots de FreeDV.

### Station Reporting

El grupo **Station Reporting** dentro de la pestaña FreeDV permite que AetherSDR transmita la actividad de su estación al mapa público del Reportero FreeDV en qso.freedv.org cada vez que el módem RADE esté activo.

#### Requisitos

- La compilación debe incluir soporte WebSocket (`HAVE_WEBSOCKETS`). En Windows, también se requiere `HAVE_RADE`.
- Tanto un indicativo como un cuadrado de cuadrícula deben resolverse en valores no vacíos antes de que se pueda activar la casilla de verificación `Enable FreeDV Reporter reporting when RADE is active`.

#### Cómo se resuelven el indicativo y la cuadrícula

Cuando habilita la notificación, AetherSDR resuelve el indicativo y la cuadrícula en el siguiente orden:

**Indicativo**
1. Si `Use radio` está marcado y la radio tiene un indicativo configurado, se usa ese indicativo.
2. De lo contrario, se usa el valor escrito en `Callsink:`.

**Cuadrado de cuadrícula**
1. Si `Use GPS` está marcado, la radio tiene hardware GPS y hay una cuadrícula derivada del GPS disponible, se usa esa cuadrícula.
2. De lo contrario, se usa el valor escrito en `Grid Square:`.

Si alguno de los valores está vacío después de la resolución, aparece un cuadro de diálogo de advertencia y la casilla de verificación vuelve a estar desmarcada. Esto evita que se transmitan valores en blanco o marcadores de posición (como `N0CALL` o `AA00`) al mapa público compartido.

#### Configurar la notificación

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `FreeDV`.
3. En el grupo **Station Reporting**, confirme que el campo de indicativo muestre el indicativo correcto.
   - Si `Use radio` está marcado, el campo se completa con el indicativo configurado de la radio y es de solo lectura. Desmarque `Use radio` para introducir un indicativo manualmente.
4. Confirme que el campo de cuadrado de cuadrícula muestre un localizador Maidenhead válido.
   - Si `Use GPS` está marcado (visible solo en radios con hardware GPS), el campo se completa desde el módulo GPS y es de solo lectura. Desmarque `Use GPS` para introducir una cuadrícula manualmente.
5. Opcionalmente, introduzca un mensaje corto en `Station Msg:`. Este texto aparece junto a su indicativo en el mapa público.
6. Marque `Enable FreeDV Reporter reporting when RADE is active`.
   - Si el indicativo o la cuadrícula están vacíos, aparece una advertencia y la casilla de verificación permanece desmarcada. Complete el campo faltante e intente de nuevo.

AetherSDR guarda la configuración en `FreeDvAutoReport` y comienza a informar a qso.freedv.org cada vez que el módem RADE está activo.

### Spot List (pestaña)

La pestaña Spot List muestra una tabla unificada y buscable de todos los spots activos.

1. Use las casillas de verificación por banda para alternar la visibilidad de los spots en cada banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). Las casillas de verificación de banda usan un diseño de flujo que se ajusta a una nueva fila cuando el cuadro de diálogo se reduce, manteniendo las etiquetas legibles en lugar de comprimirlas.
2. Haga clic en `Clear` para vaciar la lista de spots actual.
3. Haga doble clic en una fila de la tabla para sintonizar el slice activo a la frecuencia del spot. Si la información de modo está presente en el comentario del spot y `Auto:` está habilitado en la pestaña Display, el slice cambia a ese modo automáticamente.

Las columnas de la tabla son: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source.

Haga clic derecho en cualquier encabezado de columna para mostrar u ocultar columnas individuales. El menú del encabezado permanece abierto mientras se alternan las columnas marcables (por ejemplo, oculte "Band" y "Mode" de una sola vez en lugar de volver a abrir el menú para cada una). Haga clic en un área no marcable o presione Escape para cerrar el menú.

### Display (pestaña)

La pestaña Display controla la visualización de spots en el panadapter, los ajustes de Signal History y la coloración de DXCC.

#### Conmutadores maestros

| Control | Descripción | Clave de configuración |
|---------|-------------|------------------------|
| `Spots:` | Conmutador maestro para la superposición de spots DX. El botón siempre muestra "Enabled". | `IsSpotsEnabled` |
| `Memories:` | Alterna la superposición de canales de memoria en el panadapter. | `IsMemorySpotsEnabled` |
| `Auto:` | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (ej. CW, FT8, RTTY). | `SpotAutoSwitchMode` |
| `Signals` (Signal History) | Marcadores dorados para señales de ancho de voz detectadas en el panadapter. | `SHistoryMarkersEnabled` |
| `QRM` (Signal History) | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. | `SHistoryQrmEnabled` |
| `Clear All` | Limpia todos los spots DX, el feed de memoria, los marcadores de Signal History y los marcadores QRM del espectro. | — |

#### Apariencia de los spots

| Control | Descripción | Clave de configuración |
|---------|-------------|------------------------|
| `Levels:` | Número de filas de apilamiento vertical para spots (1-10). | `SpotsMaxLevel` |
| `Position:` | Posición vertical en el panadapter (0-100). | `SpotsStartingHeightPercentage` |
| `Font Size:` | Tamaño del texto del spot (8-32). | `SpotFontSize` |
| `Spot Lifetime:` | Segundos antes de que un spot se desvanezca (10 seg - 24 hrs, pasos no lineales). | `DxClusterSpotLifetimeSec` |

#### Anulaciones de color

| Control | Descripción | Clave de configuración |
|---------|-------------|------------------------|
| `Override Colors:` | Fuerza un solo color de texto para todos los spots. El botón siempre muestra "Enabled". | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto del spot | Abre QColorDialog para elegir el color del texto del spot. | `SpotsOverrideColor` |
| `Override Background: Enabled` | Habilita un color de fondo personalizado para los spots. | `IsSpotsOverrideBackgroundColorsEnabled` |
| `Override Background: Auto` | Selecciona automáticamente el color de fondo para contraste. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo del spot | Abre QColorDialog para el color de fondo del spot. | `SpotsOverrideBgColor` |
| `Background Opacity:` | Opacidad del color de fondo del spot (0-100). | `SpotsBackgroundOpacity` |
| `Spot Lines:` | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. El botón siempre muestra "Enabled". Desactívelo durante concursos para reducir el desorden visual. | `IsSpotsLinesEnabled` |

#### DXCC Coloring (sección)

La columna izquierda debajo del divisor.

| Control | Descripción | Clave de configuración |
|---------|-------------|------------------------|
| `DXCC Colors:` | Colorea los spots según el estado de DXCC trabajado/confirmado/necesario. El botón siempre muestra "Enabled". | `IsDxccColoringEnabled` |
| `Log File (ADIF):` | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Vigila automáticamente el archivo en busca de cambios después de la selección. | `DxccAdifFilePath` |
| `Imported:` | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`. | — |
| Muestras de color DXCC (New DXCC / New Band / New Mode / Worked) | Abre un selector de color para cada categoría de estado DXCC. | `DxccColorNewEntity / DxccColorNewBand / DxccColorNewMode / DxccColorWorked` |

#### Signal History (sección)

La columna derecha debajo del divisor.

| Control | Descripción | Clave de configuración |
|---------|-------------|------------------------|
| `Marker Lifetime:` | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado (15-300 seg). Valor predeterminado 60 s. | `SHistoryLifetimeS` |
| `QRM Gate:` | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de ser clasificada como QRM (3-30 seg). Valor predeterminado 6 s. | `SHistoryQrmGateS` |
| `Edge Threshold:` | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde lateral de la portadora de S-History (1.0-10.0 dB). Valor predeterminado 3.0 dB. | `SHistorySoftEdgeDb` |
| Muestras de color de Signal History (Signals / QRM) | Abre un selector de color para los marcadores de señal de voz (dorado) y los marcadores QRM (rojo). Valores predeterminados: #FFC800 / #FF0000. | `SHistoryColorSignals / SHistoryColorQrm` |
| `Snap to Step:` | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora. El botón siempre muestra "Enabled". Valor predeterminado Deshabilitado. | `SHistorySnapToStep` |

#### Indicador

`Total Spots:` muestra el recuento en vivo de spots actualmente rastreados en todas las fuentes.

## Recarga automática del registro ADIF cuando un registrador lo actualiza

Cuando la coloración DXCC está habilitada, AetherSDR lee su registro ADIF una vez al inicio. La recarga automática le indica a AetherSDR que vuelva a leer el archivo cada vez que su software de registro lo actualice, de modo que la coloración trabajado/confirmado/necesario en el panadapter se mantenga actualizada sin intervención manual.

### Antes de comenzar

- La coloración DXCC debe estar habilitada y ya debe haberse cargado un archivo de registro ADIF. Consulte [Enable DXCC coloring from an ADIF log](enable-dxcc-coloring-from-an-ad
