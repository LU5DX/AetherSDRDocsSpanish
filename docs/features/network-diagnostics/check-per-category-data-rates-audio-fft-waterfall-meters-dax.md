# Diálogo de Diagnóstico de Red

El diálogo de Diagnóstico de Red proporciona una vista completa en vivo del enlace de red con la radio. Cuenta con un diseño de múltiples pestañas que incluye un panel de Resumen con tarjetas de estado y gráficos de series temporales, un panel de Detalles con métricas etiquetadas, pestañas de gráficos por flujo de Latencia / Tasas / Pérdida de Paquetes / Audio, y una pestaña de Registros en vivo para monitorear el archivo de registro filtrado por categoría de diagnóstico.

## Abrir el diálogo

1. Haga clic en **Settings** > **Network...**

El diálogo se abre independientemente de si hay una radio conectada, pero las métricas solo son significativas cuando hay conexión.

## Pestañas

| Pestaña | Descripción |
|---------|-------------|
| **Overview** | Cuatro tarjetas de estado (Estado, Latencia, Pérdida de Paquetes, Búfer de Audio) y cuatro gráficos de series temporales (Latencia y Jitter, Pérdida de Paquetes Reciente, Tasas Totales de Flujo, Búfer de Audio). |
| **Details** | Cuadrícula desplazable con valores etiquetados para los grupos de Estado de Red, Tasas de Flujo de Entrada, Pérdida de Paquetes y Reproducción de Audio. |
| **Latency** | Gráfico de series temporales de ancho completo del RTT, intervalo de llegada y jitter en ms. |
| **Rates** | Gráfico de series temporales de ancho completo con escala logarítmica de las tasas de bits de entrada por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps. |
| **Packet Loss** | Gráfico de series temporales de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo. |
| **Audio** | Gráfico de series temporales de ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s. |
| **Logs** | Monitoreo en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector de **Timeframe** está oculto mientras esta pestaña está activa. |

## Controles

| Control | Ubicación | Descripción |
|---------|-----------|-------------|
| **Timeframe** | Esquina superior derecha de la barra de pestañas | Selecciona cuánto tiempo hacia atrás muestran los gráficos de series temporales. El valor predeterminado es **5 minutes**. Opciones: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week. Oculto cuando la pestaña **Logs** está activa. |
| **Filter Categories (Logs)** | Pestaña Logs | Casillas de verificación por categoría para filtrar la vista de registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager. |
| **Select All (Logs)** | Pestaña Logs | Muestra todas las categorías de registro en el visor. |
| **Deselect All (Logs)** | Pestaña Logs | Oculta todas las categorías de registro del visor. |
| **Live / Paused (Logs)** | Pestaña Logs | Cuando está en **Live**, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final. |
| **Close** | Parte inferior del diálogo | Cierra el diálogo. |

## Indicadores

| Indicador | Significado |
|-----------|-------------|
| **Status** | Calidad general del enlace, codificada por color verde → rojo. Estados: Excellent, Very Good, Good, Fair, Poor. |
| **Target Radio IP** | IP de la radio conectada, o "Not connected". |
| **Selected Source** | NIC local/ruta de enlace utilizada para la conexión. |
| **Local TCP** | Extremo TCP local. |
| **Local UDP** | Extremo UDP local. |
| **First UDP Packet** | Indica si se ha recibido el primer paquete UDP desde la conexión. |
| **Latency (RTT)** | Tiempo de ida y vuelta actual. |
| **Max Latency (RTT)** | RTT más alto observado desde la conexión. |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Tasa de ingreso por categoría en kbps. |
| **Total RX / Total TX** | Bytes agregados por segundo en cada dirección. |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Conteo y porcentaje de paquetes descartados por categoría. |
| **RX Buffer Now / Peak** | Llenado actual y máximo del búfer de audio en bytes y ms. |
| **Underruns (total / last sec)** | Contadores de subejecuciones de audio. |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización de llegada entre paquetes. |
| **Network Jitter** | Estimación de jitter suavizada del flujo de audio en ms. |
| **Log path label** | Muestra la ruta completa del archivo de registro que se está monitoreando. |

