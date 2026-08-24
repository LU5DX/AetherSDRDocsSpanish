# Descripción general de Diagnóstico de red

El cuadro de diálogo Diagnóstico de red le ofrece una vista en vivo, actualizada cada segundo, del enlace de red entre AetherSDR y su FLEX-8600. Úselo para confirmar los puntos finales de conexión, medir la latencia, inspeccionar las tasas de datos por flujo, diagnosticar problemas de búfer de audio y revisar el registro de la aplicación.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El cuadro de diálogo se puede abrir tanto si hay una radio conectada como si no, pero la mayoría de los indicadores estarán vacíos hasta que se establezca una conexión.

## Cómo funciona

Abra el cuadro de diálogo con `Settings > Network...`. Todos los indicadores se actualizan automáticamente una vez por segundo. Haga clic en Close cuando haya terminado.

El cuadro de diálogo utiliza un panel de navegación de árbol a la izquierda y un área de contenido a la derecha. Hay ocho páginas disponibles: **Overview**, **Connection Details**, **Latency**, **Rates**, **Packet Loss**, **Audio**, **Logs** y **TCI Clients**. Haga clic en cualquier elemento del árbol de navegación para abrir esa página. Un campo **Search** en la parte superior del panel de navegación le permite filtrar los elementos del árbol por nombre. Un selector **Timeframe** en la esquina superior derecha controla cuánto tiempo hacia atrás muestran el historial los gráficos de series temporales; está oculto cuando la página Logs o TCI Clients está activa.

El cuadro de diálogo recuerda la geometría de su ventana entre sesiones. La posición y el tamaño se guardan al cerrar el cuadro de diálogo y se restauran la próxima vez que se abra.

La página Connection Details organiza todos los indicadores etiquetados en cinco grupos que se describen a continuación.

### Estado de la red

Ruta de conexión y latencia TCP. Confirma qué ruta está utilizando AetherSDR para llegar a la radio.

| Indicador | Qué muestra |
|---|---|
| Status | Calidad general del enlace, codificada por colores de verde a rojo. Estados posibles: Excellent, Very Good, Good, Fair, Poor. |
| Target Radio IP | Dirección IP de la radio conectada. Muestra "Not connected" cuando no hay ninguna radio vinculada. |
| Selected Source | Interfaz de red local o ruta de enlace utilizada para la conexión. |
| Local TCP | Punto final TCP local (dirección y puerto). |
| Local UDP | Punto final UDP local (dirección y puerto). |
| First UDP Packet | Si se ha recibido el primer paquete UDP desde la conexión ("Yes" o "No"). |
| Latency (RTT) | Tiempo de ida y vuelta actual en milisegundos. Muestra "< 1 ms" cuando es inferior a 1 ms. Muestra "not measured on this link" cuando el transporte conectado no tiene un tiempo de ida y vuelta que medir. |
| Max Latency (RTT) | RTT más alto medido desde que se conectó la radio. Muestra "not measured on this link" cuando el transporte conectado no tiene un tiempo de ida y vuelta que medir. |

### Tasas de flujo entrante

Tasas de entrada por categoría y totales agregados. Grandes variaciones indican entrega intermitente incluso cuando no se descartan paquetes.

| Indicador | Qué muestra |
|---|---|
| Audio | Tasa de flujo de audio entrante en kbps. Muestra "n/a" cuando el transporte conectado no proporciona estadísticas por categoría de flujo. |
| FFT | Tasa de flujo FFT entrante en kbps. Muestra "n/a" cuando el transporte conectado no proporciona estadísticas por categoría de flujo. |
| Waterfall | Tasa de flujo de waterfall entrante en kbps. Muestra "n/a" cuando el transporte conectado no proporciona estadísticas por categoría de flujo. |
| Meters | Tasa de flujo de medidores entrante en kbps. Muestra "n/a" cuando el transporte conectado no proporciona estadísticas por categoría de flujo. |
| DAX | Tasa de flujo DAX entrante en kbps. Muestra "n/a" cuando el transporte conectado no proporciona estadísticas por categoría de flujo. |
| Total RX | Tasa agregada de entrada en todos los flujos en kbps. |
| Total TX | Tasa agregada de salida en kbps. |

### Limitación adaptativa de velocidad de fotogramas

Muestra el estado de la limitación adaptativa que reduce las velocidades de fotogramas del panadapter cuando se detecta latencia o pérdida. Esta sección está oculta hasta que haya datos de limitación disponibles.

