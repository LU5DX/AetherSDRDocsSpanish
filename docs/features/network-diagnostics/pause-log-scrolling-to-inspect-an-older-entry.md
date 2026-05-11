# Diagnóstico de Red

El cuadro de diálogo Diagnóstico de Red proporciona una vista en vivo del enlace de red con la radio. Presenta un diseño de múltiples pestañas con un panel de resumen, métricas detalladas, gráficos de rendimiento por flujo y un visor de registros en vivo.

## Abrir Diagnóstico de Red

1. Vaya a `Settings > Network...`.
2. Se abre el cuadro de diálogo Diagnóstico de Red.

## Pestañas

El cuadro de diálogo contiene las siguientes pestañas:

- **Overview** – Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).
- **Details** – Una cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.
- **Latency** – Gráfico de series temporales a ancho completo del RTT, intervalo de llegada y jitter en ms.
- **Rates** – Gráfico de series temporales a ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.
- **Packet Loss** – Gráfico de series temporales a ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.
- **Audio** – Gráfico de series temporales a ancho completo del llenado del búfer de reproducción (ms) y las subejecuciones por segundo.
- **Logs** – Cola en vivo del archivo de registro de AetherSDR, filtrada por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría.

## Selector de intervalo de tiempo

Un menú desplegable en la esquina superior derecha de la barra de pestañas selecciona qué tan atrás muestran los gráficos de series temporales el historial. Están disponibles las siguientes opciones:

- 1 minute
- 5 minutes (predeterminado)
- 15 minutes
- 1 hour
- 1 day
- 1 week

El selector de intervalo de tiempo se oculta cuando la pestaña **Logs** está activa.

## Pausar el desplazamiento de registros para inspeccionar una entrada anterior

La pestaña Logs sigue la cola del archivo de registro de AetherSDR en tiempo real. Esta sección explica cómo pausar ese desplazamiento automático para que pueda leer una entrada anterior sin que salte, y cómo reanudar la cola en vivo cuando haya terminado.

### Pasos

1. Abra Diagnóstico de Red mediante `Settings > Network...`.
2. Haga clic en la pestaña **Logs**.
3. Para pausar el desplazamiento, haga una de las siguientes acciones:
   - Desplácese hacia arriba en el visor de registros. El visor cambia automáticamente a **Paused**.
   - Haga clic en el botón de alternancia, que muestra **Live**, para cambiarlo a **Paused**.
4. Lea la entrada que necesita. La pantalla permanece fija mientras el botón muestra **Paused**.
5. Cuando esté listo para volver a la cola en vivo, haga clic en el botón de alternancia, que ahora muestra **Paused**, para cambiarlo de nuevo a **Live**. El visor salta inmediatamente a la salida más reciente y reanuda el desplazamiento automático.

### Controles de la pestaña Logs

| Control | Predeterminado | Comportamiento |
|---|---|---|
| **Live / Paused** (botón de alternancia) | Live | Cuando está en **Live**, el visor se desplaza automáticamente a la salida de registro más reciente. Cuando está en **Paused**, el desplazamiento se detiene y la pantalla mantiene su posición actual. Desplazarse hacia arriba en el visor cambia automáticamente el botón a **Paused**. Al hacer clic en el botón mientras muestra **Paused** se reanuda el desplazamiento automático y se salta a la cola. |
| **Filter Categories** (casillas de verificación) | – | Las casillas de verificación por categoría filtran la vista de registro. Incluye una categoría "General" (predeterminada) más todas las categorías registradas de LogManager. |
| **Select All** (botón pulsador) | – | Muestra todas las categorías de registro en el visor. |
| **Deselect All** (botón pulsador) | – | Oculta todas las categorías de registro del visor. |

### Consejos

- Desplazarse hacia arriba es la forma más rápida de pausar: no necesita buscar primero el botón de alternancia.
- La vista de registro tiene resaltado de sintaxis por nivel de registro y nombre de categoría, lo que facilita encontrar la entrada que busca.
- Las casillas de verificación de filtro de categoría y los botones **Select All** y **Deselect All** permanecen activos mientras está en pausa, para que pueda reducir las entradas visibles sin reanudar el desplazamiento en vivo.

## Indicadores

El cuadro de diálogo muestra los siguientes indicadores:

| Indicador | Significado |
|---|---|
| Status | Calidad general del enlace, codificada por colores verde → rojo. Estados: Excellent, Very Good, Good, Fair, Poor |
| Target Radio IP | IP de la radio conectada, o "Not connected" |
| Selected Source | NIC local/ruta de enlace utilizada para la conexión |
| Local TCP | Extremo TCP local |
| Local UDP | Extremo UDP local |
| First UDP Packet | Si el primer paquete UDP se ha recibido desde la conexión (Yes/No) |
| Latency (RTT) | Tiempo de ida y vuelta actual |
| Max Latency (RTT) | RTT más alto visto desde la conexión |
| Audio / FFT / Waterfall / Meters / DAX rates | Tasa de ingreso por categoría en kbps |
| Total RX / Total TX | Bytes agregados por segundo en cada dirección |
| Audio / FFT / Waterfall / Meters / DAX drops | Conteos y porcentaje de paquetes descartados por categoría |
| RX Buffer Now / Peak | Llenado actual y máximo del búfer de audio en bytes y ms |
| Underruns (total / last sec) | Contadores de subejecución de audio |
| Audio Arrival Gap / Max Arrival Gap | Temporización de llegada entre paquetes |
| Network Jitter | Estimación de jitter suavizada del flujo de audio en ms |
| Log path label | Ruta completa del archivo de registro que se está siguiendo |

## Modo sin marco

El cuadro de diálogo Diagnóstico de Red puede aparecer con o sin barra de título, según la configuración global `FramelessWindow` (`Settings > Appearance > Frameless Window`). Cuando el modo sin marco está habilitado, el cuadro de diálogo incluye una barra de título personalizada y controladores de redimensionamiento. Cuando está deshabilitado, la ventana utiliza la barra de título y decoraciones estándar del sistema operativo.

## Cerrar el cuadro de diálogo

Haga clic en **Close** para cerrar el cuadro de diálogo Diagnóstico de Red.
