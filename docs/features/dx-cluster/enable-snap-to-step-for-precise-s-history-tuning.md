# SpotHub (Diálogo de DX Cluster)

Centro central para conectarse a fuentes de spots DX — DX cluster, Reverse Beacon Network, WSJT-X, SpotCollector, POTA, FreeDV, EiBi y N1MM — y para configurar cómo se muestran los spots en el panadapter.

## Abrir SpotHub

1. Haga clic en **Settings > SpotHub...** en el menú principal.

## Conectarse a un DX Cluster

1. Haga clic en la pestaña **Cluster**.
2. Ingrese el nombre del servidor en **Server:** (predeterminado: `dxc.nc7j.com`).
3. Ingrese el puerto telnet en **Port:** (predeterminado: `7373`).
4. Ingrese su indicativo en **Callsign:**.
5. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando está conectado.
6. Opcional: Active **Auto-connect on startup** para conectarse automáticamente al iniciar.

### Consola del Cluster

- Vea el tráfico telnet sin procesar en el área de consola de solo lectura.
- Escriba comandos en el campo de texto junto a **Send** y haga clic en **Send** para transmitirlos.

### Color de los Spots

- Haga clic en **Spot Color:** para abrir un selector de color y elegir un color único para los spots del DX cluster en el panadapter.

## Conectarse a la Reverse Beacon Network (RBN)

1. Haga clic en la pestaña **RBN**.
2. Ingrese el nombre del servidor en **Server:** (predeterminado: `telnet.reversebeacon.net`).
3. Ingrese el puerto en **Port:** (predeterminado: `7000`).
4. Ingrese su indicativo en **Callsign:**.
5. Establezca el **Rate Limit:** para limitar los spots por segundo (evita la sobrecarga en bandas concurridas).
6. Haga clic en **Connect**. La etiqueta del botón cambia a **Disconnect** cuando está conectado.
7. Opcional: Active **Auto-connect on startup** para conectarse automáticamente al iniciar.

### Consola de RBN

- Vea el tráfico RBN sin procesar en el área de consola de solo lectura.
- Escriba comandos en el campo de texto junto a **Send** y haga clic en **Send** para transmitirlos.

### Color de los Spots de RBN

- Haga clic en **Spot Color:** para abrir un selector de color para los spots de RBN.

## Recibir Spots de WSJT-X

1. Haga clic en la pestaña **WSJT-X**.
2. Ingrese la dirección de enlace UDP en **Address:** (predeterminado: `127.0.0.1`).
3. Ingrese el puerto UDP en **Port:** (predeterminado: `2237`).
4. Haga clic en **Start**. La etiqueta del botón cambia a **Stop** cuando está escuchando.
5. Opcional: Active **Auto-start on startup** para iniciar el receptor automáticamente al iniciar.

### Filtros de WSJT-X

Seleccione qué decodificaciones aparecen como spots:

- **CQ** — Mostrar solo llamadas CQ.
- **CQ POTA** — Mostrar llamadas CQ POTA.
- **Calling Me** — Mostrar solo decodificaciones dirigidas a su indicativo.

### Colores de WSJT-X

Asigne colores a cada categoría de decodificación:

- **CQ color** — Haga clic para establecer el color de los spots CQ.
- **POTA color** — Haga clic para establecer el color de los spots CQ POTA.
- **Calling Me color** — Haga clic para establecer el color de los spots que lo llaman a usted.
- **Default color** — Haga clic para establecer el color predeterminado de todos los demás spots.

### Consola de Decodificaciones de WSJT-X

- Vea las transmisiones decodificadas en el área de solo lectura.

### Vida de los Spots

- Use el control **Spot Life:** para establecer cuántos segundos permanecen los spots de WSJT-X en el panadapter (predeterminado: 60 s).

## Conectarse a SpotCollector

1. Haga clic en la pestaña **SpotCollector**.
2. Ingrese el puerto UDP en **UDP Port:** (predeterminado: `7373`).
3. Haga clic en **Start**. La etiqueta del botón cambia a **Stop** cuando está escuchando.
4. Opcional: Active **Auto-start on startup** para iniciar el receptor automáticamente al iniciar.

### Consola de Spots de SpotCollector

- Vea los spots recibidos de SpotCollector en el área de solo lectura.

## Consultar Spots de POTA

1. Haga clic en la pestaña **POTA**.
2. El campo del servidor muestra **api.pota.app (HTTP polling)** — esto es fijo.
3. Establezca el **Poll Interval:** en segundos (predeterminado: `60`).
4. Haga clic en **Start**. La etiqueta del botón cambia a **Stop** cuando está consultando.
5. Opcional: Active **Auto-start on startup** para iniciar la consulta automáticamente al iniciar.