| Indicador | Qué muestra |
|---|---|
| Current State | El estado actual de la limitación. |
| Pending Lift | Si la limitación está pendiente de anularse. |
| Sessions This Run | Número de sesiones de limitación desde que se conectó la radio. |

### Pérdida de paquetes (huecos de secuencia)

Conteos de pérdida inferidos de números de secuencia VITA faltantes. Un conteo de cero aquí no descarta ráfagas de fluctuación o entrega tardía.

| Indicador | Qué muestra |
|---|---|
| Audio | Paquetes perdidos / paquetes totales (porcentaje) del flujo de audio. Muestra "n/a" cuando el transporte conectado no proporciona estadísticas por categoría de flujo. |
| FFT | Paquetes perdidos / paquetes totales (porcentaje) del flujo FFT. Muestra "n/a" cuando el transporte conectado no proporciona estadísticas por categoría de flujo. |
| Waterfall | Paquetes perdidos / paquetes totales (porcentaje) del flujo de waterfall. Muestra "n/a" cuando el transporte conectado no proporciona estadísticas por categoría de flujo. |
| Meters | Paquetes perdidos / paquetes totales (porcentaje) del flujo de medidores. Muestra "n/a" cuando el transporte conectado no proporciona estadísticas por categoría de flujo. |
| DAX | Paquetes perdidos / paquetes totales (porcentaje) del flujo DAX. Muestra "n/a" cuando el transporte conectado no proporciona estadísticas por categoría de flujo. |

### Reproducción de audio

Salud del búfer del lado del altavoz. Si los underruns aumentan mientras el búfer permanece cerca de cero, la reproducción se está quedando sin datos. El intervalo de llegada y la fluctuación miden la sincronización, no la pérdida de paquetes.

| Indicador | Qué muestra |
|---|---|
| RX Buffer Now | Relleno actual del búfer de recepción de audio, en bytes y milisegundos. |
| RX Buffer Peak | Relleno más alto del búfer visto desde la conexión, en bytes y milisegundos. |
| Underruns (total) | Conteo acumulado de underruns del búfer de audio desde la conexión. |
| Underruns (last sec) | Underruns del búfer de audio que ocurrieron en el intervalo de un segundo más reciente. |
| Audio Arrival Gap | Intervalo de tiempo entre paquetes de audio entrantes consecutivos. Muestra "not measured on this link" cuando el transporte conectado no proporciona mediciones de sincronización de entrega. |
| Max Arrival Gap | Intervalo de llegada más grande visto desde la conexión. Muestra "not measured on this link" cuando el transporte conectado no proporciona mediciones de sincronización de entrega. |
| Network Jitter | Estimación suavizada de la fluctuación del flujo de audio entrante. Muestra "not measured on this link" cuando el transporte conectado no proporciona mediciones de sincronización de entrega. |

## Controles

