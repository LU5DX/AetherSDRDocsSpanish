# Descripción general de Diagnóstico de Red

El cuadro de diálogo Diagnóstico de Red le ofrece una vista en vivo, actualizada cada segundo, del enlace de red entre AetherSDR y su FLEX-8600. Úselo para confirmar los puntos finales de la conexión, medir la latencia, inspeccionar las tasas de datos por flujo, diagnosticar problemas de búfer de audio y monitorear el registro de la aplicación.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El cuadro de diálogo se puede abrir haya o no una radio conectada, pero la mayoría de los indicadores estarán vacíos hasta que se establezca una conexión.

## Cómo funciona

Abra el cuadro de diálogo con `Settings > Network...`. Todos los indicadores se actualizan automáticamente una vez por segundo. Haga clic en Close cuando termine.

El cuadro de diálogo utiliza un panel de navegación en árbol a la izquierda y un área de contenido a la derecha. Hay siete páginas disponibles: **Overview**, **Details**, **Latency**, **Rates**, **Packet Loss**, **Audio** y **Logs**. Haga clic en cualquier elemento del árbol de navegación para abrir esa página. Un campo de **Search** en la parte superior del panel de navegación le permite filtrar los elementos del árbol por nombre. Un selector de **Timeframe** en la esquina superior derecha controla cuánto tiempo hacia atrás muestran el historial los gráficos de series temporales; está oculto cuando la página Logs está activa.

El cuadro de diálogo recuerda la geometría de su ventana entre sesiones. La posición y el tamaño se guardan al cerrar el diálogo y se restauran la próxima vez que se abre.

La página Details organiza todos los indicadores etiquetados en los cuatro grupos que se describen a continuación.

### Estado de la red

Ruta de conexión y latencia TCP. Confirma qué ruta está utilizando AetherSDR para llegar a la radio.

| Indicador | Qué muestra |
|---|---|
| Status | Calidad general del enlace, codificada por colores verde → rojo. Estados posibles: Excellent, Very Good, Good, Fair, Poor. |
| Target Radio IP | Dirección IP de la radio conectada. Muestra "Not connected" cuando no hay ninguna radio vinculada. |
| Selected Source | Interfaz de red local o ruta de enlace utilizada para la conexión. |
| Local TCP | Punto final TCP local (dirección y puerto). |
| Local UDP | Punto final UDP local (dirección y puerto). |
| First UDP Packet | Indica si se ha recibido el primer paquete UDP desde la conexión ("Yes" o "No"). |
| Latency (RTT) | Tiempo de ida y vuelta actual en milisegundos. Muestra "< 1 ms" cuando es inferior a 1 ms. |
| Max Latency (RTT) | RTT más alto medido desde que la radio se conectó. |

### Tasas de flujo entrantes

Tasas de ingreso por categoría y totales agregados. Las grandes oscilaciones indican una entrega irregular incluso cuando no se pierden paquetes.

| Indicador | Qué muestra |
|---|---|
| Audio | Tasa del flujo de audio entrante en kbps. |
| FFT | Tasa del flujo FFT entrante en kbps. |
| Waterfall | Tasa del flujo de waterfall entrante en kbps. |
| Meters | Tasa del flujo de medidores entrante en kbps. |
| DAX | Tasa del flujo DAX entrante en kbps. |
| Total RX | Tasa agregada entrante en todos los flujos en kbps. |
| Total TX | Tasa agregada saliente en kbps. |

### Pérdida de paquetes (Saltos de secuencia)

Conteos de pérdidas inferidos a partir de números de secuencia VITA faltantes. Un conteo cero aquí no descarta la fluctuación (jitter) o las ráfagas de entrega tardía.

| Indicador | Qué muestra |
|---|---|
| Audio | Paquetes perdidos / paquetes totales (porcentaje) para el flujo de audio. |
| FFT | Paquetes perdidos / paquetes totales (porcentaje) para el flujo FFT. |
| Waterfall | Paquetes perdidos / paquetes totales (porcentaje) para el flujo de waterfall. |
| Meters | Paquetes perdidos / paquetes totales (porcentaje) para el flujo de medidores. |
| DAX | Paquetes perdidos / paquetes totales (porcentaje) para el flujo DAX. |

### Reproducción de audio

Salud del búfer del lado del altavoz. Si los desbordamientos (underruns) aumentan mientras el búfer se mantiene cerca de cero, la reproducción se está quedando sin datos. El intervalo de llegada y la fluctuación miden la temporización, no la pérdida de paquetes.

