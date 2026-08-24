# Cuadro de diálogo Network Diagnostics

El cuadro de diálogo Network Diagnostics proporciona una vista en vivo completa del enlace de red hacia la radio. Presenta un diseño de múltiples pestañas con un panel Overview que incluye tarjetas de estado y gráficos de series temporales, un panel Connection Details con métricas etiquetadas (incluida la sección Adaptive Frame-Rate Throttle), gráficos de tendencia de Latency & Jitter / Stream Rates / Packet Loss / Audio con búsqueda, una página Application Logs para seguir el archivo de registro filtrado por categoría, diagnósticos de audio RX por flujo y una página TCI Clients (sujeta a compilación).

## Abrir el cuadro de diálogo

1. Haga clic en **Settings** > **Network...**

El cuadro de diálogo se abre haya o no una radio conectada, pero las métricas solo son significativas cuando hay conexión.

## Pestañas

| Pestaña | Descripción |
|-----|-------------|
| **Overview** | Cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). |
| **Connection Details** | Cuadrícula desplazable con valores etiquetados para Network Status, Incoming Stream Rates, Packet Loss, Audio Playback y la subsección Adaptive Frame-Rate Throttle. Antes se llamaba "Details" en la reorganización del árbol de navegación de la v26.8.4. |
| **Latency** | Gráfico de series temporales de ancho completo del RTT, intervalo de llegada y jitter en ms. |
| **Rates** | Gráfico de series temporales de ancho completo con escala logarítmica de las velocidades de bits entrantes por flujo (total RX, Audio, FFT, Waterfall, Meters, DAX) en kbps. |
| **Packet Loss** | Gráfico de series temporales de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo. |
| **Audio** | Gráfico de series temporales de ancho completo del llenado del búfer de reproducción (ms) y subdesbordamientos/s. Incluye diagnósticos de audio RX por flujo que muestran la velocidad de alimentación, el déficit, los paquetes tardíos, el código de clase de paquete y el estado del flujo para cada flujo de audio activo. |
| **Logs** | Seguimiento en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. |
| **TCI Clients** | Enumera los clientes TCI conectados con un monitor de tráfico en vivo (Pause/Save log/Clear), controles de supresión de comandos de respuesta y detalles por cliente. Nuevo en la v26.8.4. Sujeto a compilación por HAVE_TCI / soporte TCI. |

## Adaptive Frame-Rate Throttle

La sección **Adaptive Frame-Rate Throttle** en Connection Details muestra los valores Current State, Pending Lift y Sessions This Run del acelerador adaptativo. Esta función reduce las velocidades de fotogramas del panadapter cuando se detecta latencia o pérdida de paquetes. Nuevo en la v26.8.4. Oculto hasta que haya datos del acelerador disponibles.

## Controles

| Control                                | Ubicación                                                                                                                                                     | Descripción                                                                                                                                                                                       |
|----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Timeframe**                          | Esquina superior derecha de la barra de pestañas                                                                                                                              | Selecciona cuánto historial muestran los gráficos de series temporales. El valor predeterminado es **5 minutes**. Opciones: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week. Oculto cuando la pestaña **Logs** está activa o en la página **TCI Clients**. |
| **Filter Categories (Logs)**           | Pestaña Logs                                                                                                                                                     | Las casillas de verificación por categoría filtran la vista de registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager.                                                                     |
| **Select All (Logs)**                  | Pestaña Logs                                                                                                                                                     | Muestra todas las categorías de registro en el visor.                                                                                                                                                           |
| **Deselect All (Logs)**                | Pestaña Logs                                                                                                                                                     | Oculta todas las categorías de registro del visor.                                                                                                                                                         |
| **Live / Paused (Logs)**               | Pestaña Logs                                                                                                                                                     | Cuando está en **Live**, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final.                                                        |
| **Search**                             | Encabezado del árbol de navegación                                                                                                                                       | Filtra los elementos del árbol de navegación para mostrar solo aquellos que coinciden con el texto escrito.                                                                                                                     |
| **Navigation tree**                    | Lado izquierdo del cuadro de diálogo                                                                                                                                          | Widget de árbol que enumera todas las páginas de diagnóstico. Haga clic en cualquier elemento para cambiar la vista principal a esa sección.                                                                               |
| **Read-Only Clipboard Copy**           | Página Connection Details                                                                                                                                      | Copia todo el resumen de diagnóstico.                                                                                                                                                             |
| **Close**                              | Parte inferior del cuadro de diálogo                                                                                                                                             | Cierra el cuadro de diálogo.                                                                                                                                                                                |

## Indicadores