| Control | Comportamiento | Notas |
|---|---|---|
| Árbol de navegación | Panel de árbol en el lado izquierdo del cuadro de diálogo. Haga clic en cualquier nombre de página para abrirla. Los elementos son: Overview, Connection Details, Latency, Rates, Packet Loss, Audio, Logs, TCI Clients. | Reemplaza la barra de pestañas anterior. |
| Search | Filtra los elementos del árbol de navegación por nombre mientras escribe. | Ubicado sobre el árbol de navegación. |
| Overview (tab) | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). | |
| Connection Details (page) | Cuadrícula desplazable con valores etiquetados para Network Status, Incoming Stream Rates, Packet Loss, Audio Playback y la subsección Adaptive Frame-Rate Throttle. | Renombrado de 'Details' en la reorganización de navegación por árbol de v26.8.4. Incluye una acción Read-Only Clipboard Copy para copiar todo el resumen de diagnóstico. Los labs con estadísticas por categoría de flujo se muestran como "n/a" cuando no están disponibles. |
| Adaptive Frame-Rate Throttle (section) | Muestra los valores Current State, Pending Lift y Sessions This Run de la limitación adaptativa. Reduce las velocidades de fotogramas del panadapter cuando se detecta latencia o pérdida. | Nuevo en v26.8.4. Oculto hasta que haya datos de limitación disponibles. |
| Latency (tab) | Gráfico de series temporales de ancho completo de RTT, intervalo de llegada y fluctuación en ms. | La traza RTT se omite por completo cuando el transporte conectado no tiene un tiempo de ida y vuelta que medir. |
| Rates (tab) | Gráfico de series temporales de ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps. | |
| Packet Loss (tab) | Gráfico de series temporales de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo. | |
| Audio (tab) | Gráfico de series temporales de ancho completo del relleno del búfer de reproducción (ms) y underruns/s. Incluye diagnósticos de audio RX por flujo que muestran tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y salud del flujo para cada flujo de audio activo. | v26.5.3 (#2889): diagnósticos RX por flujo expuestos en el paquete de soporte y en la vista de detalle de esta pestaña. |
| Logs (tab) | Seguimiento en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. | El selector Timeframe está oculto mientras esta página está activa. |
| TCI Clients (page) | Lista los clientes TCI conectados con un monitor de tráfico en vivo (Pause/Save log/Clear), controles de supresión de comandos de respuesta y detalles por cliente. | Nuevo en v26.8.4. Compilación controlada por HAVE_TCI / soporte TCI. El selector Timeframe está oculto en esta página. |
| Timeframe | Selecciona cuánto tiempo hacia atrás muestran el historial los gráficos de series temporales. El valor predeterminado es 5 minutos. Opciones disponibles: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week. | Se muestra en la esquina superior derecha del área de la página; oculto cuando la página Logs o TCI Clients está activa. |
| Filter Categories (Logs) | Casillas de verificación por categoría que filtran la vista de registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager. | |
| Select All (Logs) | Muestra todas las categorías de registro en el visor. | |
| Deselect All (Logs) | Oculta todas las categorías de registro del visor. | |
| Live / Paused (Logs) | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final. | El estado predeterminado es Live. |
| Close | Cierra el cuadro de diálogo. | |

## Página Logs

La página Logs sigue el archivo de registro de AetherSDR en tiempo real. La ruta completa del archivo que se está siguiendo se muestra en la etiqueta de ruta de registro en la parte superior de la página.

Las líneas de registro tienen resaltado de sintaxis por nivel de registro (DBG, INF, WRN, CRT, FTL) y por nombre de categoría. Use las casillas de verificación **Filter Categories** para limitar la salida a las categorías que le interesan. Haga clic en **Select All** para restaurar todas las categorías o en **Deselect All** para limpiar la vista. El conmutador **Live / Paused** controla el desplazamiento automático: desplazarse hacia arriba pausa la vista automáticamente; haga clic en **Live** para reanudar y saltar a la salida más reciente.

## Página TCI Clients

La página TCI Clients enumera todos los clientes TCI conectados a la radio, con detalles por cliente. Un monitor de tráfico muestra el tráfico TCI en vivo; use **Pause** para congelarlo, **Save log** para escribirlo en un archivo y **Clear** para restablecerlo. Los controles de supresión de comandos de respuesta le permiten ajustar cómo responde AetherSDR a los comandos de los clientes TCI.

Esta página solo está disponible en compilaciones con soporte TCI (HAVE_TCI). El selector Timeframe está oculto mientras esta página está activa.

## Consejos

- El cuadro de diálogo puede permanecer abierto mientras opera. Todos los valores se actualizan cada segundo sin necesidad de interacción.
- El cuadro de diálogo guarda y restaura la posición y el tamaño de su ventana entre sesiones. Si prefiere un diseño diferente, redimensione y reposicione el cuadro de diálogo antes de cerrarlo.
- Los conteos de pérdida de paquetes en el grupo Packet Loss son acumulativos desde que se abrió el cuadro de diálogo; ciérrelo y vuelva a abrirlo para restablecer la línea base.
- Cero pérdida de paquetes combinado con underruns crecientes indica un problema de fluctuación o sincronización en lugar de pérdida absoluta: revise Audio Arrival Gap y Network Jitter en ese caso.
- En la página Rates, el eje y utiliza una escala logarítmica, lo que facilita ver flujos de baja tasa (como Meters) junto al total RX mucho más alto.
- Cuando el transporte conectado no proporciona un tiempo de ida y vuelta ni estadísticas por categoría de flujo, los indicadores relevantes muestran "not measured on this link" o "n/a" en lugar de "0" — esto distingue "no se tomó medida" de "medida cero", por lo que un transporte que no puede producir una cifra determinada no se confunde con uno perfectamente saludable.

## Relacionados

- [Verify the radio's IP and local bind address](verify-the-radio-s-ip-and-local-bind-address.md)
- [Measure RTT and packet drops during audio problems](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- Diagnosticar underruns de audio y fluctuación
- [Watch the first-UDP-packet timestamp after connect](../../getting-started/setup/watch-the-first-udp-packet-timestamp-after-connect.md)