## Pestaña Logs

La pestaña **Logs** monitorea el archivo de registro de AetherSDR en tiempo real. La ruta completa del archivo monitoreado se muestra en la etiqueta de ruta de registro en la parte superior de la pestaña.

La salida del registro tiene resaltado de sintaxis por nivel de registro y nombre de categoría:

- Las marcas de tiempo se muestran en gris azulado apagado.
- Las entradas `DBG` se muestran en gris azulado apagado.
- Las entradas `INF` se muestran en azul claro.
- Las entradas `WRN` se muestran en ámbar.
- Las entradas `CRT` y `FTL` se muestran en rojo.
- Los nombres de categoría se muestran en gris claro negrita.
- Los valores numéricos y los tokens de protocolo (por ejemplo, UDP, TCP, VITA-49, RX, TX) se muestran en colores de acento distintivos.

Use las casillas de verificación de **Filter Categories** para mostrar solo las categorías relevantes para el problema que está diagnosticando. Haga clic en **Select All** para restaurar todas las categorías, o en **Deselect All** para limpiar la vista antes de seleccionar categorías específicas. Desplácese hacia arriba para pausar el desplazamiento automático; haga clic en **Live** para reanudar y saltar al final del archivo.

## Consejos

- Una tasa de 0 kbps para una categoría que debería estar activa (por ejemplo, **Audio** mientras hay un slice abierto) indica que el flujo ha dejado de llegar. Primero verifique el indicador **Status** en el grupo **Network Status** de la pestaña **Details**.
- Grandes fluctuaciones en la tasa de una categoría de un segundo a otro pueden indicar una entrega en ráfagas incluso cuando el conteo de descartes permanece en cero.
- Cero descartes en el grupo **Packet Loss** no descarta jitter o ráfagas que llegan tarde. Si el audio es entrecortado pero los descartes muestran cero, revise el grupo **Audio Playback** en la pestaña **Details** para ver subejecuciones y jitter, o revise la pestaña **Audio** para una vista de series temporales del llenado del búfer y subejecuciones/s.
- La pestaña **Rates** utiliza un eje y logarítmico, lo que facilita ver flujos de baja tasa (por ejemplo, Meters) junto con flujos de alta tasa (por ejemplo, RX total) en el mismo gráfico.
- Extienda el selector de **Timeframe** a **1 hour** o más cuando investigue problemas intermitentes que ocurren con poca frecuencia.

## Solución de problemas

- **Todas las tasas de categoría muestran 0 kbps** — La radio no está transmitiendo. Confirme que la conexión esté activa verificando **Status** y **Target Radio IP** en el grupo **Network Status** de la pestaña **Details**. Vuelva a conectarse mediante **Settings** > **Connect to Radio...** si es necesario.
- **La tasa de DAX muestra 0 kbps cuando se espera DAX** — Es posible que la transmisión de DAX no esté habilitada. Verifique que DAX esté iniciado; en plataformas compatibles, revise **Settings** > **Autostart DAX with AetherSDR**.
- **El porcentaje de descartes no es cero en una sola categoría** — La pérdida está aislada en ese flujo. Esto puede indicar que la radio está sobrecargada para ese tipo de datos específico o que una cola de red está descartando preferentemente paquetes UDP de ese tamaño.
- **La pestaña Logs no muestra salida** — Confirme que la etiqueta de ruta de registro muestre una ruta de archivo válida. Si la ruta falta o el archivo no existe, reinicie AetherSDR y vuelva a abrir el diálogo.

## Relacionados

- [Network Diagnostics overview](overview.md)
- [Measure RTT and packet drops during audio problems](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnose audio underruns and jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verify the radio's IP and local bind address](verify-the-radio-s-ip-and-local-bind-address.md)
