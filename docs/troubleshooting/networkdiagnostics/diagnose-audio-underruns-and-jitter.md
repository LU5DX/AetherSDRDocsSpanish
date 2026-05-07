# Diagnosticar subejecuciones de audio y fluctuación (jitter)

Utilice el cuadro de diálogo Network Diagnostics para leer el estado del búfer de audio en vivo, los recuentos de subejecuciones, el intervalo de llegada de paquetes y las estimaciones de fluctuación. Esto le ayuda a identificar si las interrupciones de audio son causadas por un búfer vacío, una entrega irregular de paquetes o fluctuación de la red.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El cuadro de diálogo no requiere una conexión de radio activa, pero los indicadores de audio solo son significativos mientras una radio está conectada y transmitiendo audio.
- Reproduzca el problema de audio antes de abrir el cuadro de diálogo para que los contadores y los valores máximos reflejen la condición de falla.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el cuadro de diálogo Network Diagnostics.
2. Localice el grupo **Audio Playback** en el área inferior derecha del cuadro de diálogo.
3. Lea **RX Buffer Now** para ver cuántos bytes (y milisegundos) de audio se mantienen actualmente en el búfer de reproducción.
4. Lea **RX Buffer Peak** para ver el nivel máximo de llenado del búfer registrado desde que se abrió el cuadro de diálogo.
5. Lea **Underruns (total)** para ver el recuento acumulativo de subejecuciones del búfer desde que se inició el motor de audio.
6. Lea **Underruns (last sec)** para ver cuántas subejecuciones ocurrieron en el intervalo de un segundo más reciente. Un valor distinto de cero aquí mientras el audio se está transmitiendo activamente indica un problema continuo.
7. Lea **Audio Arrival Gap** para ver el intervalo actual de llegada entre paquetes. Un valor significativamente mayor que el período de paquete esperado indica una entrega irregular.
8. Lea **Max Arrival Gap** para ver el intervalo de llegada máximo registrado desde que se abrió el cuadro de diálogo.
9. Lea **Network Jitter** para ver la estimación suavizada de fluctuación de la red para el flujo de audio.
10. Si las subejecuciones están aumentando pero **RX Buffer Now** se mantiene cerca de cero, el búfer se está vaciando — consulte los consejos a continuación.
11. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Indicador                 | Significado                                                                                                                                                                              | Notas                                                                             |
|---------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| **RX Buffer Now**         | Nivel actual de llenado del búfer de audio, mostrado en bytes y milisegundos.                                                                                                            |                                                                                   |
| **RX Buffer Peak**        | Nivel máximo de llenado del búfer registrado desde que se abrió el cuadro de diálogo.                                                                                                   |                                                                                   |
| **Underruns (total)**     | Recuento acumulativo de subejecuciones del búfer de audio desde que se inició el motor de audio.                                                                                        |                                                                                   |
| **Underruns (last sec)**  | Número de subejecuciones que ocurrieron en el último intervalo de un segundo.                                                                                                            |                                                                                   |
| **Audio Arrival Gap**     | Tiempo entre llegadas consecutivas de paquetes de audio entrantes.                                                                                                                       |                                                                                   |
| **Max Arrival Gap**       | Mayor intervalo de llegada registrado desde que se abrió el cuadro de diálogo.                                                                                                           |                                                                                   |
| **Network Jitter**        | Estimación suavizada de la fluctuación del flujo de audio.                                                                                                                               |                                                                                   |
| Overview (pestaña)        | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). |                                                                                   |
| Details (pestaña)         | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                                     |                                                                                   |
| Latency (pestaña)         | Gráfico de series temporales de ancho completo de RTT, intervalo de llegada y fluctuación (jitter) en ms.                                                                                |                                                                                   |
| Rates (pestaña)           | Gráfico de series temporales de ancho completo con escala logarítmica de las velocidades binarias entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.            |                                                                                   |
| Packet Loss (pestaña)     | Gráfico de series temporales de ancho completo del % de pérdida de paquetes por categoría de flujo.                                                                                     |                                                                                   |
| Audio (pestaña)           | Gráfico de series temporales de ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s.                                                                            |                                                                                   |
| Logs (pestaña)            | Visualización en vivo del archivo de registro de AetherSDR, filtrada por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría.      | El selector Timeframe está oculto mientras esta pestaña está activa.              |
| Timeframe                 | Selecciona cuánto atrás en el tiempo muestran el historial los gráficos de series temporales. El valor predeterminado es 5 minutos. Valores válidos: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week. | Se muestra en la esquina superior derecha de la barra de pestañas; oculto cuando la pestaña Logs está activa. |
| Filter Categories (Logs)  | Casillas de verificación por categoría para filtrar la vista de registros. Incluye una categoría General (predeterminada) más todas las categorías registradas por LogManager.           |                                                                                   |
| Select All (Logs)         | Muestra todas las categorías de registro en el visor.                                                                                                                                    |                                                                                   |
| Deselect All (Logs)       | Oculta todas las categorías de registro del visor.                                                                                                                                       |                                                                                   |
| Live / Paused (Logs)      | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba detiene el desplazamiento automático; al hacer clic en Live se reanuda y salta al final. |                                                                                   |

