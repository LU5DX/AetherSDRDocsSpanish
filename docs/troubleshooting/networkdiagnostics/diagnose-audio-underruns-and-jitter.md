# Diagnosticar subejecuciones de audio y fluctuación

Utilice el cuadro de diálogo Diagnóstico de Red para leer el estado actual del búfer de audio, los contadores de subejecución, la temporización de llegada de paquetes y las estimaciones de fluctuación. Esto le ayuda a identificar si las interrupciones de audio son causadas por un búfer insuficiente, una entrega irregular de paquetes o fluctuación de red.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión de radio activa, pero los indicadores de audio solo son significativos mientras una radio está conectada y transmitiendo audio.
- Reproduzca el problema de audio antes de abrir el diálogo para que los contadores y valores pico reflejen la condición de falla.
- La geometría de la ventana del diálogo se guarda y restaura automáticamente entre sesiones.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el cuadro de diálogo Diagnóstico de Red.
2. Use la barra de pestañas en la parte superior para seleccionar la vista que necesita:
   - **Overview** – Tarjetas de estado y gráficos de series temporales resumidos.
   - **Details** – Cuadrícula desplazable con todas las métricas etiquetadas.
   - **Latency** – Gráfico de RTT, intervalo de llegada y fluctuación.
   - **Rates** – Gráfico de tasa de bits entrante por flujo.
   - **Packet Loss** – Gráfico de porcentaje de pérdida de paquetes por categoría.
   - **Audio** – Gráfico de llenado del búfer de reproducción y tasa de subejecuciones.
   - **Logs** – Visualización en vivo del archivo de registro de AetherSDR.
3. En la pestaña **Details**, localice el grupo **Audio Playback**.
4. Lea **RX Buffer Now** para ver cuántos bytes (y milisegundos) de audio están actualmente almacenados en el búfer de reproducción.
5. Lea **RX Buffer Peak** para ver el llenado máximo del búfer registrado desde que se abrió el diálogo.
6. Lea **Underruns (total)** para ver el conteo acumulado de subejecuciones de búfer desde que se inició el motor de audio.
7. Lea **Underruns (last sec)** para ver cuántas subejecuciones ocurrieron en la ventana de un segundo más reciente. Un valor distinto de cero aquí mientras el audio se está transmitiendo activamente indica un problema en curso.
8. Lea **Audio Arrival Gap** para ver el intervalo de llegada entre paquetes actual. Un valor significativamente mayor que el período de paquete esperado indica una entrega irregular.
9. Lea **Max Arrival Gap** para ver el peor caso de intervalo de llegada registrado desde que se abrió el diálogo.
10. Lea **Network Jitter** para ver la estimación de fluctuación suavizada para el flujo de audio.
11. Si las subejecuciones están aumentando pero **RX Buffer Now** permanece cerca de cero, el búfer se está quedando sin datos — consulte los consejos a continuación.
12. Haga clic en **Close** cuando termine.

## Qué hace cada control

### Pestañas

| Pestaña          | Comportamiento                                                                                                                                       |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Overview**     | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). |
| **Details**      | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                        |
| **Latency**      | Gráfico de series temporales a ancho completo de RTT, intervalo de llegada y fluctuación en ms.                                                        |
| **Rates**        | Gráfico de series temporales a ancho completo en escala logarítmica de tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps. |
| **Packet Loss**  | Gráfico de series temporales a ancho completo del % de pérdida de paquetes por categoría de flujo.                                                    |
| **Audio**        | Gráfico de series temporales a ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s.                                          |
| **Logs**         | Visualización en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector de marco temporal se oculta mientras esta pestaña está activa. |

### Controles

| Control                         | Tipo           | Valor predeterminado | Comportamiento                                                                                                                                                |
|---------------------------------|----------------|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Timeframe**                   | Cuadro combinado | 5 minutos          | Selecciona cuánto tiempo atrás muestran los gráficos de series temporales. Opciones: 1 minuto, 5 minutos, 15 minutos, 1 hora, 1 día, 1 semana. Se muestra en la esquina superior derecha de la barra de pestañas; se oculta cuando la pestaña Logs está activa. |
| **Filter Categories (Logs)**    | Casillas de verificación | –         | Casillas de verificación por categoría para filtrar la vista de registro. Incluye una categoría General (predeterminada) más todas las categorías registradas por LogManager.            |
| **Select All (Logs)**           | Botón          | –                   | Muestra todas las categorías de registro en el visor.                                                                                                           |
| **Deselect All (Logs)**         | Botón          | –                   | Oculta todas las categorías de registro del visor.                                                                                                             |
| **Live / Paused (Logs)**        | Botón de alternancia | Live         | En modo Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final.             |
| **Close**                       | Botón          | –                   | Cierra el cuadro de diálogo.                                                                                                                                  |

### Indicadores

Todos los indicadores se actualizan una vez por segundo.

