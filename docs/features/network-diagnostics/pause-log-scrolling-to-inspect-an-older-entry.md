# Diagnóstico de Red

El cuadro de diálogo de Diagnóstico de Red proporciona una vista en vivo del enlace de red con la radio. Cuenta con un diseño de paneles múltiples que incluye un árbol de navegación a la izquierda y un área de contenido a la derecha, reemplazando el diseño anterior basado en pestañas. Las páginas incluyen un panel de resumen, métricas detalladas, gráficos de rendimiento por flujo y un visor de registros en vivo.

## Abrir Diagnóstico de Red

1. Vaya a `Settings > Network...`.
2. Se abre el cuadro de diálogo de Diagnóstico de Red.

## Navegación

El panel izquierdo contiene un widget de navegación en árbol que enumera todas las páginas de diagnóstico disponibles. Haga clic en cualquier nombre de página para mostrar su contenido en el panel derecho.

Un campo de búsqueda en la parte superior del árbol de navegación le permite filtrar la lista escribiendo parte del nombre de una página.

## Páginas

El cuadro de diálogo contiene las siguientes páginas, seleccionables desde el árbol de navegación:

- **Overview** – Muestra cuatro tarjetas de estado (Estado, Latencia, Pérdida de Paquetes, Buffer de Audio) y cuatro gráficos de series temporales (Latencia y Jitter, Pérdida de Paquetes Reciente, Tasas Totales de Flujo, Buffer de Audio).
- **Details** – Una cuadrícula desplazable con valores etiquetados para los grupos de Estado de Red, Tasas de Flujo Entrante, Pérdida de Paquetes y Reproducción de Audio.
- **Latency** – Gráfico de series temporales a ancho completo de RTT, intervalo de llegada y jitter en ms.
- **Rates** – Gráfico de series temporales a ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.
- **Packet Loss** – Gráfico de series temporales a ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.
- **Audio** – Gráfico de series temporales a ancho completo del llenado del buffer de reproducción (ms) y sub-ejecuciones por segundo. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y estado del flujo para cada flujo de audio activo.
- **Logs** – Visualización en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Con resaltado de sintaxis por nivel de registro y nombre de categoría. El selector de período de tiempo está oculto mientras esta página está activa.

## Selector de período de tiempo

Un menú desplegable en la esquina superior derecha del área de contenido selecciona cuánto tiempo hacia atrás muestran el historial los gráficos de series temporales. Las siguientes opciones están disponibles:

- 1 minute
- 5 minutes (predeterminado)
- 15 minutes
- 1 hour
- 1 day
- 1 week

El selector de período de tiempo está oculto cuando la página **Logs** está activa.

## Pausar el desplazamiento de registros para inspeccionar una entrada anterior

La página Logs sigue el archivo de registro de AetherSDR en tiempo real. Esta sección explica cómo pausar ese desplazamiento automático para que pueda leer una entrada anterior sin que la vista salte, y cómo reanudar el seguimiento en vivo cuando haya terminado.

### Pasos

1. Abra Diagnóstico de Red mediante `Settings > Network...`.
2. Haga clic en **Logs** en el árbol de navegación.
3. Para pausar el desplazamiento, realice una de las siguientes acciones:
   - Desplácese hacia arriba en el visor de registros. El visor cambia automáticamente a **Paused**.
   - Haga clic en el botón de alternancia, que muestra **Live**, para cambiarlo a **Paused**.
4. Lea la entrada que necesita. La pantalla permanece fija mientras el botón muestra **Paused**.
5. Cuando esté listo para volver al seguimiento en vivo, haga clic en el botón de alternancia, que ahora muestra **Paused**, para cambiarlo de nuevo a **Live**. El visor salta inmediatamente a la salida más reciente y reanuda el desplazamiento automático.

### Controles de la página Logs

| Control                            | Predeterminado | Comportamiento                                                                                                                                                                                                                                                                                                                      |
|------------------------------------|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Live / Paused** (botón de alternancia) | Live           | Cuando está en **Live**, el visor se desplaza automáticamente a la salida de registro más reciente. Cuando está en **Paused**, el desplazamiento se detiene y la pantalla mantiene su posición actual. Desplazarse hacia arriba en el visor cambia automáticamente el botón a **Paused**. Al hacer clic en el botón mientras muestra **Paused** se reanuda el desplazamiento automático y salta al final. |
| **Filter Categories** (casillas de verificación) | –              | Las casillas de verificación por categoría filtran la vista de registro. Incluye una categoría "General" (predeterminada) más todas las categorías registradas de LogManager.                                                                                                                                                        |
| **Select All** (botón pulsador)    | –              | Muestra todas las categorías de registro en el visor.                                                                                                                                                                                                                                                                                |
| **Deselect All** (botón pulsador)  | –              | Oculta todas las categorías de registro del visor.                                                                                                                                                                                                                                                                                   |

### Consejos

- Desplazarse hacia arriba es la forma más rápida de pausar: no necesita buscar primero el botón de alternancia.
- La vista de registro tiene resaltado de sintaxis por nivel de registro y nombre de categoría, lo que facilita encontrar la entrada que busca.
- Las casillas de verificación de filtro de categoría y los botones **Select All** y **Deselect All** permanecen activos mientras está en pausa, para que pueda reducir las entradas visibles sin reanudar el desplazamiento en vivo.

## Indicadores

El cuadro de diálogo muestra los siguientes indicadores:

| Indicador | Significado |
|---|---|
| Status | Calidad general del enlace, codificada con colores verde → rojo. Estados: Excelente, Muy Buena, Buena, Regular, Mala |
| Target Radio IP | IP de la radio conectada, o "No conectado" |
| Selected Source | NIC/ruta de enlace local utilizada para la conexión |
| Local TCP | Extremo TCP local |
| Local UDP | Extremo UDP local |
| First UDP Packet | Si se ha recibido el primer paquete UDP desde la conexión (Sí/No) |
| Latency (RTT) | Tiempo de ida y vuelta actual |
| Max Latency (RTT) | RTT más alto observado desde la conexión |
| Audio / FFT / Waterfall / Meters / DAX rates | Tasa de ingreso por categoría en kbps |
| Total RX / Total TX | Bytes agregados por segundo en cada dirección |
| Audio / FFT / Waterfall / Meters / DAX drops | Conteo y porcentaje de paquetes perdidos por categoría |
| RX Buffer Now / Peak | Llenado actual y máximo del buffer de audio en bytes y ms |
| Underruns (total / last sec) | Contadores de sub-ejecución de audio |
| Audio Arrival Gap / Max Arrival Gap | Temporización entre llegadas de paquetes |
| Network Jitter | Estimación de jitter suavizada del flujo de audio en ms |
| Log path label | Ruta completa del archivo de registro que se está siguiendo |

## Cerrar el cuadro de diálogo

Haga clic en **Close** para cerrar el cuadro de diálogo de Diagnóstico de Red.
