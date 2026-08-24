# Diagnóstico de Red

El diálogo de Diagnóstico de Red proporciona una vista en vivo del enlace de red con la radio. Cuenta con un diseño de múltiples paneles con un árbol de navegación a la izquierda y un área de contenido a la derecha. Las páginas incluyen un panel de resumen, métricas detalladas, gráficos de rendimiento por flujo, un visor de registros de aplicación y una página de clientes TCI.

## Abrir el Diagnóstico de Red

1. Vaya a `Settings > Network...`.
2. Se abre el diálogo de Diagnóstico de Red.

## Navegación

El panel izquierdo contiene un widget de navegación en árbol que enumera todas las páginas de diagnóstico disponibles. Haga clic en cualquier nombre de página para mostrar su contenido en el panel derecho.

Un campo de búsqueda en la parte superior del árbol de navegación le permite filtrar la lista escribiendo parte del nombre de una página.

## Páginas

El diálogo contiene las siguientes páginas, seleccionables desde el árbol de navegación:

- **Overview** – Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).
- **Connection Details** – Una cuadrícula desplazable con valores etiquetados para Network Status, Incoming Stream Rates, Packet Loss, Audio Playback y la subsección Adaptive Frame-Rate Throttle. Incluye una acción Read-Only Clipboard Copy para copiar todo el resumen de diagnóstico. Renombrada de "Details" en la reorganización del árbol de navegación v26.8.4.
- **Latency** – Gráfico de series temporales de ancho completo de RTT, intervalo de llegada y jitter en ms.
- **Rates** – Gráfico de series temporales de ancho completo con escala logarítmica de las velocidades de bits entrantes por flujo (total RX, Audio, FFT, Waterfall, Meters, DAX) en kbps.
- **Packet Loss** – Gráfico de series temporales de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.
- **Audio** – Gráfico de series temporales de ancho completo del llenado del búfer de reproducción (ms) y subejecuciones por segundo. Incluye diagnósticos de audio RX por flujo que muestran velocidad de alimentación, déficit, paquetes tardíos, código de clase de paquete y estado del flujo para cada flujo de audio activo.
- **Logs** – Seguimiento en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector de período de tiempo está oculto mientras esta página está activa.
- **TCI Clients** – Enumera los clientes TCI conectados con un monitor de tráfico en vivo (Pause/Save log/Clear), controles de supresión de comandos de respuesta y detalles por cliente. Nuevo en v26.8.4. Compilación controlada por soporte HAVE_TCI / TCI. El selector de período de tiempo está oculto en esta página.

## Selector de período de tiempo

Un menú desplegable en la esquina superior derecha del área de contenido selecciona cuánto historial muestran los gráficos de series temporales. Las siguientes opciones están disponibles:

- 1 minuto
- 5 minutos (predeterminado)
- 15 minutos
- 1 hora
- 1 día
- 1 semana

El selector de período de tiempo está oculto cuando la página **Logs** o **TCI Clients** está activa.

## Pausar el desplazamiento del registro para inspeccionar una entrada anterior

La página Logs sigue el archivo de registro de AetherSDR en tiempo real. Esta sección explica cómo pausar ese desplazamiento automático para que pueda leer una entrada anterior sin que salte, y cómo reanudar el seguimiento en vivo cuando haya terminado.

### Pasos

1. Abra el Diagnóstico de Red mediante `Settings > Network...`.
2. Haga clic en **Logs** en el árbol de navegación.
3. Para pausar el desplazamiento, haga cualquiera de las siguientes acciones:
   - Desplácese hacia arriba en el visor de registros. El visor cambia automáticamente a **Paused**.
   - Haga clic en el botón de alternancia, que muestra **Live**, para cambiarlo a **Paused**.
4. Lea la entrada que necesite. La pantalla permanece fija mientras el botón muestra **Paused**.
5. Cuando esté listo para volver al seguimiento en vivo, haga clic en el botón de alternancia, que ahora muestra **Paused**, para cambiarlo de nuevo a **Live**. El visor salta inmediatamente a la salida más reciente y reanuda el desplazamiento automático.