### Consola de Activaciones de POTA

- Vea el flujo de activaciones en el área de solo lectura.

### Color de los Spots de POTA

- Haga clic en **Spot Color:** para abrir un selector de color para los spots de POTA.

## Conectarse a FreeDV

1. Haga clic en la pestaña **FreeDV**.
2. El campo del servidor muestra **qso.freedv.org (WebSocket)** — esto es fijo.
3. Haga clic en **Start**. La etiqueta del botón cambia a **Stop** cuando está conectado.
4. Opcional: Active **Auto-start on startup** para conectarse automáticamente al iniciar.

### Consola de Spots de FreeDV

- Vea la actividad de FreeDV en el área de solo lectura.

### Color de los Spots de FreeDV

- Haga clic en **Spot Color:** para abrir un selector de color para los spots de FreeDV.

## Usar la Lista de Spots

1. Haga clic en la pestaña **Spot List** para ver todos los spots activos en una tabla unificada y ordenable.
2. Use las casillas de verificación de **Bands:** para filtrar por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). Las casillas de filtro de banda se ajustan a nuevas filas cuando el diálogo es estrecho para mantener las etiquetas legibles.
3. Haga clic en **Clear** para vaciar la lista de spots actual.
4. Haga doble clic en cualquier fila de la **Spot table** para sintonizar su radio a esa frecuencia.

Las columnas de la **Spot table** son:

| Columna | Descripción |
|---|---|
| Time | Hora en que se recibió el spot |
| Freq | Frecuencia en MHz |
| DX Call | La estación que está siendo reportada |
| Comment | Comentario del reportador |
| Spotter | La estación que publicó el spot |
| Band | Nombre de la banda |
| Mode | Modo (p. ej., CW, FT8, RTTY) |
| Source | Qué fuente proporcionó el spot (Cluster, RBN, WSJT-X, SpotCollector, POTA, FreeDV, EiBi, N1MM) |

Haga clic en cualquier encabezado de columna para ordenar por esa columna. Las columnas **Time** y **Freq** admiten ordenamiento; haga clic en **Time** para volver al orden del más reciente primero.

### Ocultar y mostrar columnas de la tabla

Haga clic con el botón derecho en la fila de encabezado de la tabla de spots para abrir un menú contextual donde puede mostrar u ocultar columnas individuales. El menú permanece abierto mientras alterna columnas marcables, de modo que puede mostrar u ocultar varias columnas en una sola pasada en lugar de reabrir el menú para cada columna.

## Configurar la Visualización de Spots

1. Haga clic en la pestaña **Display**.
2. Use los siguientes interruptores y controles:

### Interruptores Principales

| Control | Predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Spots:** | Habilitado | Interruptor principal para la superposición de spots DX | `IsSpotsEnabled` |
| **Memories:** | Deshabilitado | Alterna la superposición de canales de memoria en el panadapter | `IsMemorySpotsEnabled` |
| **Auto:** | Habilitado | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (p. ej., CW, FT8, RTTY) | `SpotAutoSwitchMode` |
| **Signals (Signal History)** | Deshabilitado | Marcadores dorados para señales detectadas de ancho de voz en el panadapter | `SHistoryMarkersEnabled` |
| **QRM (Signal History)** | Deshabilitado | Marcadores rojos para portadoras persistentes e interferencia de banda ancha | `SHistoryQrmEnabled` |

### Controles Globales

| Control | Predeterminado | Rango | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| **Clear All** | — | — | Borra todos los spots DX, el flujo de memoria, los marcadores de Signal History y los marcadores QRM del espectro | — |
| **Levels:** | 3 | 1–10 | Número de filas verticales apiladas para los spots | `SpotsMaxLevel` |
| **Position:** | 50 | 0–100 | Posición vertical en el panadapter | `SpotsStartingHeightPercentage` |
| **Font Size:** | 16 | 8–32 | Tamaño del texto de los spots | `SpotFontSize` |
| **Spot Lifetime:** | — | 10 seg – 24 hrs (pasos no lineales) | Segundos antes de que un spot se desvanezca | `DxClusterSpotLifetimeSec` |

### Anulaciones de Color

| Control | Predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Override Colors:** | Off | Fuerza un solo color de texto para todos los spots | `IsSpotsOverrideColorsEnabled` |
| Selector de color de texto de spot | `#FFFF00` | Abre un selector de color para elegir el color de texto de anulación | `SpotsOverrideColor` |
| **Override Background: Enabled** | Habilitado | Habilita un color de fondo personalizado para los spots | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** | Habilitado | Selecciona automáticamente el color de fondo para contraste | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo de spot | `#000000` | Abre un selector de color para el color de fondo de los spots | `SpotsOverrideBgColor` |
| **Background Opacity:** | 48 | 0–100 | Opacidad del color de fondo de los spots | `SpotsBackgroundOpacity` |