| Indicador | Qué muestra |
|---|---|
| RX Buffer Now | Llenado actual del búfer de recepción de audio, en bytes y milisegundos. |
| RX Buffer Peak | Llenado más alto del búfer visto desde la conexión, en bytes y milisegundos. |
| Underruns (total) | Conteo acumulado de desbordamientos del búfer de audio desde la conexión. |
| Underruns (last sec) | Desbordamientos del búfer de audio que ocurrieron en el intervalo de un segundo más reciente. |
| Audio Arrival Gap | Intervalo de tiempo entre paquetes de audio entrantes consecutivos. |
| Max Arrival Gap | Intervalo de llegada más grande visto desde la conexión. |
| Network Jitter | Estimación suavizada de la fluctuación (jitter) del flujo de audio entrante. |

## Controles

| Control                  | Comportamiento                                                                                                                                                                                                                    | Notas                                                                                                  |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| Navigation tree          | Panel de árbol en el lado izquierdo del cuadro de diálogo. Haga clic en cualquier nombre de página para abrir esa página. Los elementos son: Overview, Details, Latency, Rates, Packet Loss, Audio, Logs.                         | Reemplaza la barra de pestañas anterior.                                                               |
| Search                   | Filtra los elementos del árbol de navegación por nombre a medida que escribe.                                                                                                                                                     | Ubicado sobre el árbol de navegación.                                                                  |
| Overview (page)          | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).                                  |                                                                                                        |
| Details (page)           | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                                                                                |                                                                                                        |
| Latency (page)           | Gráfico de series temporales a ancho completo de RTT, intervalo de llegada y fluctuación (jitter) en ms.                                                                                                                           |                                                                                                        |
| Rates (page)             | Gráfico de series temporales a ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.                                                              |                                                                                                        |
| Packet Loss (page)       | Gráfico de series temporales a ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.                                                                                                                        |                                                                                                        |
| Audio (page)             | Gráfico de series temporales a ancho completo del llenado del búfer de reproducción (ms) y desbordamientos/s. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y estado del flujo para cada flujo de audio activo. | v26.5.3 (#2889): diagnósticos RX por flujo expuestos en el paquete de soporte y en la vista detallada de esta página. |
| Logs (page)              | Seguimiento en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría.                                                  | El selector de Timeframe está oculto mientras esta página está activa.                                  |
| Timeframe                | Selecciona cuánto tiempo hacia atrás muestran el historial los gráficos de series temporales. El valor predeterminado es 5 minutos. Opciones disponibles: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week.                  | Se muestra en la esquina superior derecha del área de la página; oculto cuando la página Logs está activa. |
| Filter Categories (Logs) | Casillas de verificación por categoría que filtran la vista del registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager.                                                       |                                                                                                        |
| Select All (Logs)        | Muestra todas las categorías de registro en el visor.                                                                                                                                                                             |                                                                                                        |
| Deselect All (Logs)      | Oculta todas las categorías de registro del visor.                                                                                                                                                                                |                                                                                                        |
| Live / Paused (Logs)     | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final.                                                    | El estado predeterminado es Live.                                                                      |
| Close                    | Cierra el cuadro de diálogo.                                                                                                                                                                                                      |                                                                                                        |

## Página Logs

La página Logs sigue el archivo de registro de AetherSDR en tiempo real. La ruta completa del archivo que se está siguiendo se muestra en la etiqueta de ruta de registro en la parte superior de la página.

Las líneas de registro tienen resaltado de sintaxis por nivel de registro (DBG, INF, WRN, CRT, FTL) y por nombre de categoría. Use las casillas de verificación **Filter Categories** para limitar la salida a las categorías que le interesen. Haga clic en **Select All** para restaurar todas las categorías o en **Deselect All** para limpiar la vista. La alternancia **Live / Paused** controla el desplazamiento automático: desplazarse hacia arriba pausa la vista automáticamente; haga clic en **Live** para reanudar y saltar a la salida más reciente.

## Consejos

- El cuadro de diálogo puede permanecer abierto mientras opera. Todos los valores se actualizan cada segundo sin necesidad de interacción.
- El cuadro de diálogo guarda y restaura la posición y el tamaño de su ventana entre sesiones. Si prefiere una disposición diferente, cambie el tamaño y la posición del diálogo antes de cerrarlo.
- Los conteos de pérdida de paquetes en el grupo Packet Loss son acumulativos desde que se abrió el cuadro de diálogo; ciérrelo y vuélvalo a abrir para restablecer la línea base.
- Una pérdida de paquetes de cero combinada con desbordamientos crecientes apunta a un problema de fluctuación (jitter) o temporización, más que a una pérdida directa: verifique Audio Arrival Gap y Network Jitter en ese caso.
- En la página Rates, el eje Y utiliza una escala logarítmica, lo que facilita ver flujos de baja tasa (como Meters) junto con el total RX mucho más alto.

## Relacionado

- [Verify the radio's IP and local bind address](verify-the-radio-s-ip-and-local-bind-address.md)
- [Measure RTT and packet drops during audio problems](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnose audio underruns and jitter](../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Watch the first-UDP-packet timestamp after connect](../../getting-started/setup/watch-the-first-udp-packet-timestamp-after-connect.md)