### Controles de la página Logs

| Control                                | Predeterminado                                                                                                                                                      | Comportamiento                                                                                                                                                                                                                                                                                                                            |
|----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Live / Paused** (botón de alternancia)      | Live                                                                                                                                                         | Cuando está en **Live**, el visor se desplaza automáticamente a la salida de registro más reciente. Cuando está en **Paused**, el desplazamiento se detiene y la pantalla mantiene su posición actual. Desplazarse hacia arriba en el visor cambia automáticamente el botón a **Paused**. Al hacer clic en el botón mientras muestra **Paused** se reanuda el desplazamiento automático y salta al final. |
| **Filter Categories** (casillas de verificación)     | –                                                                                                                                                            | Las casillas de verificación por categoría filtran la vista de registro. Incluye una categoría "General" (predeterminada) más todas las categorías registradas de LogManager.                                                                                                                                                                                                     |
| **Select All** (botón pulsador)           | –                                                                                                                                                            | Muestra todas las categorías de registro en el visor.                                                                                                                                                                                                                                                                                             |
| **Deselect All** (botón pulsador)         | –                                                                                                                                                            | Oculta todas las categorías de registro del visor.                                                                                                                                                                                                                                                                                           |

### Consejos

- Desplazarse hacia arriba es la forma más rápida de pausar: no necesita buscar el botón de alternancia primero.
- La vista de registro tiene resaltado de sintaxis por nivel de registro y nombre de categoría, lo que facilita localizar la entrada que busca.
- Las casillas de verificación de filtro de categoría y los botones **Select All** y **Deselect All** permanecen activos mientras está en pausa, de modo que puede reducir las entradas visibles sin reanudar el desplazamiento en vivo.

## Indicadores

El diálogo muestra los siguientes indicadores:

| Indicador | Significado |
|---|---|
| Status | Calidad general del enlace, con código de colores verde → rojo. Estados: Excellent, Very Good, Good, Fair, Poor |
| Target Radio IP | IP de la radio conectada, o "Not connected" |
| Selected Source | NIC local/ruta de enlace utilizada para la conexión |
| Local TCP | Punto final TCP local |
| Local UDP | Punto final UDP local |
| First UDP Packet | Si se ha recibido el primer paquete UDP desde la conexión (Yes/No) |
| Latency (RTT) | Tiempo de ida y vuelta actual. Muestra "not measured on this link" cuando el transporte no tiene ida y vuelta que medir. |
| Max Latency (RTT) | RTT más alto observado desde la conexión. Muestra "not measured on this link" cuando el transporte no tiene ida y vuelta que medir. |
| Audio / FFT / Waterfall / Meters / DAX rates | Velocidad de ingreso por categoría en kbps. Muestra "n/a" cuando el transporte no proporciona estadísticas de categoría por flujo. |
| Total RX / Total TX | Bytes agregados por segundo en cada dirección |
| Audio / FFT / Waterfall / Meters / DAX drops | Conteos y porcentaje de paquetes descartados por categoría. Muestra "n/a" cuando el transporte no proporciona estadísticas de categoría por flujo. |
| RX Buffer Now / Peak | Llenado actual y máximo del búfer de audio en bytes y ms |
| Underruns (total / last sec) | Contadores de subejecución de audio |
| Audio Arrival Gap / Max Arrival Gap | Temporización de llegada entre paquetes. Muestra "not measured on this link" antes de que se cierre la primera ventana de temporización de entrega. |
| Network Jitter | Estimación de jitter suavizada del flujo de audio en ms. Muestra "not measured on this link" antes de que se cierre la primera ventana de temporización de entrega. |
| Adaptive Frame-Rate Throttle | Valores de Current State, Pending Lift y Sessions This Run. Reduce las velocidades de fotogramas del panadapter cuando se detecta latencia o pérdida. Oculto hasta que los datos de limitación estén disponibles. |
| Log path label | Ruta completa del archivo de registro que se está siguiendo |

## Cerrar el diálogo

Haga clic en **Close** para cerrar el diálogo de Diagnóstico de Red.
