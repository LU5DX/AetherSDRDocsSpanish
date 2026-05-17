# Diagnóstico de Red

El diálogo de Diagnóstico de Red ofrece una vista en vivo del enlace de red con la radio. Presenta un diseño de múltiples pestañas con un panel de resumen, métricas detalladas, gráficos de rendimiento por flujo y un visor de registros en vivo.

## Abrir el Diagnóstico de Red

1. Vaya a `Settings > Network...`.
2. Se abre el diálogo de Diagnóstico de Red.

## Pestañas

El diálogo contiene las siguientes pestañas:

- **Overview** – Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).
- **Details** – Una cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.
- **Latency** – Gráfico de series temporales a ancho completo del RTT, intervalo de llegada y fluctuación en ms.
- **Rates** – Gráfico de series temporales a ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.
- **Packet Loss** – Gráfico de series temporales a ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.
- **Audio** – Gráfico de series temporales a ancho completo del llenado del búfer de reproducción (ms) y las subejecuciones por segundo.
- **Logs** – Visualización en vivo del archivo de registro de AetherSDR, filtrada mediante casillas de verificación por categoría. Resaltado de sintaxis según el nivel de registro y el nombre de la categoría. El selector de marco temporal se oculta mientras esta pestaña está activa.

## Selector de marco temporal

Un menú desplegable en la esquina superior derecha de la barra de pestañas selecciona cuánto tiempo atrás muestran la historia los gráficos de series temporales. Las siguientes opciones están disponibles:

- 1 minute
- 5 minutes (predeterminado)
- 15 minutes
- 1 hour
- 1 day
- 1 week

El selector de marco temporal se oculta cuando la pestaña **Logs** está activa.

## Pausar el desplazamiento del registro para inspeccionar una entrada anterior

La pestaña Logs muestra el archivo de registro de AetherSDR en tiempo real. Esta sección explica cómo pausar ese desplazamiento automático para que pueda leer una entrada anterior sin que la vista se mueva, y cómo reanudar la visualización en vivo cuando haya terminado.

### Pasos

1. Abra Diagnóstico de Red mediante `Settings > Network...`.
2. Haga clic en la pestaña **Logs**.
3. Para pausar el desplazamiento, realice una de las siguientes acciones:
   - Desplácese hacia arriba en el visor de registros. El visor cambia automáticamente al estado **Paused**.
   - Haga clic en el botón de alternancia, que muestra **Live**, para cambiarlo a **Paused**.
4. Lea la entrada que necesita. La pantalla permanece fija mientras el botón muestra **Paused**.
5. Cuando esté listo para volver a la visualización en vivo, haga clic en el botón de alternancia, que ahora muestra **Paused**, para cambiarlo de nuevo a **Live**. El visor salta inmediatamente a la salida más reciente y reanuda el desplazamiento automático.

### Controles de la pestaña Logs

| Control | Predeterminado | Comportamiento |
|---|---|---|
| **Live / Paused** (botón de alternancia) | Live | Cuando está en **Live**, el visor se desplaza automáticamente a la salida de registro más reciente. Cuando está en **Paused**, el desplazamiento se detiene y la pantalla mantiene su posición actual. Desplazarse hacia arriba en el visor cambia automáticamente el botón a **Paused**. Al hacer clic en el botón mientras muestra **Paused** se reanuda el desplazamiento automático y se salta al final. |
| **Filter Categories** (casillas de verificación) | – | Las casillas de verificación por categoría filtran la vista del registro. Incluye una categoría "General" (predeterminada) más todas las categorías registradas de LogManager. |
| **Select All** (botón pulsador) | – | Muestra todas las categorías de registro en el visor. |
| **Deselect All** (botón pulsador) | – | Oculta todas las categorías de registro del visor. |

### Consejos

- Desplazarse hacia arriba es la forma más rápida de pausar: no necesita buscar el botón de alternancia primero.
- La vista de registro tiene resaltado de sintaxis por nivel de registro y nombre de categoría, lo que facilita localizar la entrada que busca.
- Las casillas de verificación de filtro por categoría y los botones **Select All** y **Deselect All** permanecen activos mientras está en pausa, para que pueda reducir las entradas visibles sin reanudar el desplazamiento en vivo.

## Indicadores

El diálogo muestra los siguientes indicadores:

| Indicador | Significado |
|---|---|
| Status | Calidad general del enlace, codificada por color verde → rojo. Estados: Excellent, Very Good, Good, Fair, Poor |
| Target Radio IP | IP de la radio conectada, o "Not connected" |
| Selected Source | NIC local/ruta de enlace utilizada para la conexión |
| Local TCP | Extremo TCP local |
| Local UDP | Extremo UDP local |
| First UDP Packet | Indica si se ha recibido el primer paquete UDP desde la conexión (Yes/No) |
| Latency (RTT) | Tiempo de ida y vuelta actual |
| Max Latency (RTT) | RTT más alto observado desde la conexión |
| Audio / FFT / Waterfall / Meters / DAX rates | Tasa de ingreso por categoría en kbps |
| Total RX / Total TX | Bytes agregados por segundo en cada dirección |
| Audio / FFT / Waterfall / Meters / DAX drops | Conteo y porcentaje de paquetes descartados por categoría |
| RX Buffer Now / Peak | Llenado actual y máximo del búfer de audio en bytes y ms |
| Underruns (total / last sec) | Contadores de subejecuciones de audio |
| Audio Arrival Gap / Max Arrival Gap | Temporización de llegada entre paquetes |
| Network Jitter | Estimación suavizada de fluctuación de la transmisión de audio en ms |
| Log path label | Ruta completa del archivo de registro que se está visualizando |

## Cerrar el diálogo

Haga clic en **Close** para cerrar el diálogo de Diagnóstico de Red.
