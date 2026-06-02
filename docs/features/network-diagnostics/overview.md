# Resumen de Diagnósticos de Red

El cuadro de diálogo de Diagnósticos de Red le ofrece una vista en vivo, actualizada cada segundo, del enlace de red entre AetherSDR y su FLEX-8600. Úselo para confirmar los puntos de conexión, medir la latencia, inspeccionar las tasas de datos por flujo, diagnosticar problemas en el búfer de audio y monitorear el registro de la aplicación.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El cuadro de diálogo se puede abrir incluso si no hay una radio conectada, pero la mayoría de los indicadores estarán vacíos hasta que se establezca una conexión.

## Cómo funciona

Abra el cuadro de diálogo con `Settings > Network...`. Todos los indicadores se actualizan automáticamente una vez por segundo. Haga clic en Close cuando termine.

El cuadro de diálogo utiliza un diseño de pestañas. Hay siete pestañas disponibles: **Overview**, **Details**, **Latency**, **Rates**, **Packet Loss**, **Audio** y **Logs**. Un selector **Timeframe** en la esquina superior derecha de la barra de pestañas controla cuánto tiempo atrás muestran el historial los gráficos de series temporales; está oculto cuando la pestaña Logs está activa.

El cuadro de diálogo recuerda la geometría de su ventana entre sesiones. La posición y el tamaño se guardan al cerrar el diálogo y se restauran la próxima vez que se abre.

La pestaña Details organiza todos los indicadores etiquetados en cuatro grupos, descritos a continuación.

### Estado de la Red

Ruta de conexión y latencia TCP. Confirma qué ruta está usando AetherSDR para llegar a la radio.

| Indicador | Qué muestra |
|---|---|
| Status | Calidad general del enlace, codificada por color verde → rojo. Estados posibles: Excellent, Very Good, Good, Fair, Poor. |
| Target Radio IP | Dirección IP de la radio conectada. Muestra "Not connected" cuando no hay ninguna radio vinculada. |
| Selected Source | Interfaz de red local o ruta de enlace utilizada para la conexión. |
| Local TCP | Punto final TCP local (dirección y puerto). |
| Local UDP | Punto final UDP local (dirección y puerto). |
| First UDP Packet | Indica si el primer paquete UDP se ha recibido desde la conexión ("Yes" o "No"). |
| Latency (RTT) | Tiempo de ida y vuelta actual en milisegundos. Muestra "< 1 ms" cuando es inferior a 1 ms. |
| Max Latency (RTT) | RTT más alto medido desde que la radio se conectó. |

### Tasas de Flujo de Entrada

Taxas de ingreso por categoría y totales agregados. Las grandes fluctuaciones indican una entrega irregular incluso cuando no se pierden paquetes.

| Indicador | Qué muestra |
|---|---|
| Audio | Tasa del flujo de audio entrante en kbps. |
| FFT | Tasa del flujo FFT entrante en kbps. |
| Waterfall | Tasa del flujo de waterfall entrante en kbps. |
| Meters | Tasa del flujo de medidores entrante en kbps. |
| DAX | Tasa del flujo DAX entrante en kbps. |
| Total RX | Tasa agregada de entrada en todos los flujos en kbps. |
| Total TX | Tasa agregada de salida en kbps. |

### Pérdida de Paquetes (Huecos de Secuencia)

Conteos de pérdida inferidos a partir de números de secuencia VITA faltantes. Un conteo de cero aquí no descarta la fluctuación de fase o ráfagas de entrega tardía.

| Indicador | Qué muestra |
|---|---|
| Audio | Paquetes perdidos / paquetes totales (porcentaje) para el flujo de audio. |
| FFT | Paquetes perdidos / paquetes totales (porcentaje) para el flujo FFT. |
| Waterfall | Paquetes perdidos / paquetes totales (porcentaje) para el flujo de waterfall. |
| Meters | Paquetes perdidos / paquetes totales (porcentaje) para el flujo de medidores. |
| DAX | Paquetes perdidos / paquetes totales (porcentaje) para el flujo DAX. |

### Reproducción de Audio

Salud del búfer del lado del altavoz. Si los subdesbordamientos aumentan mientras el búfer se mantiene cerca de cero, la reproducción está sufriendo de falta de datos. La brecha de llegada y la fluctuación miden la temporización, no la pérdida de paquetes.

| Indicador | Qué muestra |
|---|---|
| RX Buffer Now | Llenado actual del búfer de recepción de audio, en bytes y milisegundos. |
| RX Buffer Peak | Llenado máximo del búfer observado desde la conexión, en bytes y milisegundos. |
| Underruns (total) | Conteo acumulativo de subdesbordamientos del búfer de audio desde la conexión. |
| Underruns (last sec) | Subdesbordamientos del búfer de audio que ocurrieron en el intervalo de un segundo más reciente. |
| Audio Arrival Gap | Brecha de tiempo entre paquetes de audio entrantes consecutivos. |
| Max Arrival Gap | Brecha de llegada más grande observada desde la conexión. |
| Network Jitter | Estimación suavizada de la fluctuación de fase de la red para el flujo de audio entrante. |