Todos los indicadores se actualizan una vez por segundo.

## Uso de la pestaña Logs

La pestaña Logs proporciona una visualización en vivo del archivo de registro de AetherSDR directamente dentro del cuadro de diálogo Network Diagnostics.

1. Haga clic en la pestaña **Logs**. El selector **Timeframe** en la esquina superior derecha se oculta mientras esta pestaña está activa.
2. La ruta del archivo de registro se muestra en la parte superior de la pestaña. Esta es la ruta completa del archivo que se está visualizando.
3. Use las casillas de verificación **Filter Categories (Logs)** para incluir o excluir categorías de registro específicas. La categoría General está disponible de forma predeterminada; las categorías adicionales aparecen a medida que LogManager las registra.
4. Haga clic en **Select All (Logs)** para habilitar todas las categorías a la vez. Haga clic en **Deselect All (Logs)** para ocultar todas las categorías.
5. El visor está en modo **Live** de forma predeterminada y se desplaza automáticamente a la salida más reciente. Desplácese hacia arriba para pausar el desplazamiento automático; el botón cambia a **Paused**. Haga clic en **Live** para reanudar y saltar de nuevo al final.
6. Las entradas de registro tienen resaltado de sintaxis por nivel de registro (debug, info, warning, critical) y nombre de categoría.

## Consejos

- **Subejecuciones en aumento, búfer cerca de cero:** El flujo de audio no llega con la suficiente rapidez para mantener el búfer lleno. Verifique la velocidad **Audio** en el grupo **Incoming Stream Rates** y compárela con la velocidad binaria esperada. Una velocidad de Audio muy baja o cero significa que los paquetes no están llegando en absoluto.
- **Pérdida de paquetes cero pero aún se producen subejecuciones:** El grupo **Packet Loss (Sequence Gaps)** solo cuenta los números de secuencia VITA faltantes. Los paquetes que llegan tarde en lugar de faltar no incrementarán el contador de pérdidas, pero aun así causarán fluctuación y subejecuciones. Use **Audio Arrival Gap** y **Network Jitter** para detectar esta condición.
- **Max Arrival Gap grande con un intervalo promedio bajo:** Esto indica ráfagas ocasionales de paquetes retrasados en lugar de una pérdida sostenida. Aísle la ruta de red hacia la radio y verifique si hay tráfico en competencia.
- **RX Buffer Peak es muy bajo:** El búfer nunca acumuló una reserva útil. Esto hace que el flujo sea sensible a cualquier variación en la entrega. Verifique la ruta de red y considere si otro tráfico pesado compite en el mismo enlace.
- **Investigar desconexiones o errores inesperados:** Abra la pestaña **Logs** y active las categorías relevantes de LogManager. Use **Filter Categories (Logs)** para centrarse en la categoría de interés, luego reproduzca la falla mientras el visor está en modo **Live**.

## Solución de problemas

- **Todos los indicadores de audio muestran cero o ningún dato** — La radio no está transmitiendo audio. Confirme que la radio esté conectada y que un slice receptor esté activo.
- **Underruns (last sec) es distinto de cero pero Underruns (total) es pequeño** — El problema es intermitente. Deje el cuadro de diálogo abierto y espere un período de observación más largo. Observe **Max Arrival Gap** para detectar evidencia de ráfagas periódicas.
- **Network Jitter es alto pero las caídas de audio muestran cero** — Los paquetes llegan tarde en lugar de perderse. La fluctuación reduce directamente el margen efectivo del búfer. Verifique si hay otro tráfico UDP compitiendo en la misma interfaz.
- **La pestaña Logs no muestra salida** — Confirme que la ruta del archivo de registro que se muestra en la parte superior de la pestaña sea accesible. Si no hay categorías marcadas, haga clic en **Select All (Logs)** para restaurar la visibilidad.

## Relacionado

- [Network Diagnostics overview](../../features/network-diagnostics/overview.md)
- [Measure RTT and packet drops during audio problems](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](../../features/network-diagnostics/check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