| Indicador | Significado |
|-----------|---------|
| **Status** | Calidad general del enlace, codificada por colores de verde a rojo. Estados: Excellent, Very Good, Good, Fair, Poor. |
| **Target Radio IP** | IP de la radio conectada, o "Not connected". |
| **Selected Source** | NIC local/ruta de enlace utilizada para la conexión. |
| **Local TCP** | Punto final TCP local. |
| **Local UDP** | Punto final UDP local. |
| **First UDP Packet** | Si se ha recibido el primer paquete UDP desde la conexión. |
| **Latency (RTT)** | Tiempo de ida y vuelta actual. Puede mostrar "not measured on this link" o "n/a" en transportes sin ida y vuelta que medir. |
| **Max Latency (RTT)** | RTT más alto observado desde la conexión. Puede mostrar "not measured on this link" en transportes sin ida y vuelta que medir. |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Velocidad de ingreso por categoría en kbps. Puede mostrar "n/a" en transportes que no exponen estadísticas por categoría de flujo. |
| **Total RX / Total TX** | Bytes agregados por segundo en cada dirección. |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Conteos de paquetes descartados y porcentaje por categoría. Puede mostrar "n/a" en transportes que no exponen estadísticas por categoría de flujo. |
| **RX Buffer Now / Peak** | Llenado del búfer de audio actual y máximo en bytes y ms. |
| **Underruns (total / last sec)** | Contadores de subdesbordamiento de audio. |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización de llegada entre paquetes. Puede mostrar "not measured on this link" antes de que se cierre la primera ventana de temporización de entrega. |
| **Network Jitter** | Estimación suavizada de jitter del flujo de audio en ms. Puede mostrar "not measured on this link" antes de que se cierre la primera ventana de temporización de entrega. |
| **Adaptive Frame-Rate Throttle** | Valores Current State, Pending Lift y Sessions This Run. Nuevo en la v26.8.4. Oculto hasta que haya datos del acelerador disponibles. |
| **Log path label** | Muestra la ruta completa del archivo de registro que se está siguiendo. |

## Pestaña Logs

La pestaña **Logs** sigue el archivo de registro de AetherSDR en tiempo real. La ruta completa del archivo que se está siguiendo se muestra en la etiqueta de ruta de registro en la parte superior de la pestaña.

La salida del registro tiene resaltado de sintaxis por nivel de registro y nombre de categoría:

- Las marcas de tiempo se muestran en azul grisáceo apagado.
- Las entradas `DBG` se muestran en azul grisáceo apagado.
- Las entradas `INF` se muestran en azul claro.
- Las entradas `WRN` se muestran en ámbar.
- Las entradas `CRT` y `FTL` se muestran en rojo.
- Los nombres de categoría se muestran en gris claro en negrita.
- Los valores numéricos y los tokens de protocolo (por ejemplo, UDP, TCP, VITA-49, RX, TX) se muestran en colores de acento distintos.

Use las casillas de verificación **Filter Categories** para mostrar solo las categorías relevantes al problema que está diagnosticando. Haga clic en **Select All** para restaurar todas las categorías, o en **Deselect All** para limpiar la vista antes de seleccionar categorías específicas. Desplácese hacia arriba para pausar el desplazamiento automático; haga clic en **Live** para reanudar y volver al final.

## Consejos

- Una velocidad de 0 kbps para una categoría que debería estar activa (por ejemplo, **Audio** mientras hay un slice abierto) indica que el flujo ha dejado de llegar. Primero verifique el indicador **Status** en el grupo **Network Status** de la pestaña **Connection Details**.
- Si un indicador de velocidad o latencia muestra "n/a" o "not measured on this link", ese diagnóstico no aplica al transporte conectado actualmente. Esto es distinto de una medición de cero, que indicaría una lectura real de cero.
- Grandes variaciones en la velocidad de una categoría de un segundo a otro pueden indicar entrega en ráfagas incluso cuando el conteo de descartes permanece en cero.
- Cero descartes en el grupo **Packet Loss** no descarta jitter o ráfagas tardías. Si el audio es entrecortado pero los descartes muestran cero, revise el grupo **Audio Playback** en la pestaña **Connection Details** para ver subdesbordamientos y jitter, o revise la pestaña **Audio** para una vista de series temporales del llenado del búfer y subdesbordamientos/s.
- La pestaña **Rates** usa un eje Y logarítmico, lo que facilita ver flujos de baja velocidad (por ejemplo, Meters) junto con flujos de alta velocidad (por ejemplo, total RX) en el mismo gráfico.
- Extienda el selector **Timeframe** a **1 hour** o más al investigar problemas intermitentes que ocurren con poca frecuencia.

## Solución de problemas

- **Todas las velocidades de categoría muestran 0 kbps** — La radio no está transmitiendo. Confirme que la conexión está activa verificando **Status** y **Target Radio IP** en el grupo **Network Status** de la pestaña **Connection Details**. Vuelva a conectar mediante **Settings** > **Connect to Radio...** si es necesario.
- **La velocidad de DAX muestra 0 kbps cuando se espera DAX** — La transmisión de DAX puede no estar habilitada. Verifique que DAX esté iniciado; en plataformas compatibles, revise **Settings** > **Autostart DAX with AetherSDR**.
- **El porcentaje de descartes no es cero en una sola categoría** — La pérdida está aislada a ese flujo. Esto puede indicar que la radio está sobrecargada para ese tipo de datos específico o que una cola de red está descartando preferentemente paquetes UDP de ese tamaño.
- **La pestaña Logs no muestra salida** — Confirme que la etiqueta de ruta de registro muestra una ruta de archivo válida. Si la ruta falta o el archivo no existe, reinicie AetherSDR y vuelva a abrir el cuadro de diálogo.

## Relacionado

- [Network Diagnostics overview](overview.md)
- [Measure RTT and packet drops during audio problems](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnose audio underruns and jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verify the radio's IP and local bind address](verify-the-radio-s-ip-and-local-bind-address.md)