## Controles

| Control                  | Comportamiento                                                                                                                                                                                                                                                                                    | Notas                                                                                                   |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| Overview (pestaña)       | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).                                                                                                  |                                                                                                         |
| Details (pestaña)        | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                                                                                                                                              |                                                                                                         |
| Latency (pestaña)        | Gráfico de series temporales a ancho completo del RTT, la brecha de llegada y la fluctuación en ms.                                                                                                                                                                                              |                                                                                                         |
| Rates (pestaña)          | Gráfico de series temporales a ancho completo en escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.                                                                                                                              |                                                                                                         |
| Packet Loss (pestaña)    | Gráfico de series temporales a ancho completo del % de pérdida de paquetes por categoría de flujo.                                                                                                                                                                                              |                                                                                                         |
| Audio (pestaña)          | Gráfico de series temporales a ancho completo del llenado del búfer de reproducción (ms) y subdesbordamientos/s. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, el déficit, los paquetes tardíos, el código de clase de paquete y el estado del flujo para cada flujo de audio activo. | v26.5.3 (#2889): los diagnósticos RX por flujo se exponen en el paquete de soporte y en la vista de detalle de esta pestaña. |
| Logs (pestaña)           | Seguimiento en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría.                                                                                                                | El selector Timeframe está oculto mientras esta pestaña está activa.                                  |
| Timeframe                | Selecciona cuánto tiempo atrás muestran el historial los gráficos de series temporales. El valor predeterminado es 5 minutos. Opciones disponibles: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week.                                                                                     | Se muestra en la esquina superior derecha de la barra de pestañas; oculto cuando la pestaña Logs está activa. |
| Filter Categories (Logs) | Casillas de verificación por categoría para filtrar la vista del registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager.                                                                                                                    |                                                                                                         |
| Select All (Logs)        | Muestra todas las categorías de registro en el visor.                                                                                                                                                                                                                                             |                                                                                                         |
| Deselect All (Logs)      | Oculta todas las categorías de registro del visor.                                                                                                                                                                                                                                                |                                                                                                         |
| Live / Paused (Logs)     | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final.                                                                                                                | El estado predeterminado es Live.                                                                       |
| Close                    | Cierra el cuadro de diálogo.                                                                                                                                                                                                                                                                      |                                                                                                         |

## Pestaña Logs

La pestaña Logs realiza un seguimiento en tiempo real del archivo de registro de AetherSDR. La ruta completa del archivo en seguimiento se muestra en la etiqueta de ruta de registro en la parte superior de la pestaña.

Las líneas de registro se resaltan por sintaxis según el nivel de registro (DBG, INF, WRN, CRT, FTL) y el nombre de la categoría. Use las casillas de verificación **Filter Categories** para limitar la salida a las categorías que le interesen. Haga clic en **Select All** para restaurar todas las categorías o en **Deselect All** para limpiar la vista. El conmutador **Live / Paused** controla el desplazamiento automático: desplazarse hacia arriba pausa la vista automáticamente; haga clic en **Live** para reanudar y saltar a la salida más reciente.

## Consejos

- El cuadro de diálogo puede permanecer abierto mientras usted opera. Todos los valores se actualizan cada segundo sin necesidad de interacción.
- El cuadro de diálogo guarda y restaura la posición y el tamaño de su ventana entre sesiones. Si prefiere un diseño diferente, cambie el tamaño y la posición del diálogo antes de cerrarlo.
- Los conteos de pérdida de paquetes en el grupo Packet Loss son acumulativos desde que se abrió el diálogo; ciérrelo y ábralo de nuevo para restablecer la línea de base.
- Cero pérdida de paquetes combinado con subdesbordamientos crecientes apunta a un problema de fluctuación o temporización en lugar de una pérdida directa; en ese caso, revise Audio Arrival Gap y Network Jitter.
- En la pestaña Rates, el eje y utiliza una escala logarítmica, lo que facilita ver flujos de baja tasa (como Meters) junto con la tasa RX total mucho más alta.

## Relacionados

- [Verify the radio's IP and local bind address](verify-the-radio-s-ip-and-local-bind-address.md)
- [Measure RTT and packet drops during audio problems](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnose audio underruns and jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Watch the first-UDP-packet timestamp after connect](../../getting-started/setup/watch-the-first-udp-packet-timestamp-after-connect.md)