| Indicador                 | Significado                                                                                                 |
|---------------------------|-------------------------------------------------------------------------------------------------------------|
| **Status**                | Calidad general del enlace, codificada con colores verde → rojo. Estados: Excellent, Very Good, Good, Fair, Poor. |
| **Target Radio IP**       | IP de la radio conectada, o "Not connected".                                                                |
| **Selected Source**       | NIC local/ruta de enlace utilizada para la conexión.                                                        |
| **Local TCP**             | Extremo TCP local.                                                                                          |
| **Local UDP**             | Extremo UDP local.                                                                                          |
| **First UDP Packet**      | Si el primer paquete UDP se ha recibido desde la conexión. Estados: Yes, No.                                |
| **Latency (RTT)**         | Tiempo de ida y vuelta actual.                                                                              |
| **Max Latency (RTT)**     | RTT más alto visto desde la conexión.                                                                       |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Tasa de ingreso por categoría en kbps.                                                   |
| **Total RX / Total TX**   | Bytes agregados por segundo en cada dirección.                                                              |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Conteos y porcentaje de paquetes perdidos por categoría.                                   |
| **RX Buffer Now / Peak**  | Llenado actual y máximo del búfer de audio en bytes y ms.                                                   |
| **Underruns (total / last sec)** | Contadores de subejecuciones de audio.                                                              |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización de llegada entre paquetes.                                                        |
| **Network Jitter**        | Estimación de fluctuación suavizada del flujo de audio en ms.                                               |
| **Log path label**        | Muestra la ruta completa del archivo de registro que se está siguiendo.                                      |

## Uso de la pestaña Logs

La pestaña Logs proporciona una vista en vivo del archivo de registro de AetherSDR directamente dentro del cuadro de diálogo Diagnóstico de Red.

1. Haga clic en la pestaña **Logs**. El selector **Timeframe** en la esquina superior derecha se oculta mientras esta pestaña está activa.
2. La ruta del registro se muestra en la parte superior de la pestaña. Esta es la ruta completa del archivo que se está siguiendo.
3. Use las casillas de verificación **Filter Categories (Logs)** para incluir o excluir categorías de registro específicas. La categoría General está disponible de forma predeterminada; aparecen categorías adicionales a medida que LogManager las registra.
4. Haga clic en **Select All (Logs)** para activar todas las categorías a la vez. Haga clic en **Deselect All (Logs)** para ocultar todas las categorías.
5. El visor está en modo **Live** de forma predeterminada y se desplaza automáticamente a la salida más reciente. Desplácese hacia arriba para pausar el desplazamiento automático; el botón cambia a **Paused**. Haga clic en **Live** para reanudar y saltar al final.
6. Las entradas de registro tienen resaltado de sintaxis por nivel de registro (debug, info, warning, critical) y nombre de categoría.

## Consejos

- **Subejecuciones en aumento, búfer cerca de cero:** El flujo de audio no llega lo suficientemente rápido para mantener el búfer lleno. Verifique la tasa **Audio** en el grupo **Incoming Stream Rates** y compárela con la tasa de bits esperada. Una tasa de Audio muy baja o cero significa que los paquetes no están llegando en absoluto.
- **Pérdida de paquetes cero pero aún así hay subejecuciones:** El grupo **Packet Loss (Sequence Gaps)** solo cuenta los números de secuencia VITA faltantes. Los paquetes que llegan tarde en lugar de faltar no incrementarán el contador de pérdidas, pero aún así causarán fluctuación y subejecuciones. Use **Audio Arrival Gap** y **Network Jitter** para detectar esta condición.
- **Max Arrival Gap grande con promedio bajo:** Esto indica ráfagas ocasionales de paquetes retrasados en lugar de pérdida sostenida. Aísle la ruta de red hacia la radio y verifique si hay tráfico competidor.
- **RX Buffer Peak es muy bajo:** El búfer nunca acumuló una reserva útil. Esto hace que el flujo sea sensible a cualquier variación en la entrega. Verifique la ruta de red y considere si otro tráfico pesado compite en el mismo enlace.
- **Investigar desconexiones o errores inesperados:** Abra la pestaña **Logs** y active las categorías relevantes de LogManager. Use **Filter Categories (Logs)** para centrarse en la categoría de interés, luego reproduzca la falla mientras el visor está en modo **Live**.

## Solución de problemas

- **Todos los indicadores de audio muestran cero o sin datos** — La radio no está transmitiendo audio. Confirme que la radio esté conectada y que un receptor (slice) esté activo.
- **Underruns (last sec) es distinto de cero pero Underruns (total) es pequeño** — El problema es intermitente. Deje el diálogo abierto y espere un período de observación más largo. Vigile **Max Arrival Gap** para detectar evidencia de ráfagas periódicas.
- **Network Jitter es alto pero Audio drops muestra cero** — Los paquetes llegan tarde en lugar de perderse. La fluctuación reduce directamente el margen efectivo del búfer. Verifique si hay otro tráfico UDP compitiendo en la misma interfaz.
- **La pestaña Logs no muestra salida** — Confirme que la ruta del archivo de registro que se muestra en la parte superior de la pestaña sea accesible. Si no hay categorías marcadas, haga clic en **Select All (Logs)** para restaurar la visibilidad.

## Relacionados

- [Network Diagnostics overview](../../features/network-diagnostics/overview.md)
- [Measure RTT and packet drops during audio problems](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](../../features/network-diagnostics/check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