### Líneas de Spots

| Control | Predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Spot Lines:** | Habilitado | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Deshabilítelo durante concursos para reducir el desorden visual | `IsSpotsLinesEnabled` |

### Total de Spots

- El indicador **Total Spots:** muestra el conteo en vivo de spots actualmente rastreados en todas las fuentes.

## Coloración DXCC

En la pestaña **Display**, la sección **DXCC Coloring** controla el coloreado de spots según su registro.

1. Haga clic en **Load ADIF Log** para seleccionar un archivo de registro ADIF (usa la configuración `DxccAdifFilePath`).
2. Después de cargar, el indicador **Imported:** muestra `<N> QSOs / <M> entities`.

| Control | Predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|
| **DXCC Colors:** | Off | Colorea los spots según el estado DXCC trabajado/confirmado/necesario | `IsDxccColoringEnabled` |
| **Log File (ADIF):** | — | Abre el diálogo de archivo para seleccionar un registro ADIF. Vigila automáticamente el archivo en busca de cambios | `DxccAdifFilePath` |
| **Imported:** | (sin registro cargado) | Muestra el conteo de QSO y el conteo de entidades | — |

### Configuración de Colores DXCC

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Muestra de color New DXCC | Abre un selector de color para spots de entidades nuevas | `DxccColorNewEntity` |
| Muestra de color New Band | Abre un selector de color para spots de bandas nuevas | `DxccColorNewBand` |
| Muestra de color New Mode | Abre un selector de color para spots de modos nuevos | `DxccColorNewMode` |
| Muestra de color Worked | Abre un selector de color para spots ya trabajados | `DxccColorWorked` |

## Signal History

En la pestaña **Display**, la sección **Signal History** configura marcadores para señales de ancho de voz y QRM.

| Control | Predeterminado | Rango | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| **Signals (Signal History)** | Deshabilitado | On/Off | Marcadores dorados para señales detectadas de ancho de voz | `SHistoryMarkersEnabled` |
| **QRM (Signal History)** | Deshabilitado | On/Off | Marcadores rojos para portadoras persistentes e interferencia de banda ancha | `SHistoryQrmEnabled` |
| **Marker Lifetime:** | 60 | 15–300 seg | Cuánto tiempo persiste un marcador inactivo de Signal History antes de eliminarse | `SHistoryLifetimeS` |
| **QRM Gate:** | 6 | 3–30 seg | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de clasificarse como QRM | `SHistoryQrmGateS` |
| **Edge Threshold:** | 3.0 | 1.0–10.0 dB | Umbral sobre el piso de ruido para el recorrido de borde de pendiente que refina el borde del lado de la portadora del S-History. Más bajo = más cerca de la portadora pero más sensible al ruido | `SHistorySoftEdgeDb` |
| **Snap to Step:** | Deshabilitado | On/Off | Redondea el clic-para-sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de la portadora | `SHistorySnapToStep` |

### Configuración de Colores de Signal History

| Control | Predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|
| Muestra de color Signals | `#FFC800` | Abre un selector de color para marcadores de señales de voz (dorado) | `SHistoryColorSignals` |
| Muestra de color QRM | `#FF0000` | Abre un selector de color para marcadores QRM (rojo) | `SHistoryColorQrm` |

## Consejos

- Todos los controles deslizantes admiten **doble clic izquierdo** para restablecer su valor predeterminado almacenado.
- El diálogo de SpotHub usa los colores de su tema actual para las etiquetas de estado y el estilo de las pestañas. El estado conectado aparece en el color de acento, el desconectado en el color de etiqueta y los mensajes de error en el color de acento de peligro.
- Las casillas de filtro de banda de la Spot List se ajustan a nuevas filas cuando el diálogo es estrecho, manteniendo las etiquetas legibles (#4157).
- Haga clic con el botón derecho en el encabezado de la tabla de la Spot List para mostrar/ocultar columnas; el menú permanece abierto mientras alterna varias columnas en una sola pasada (#4157).
- Snap to Step solo afecta los clics en los marcadores de Signal History — no cambia la forma en que el slice sintoniza cuando hace clic directamente en el espectro.
- Haga clic en el encabezado de la columna **Time** en la Spot List para volver al orden del más reciente primero después de ordenar por otra columna (#4749).

## Solución de Problemas

- **Las casillas de
