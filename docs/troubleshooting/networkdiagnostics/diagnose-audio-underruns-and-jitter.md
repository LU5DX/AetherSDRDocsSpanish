# Diagnosticar subruns de audio y fluctuación (jitter)

Utilice el diálogo de Diagnóstico de Red para leer la salud del búfer de audio en vivo, los contadores de subruns, la sincronización de los intervalos de llegada y las estimaciones de fluctuación. Esto le ayuda a identificar si las interrupciones de audio son causadas por un búfer agotado, una entrega de paquetes irregular o fluctuación de red.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión de radio activa, pero los indicadores de audio solo son significativos mientras una radio está conectada y transmitiendo audio.
- Reproduzca el problema de audio antes de abrir el diálogo para que los contadores y los valores máximos reflejen la condición de la falla.
- La geometría de la ventana del diálogo se guarda y restaura automáticamente entre sesiones.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo de Diagnóstico de Red.
2. Utilice el árbol de navegación a la izquierda para seleccionar la vista que necesita:
   - **Overview** – Tarjetas de salud y gráficos de series de tiempo resumidos.
   - **Connection Details** – Cuadrícula desplazable de todas las métricas etiquetadas, incluida la sección Adaptive Frame-Rate Throttle.
   - **Latency** – Gráfico de RTT, intervalo de llegada y fluctuación.
   - **Rates** – Gráfico de velocidad de bits entrante por flujo.
   - **Packet Loss** – Gráfico de porcentaje de pérdida de paquetes por categoría.
   - **Audio** – Gráfico de llenado del búfer de reproducción y tasa de subruns. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, el déficit, los paquetes tardíos, el código de clase de paquete y la salud del flujo para cada flujo de audio activo.
   - **Logs** – Cola en vivo del archivo de registro de AetherSDR.
   - **TCI Clients** – Lista los clientes TCI conectados con un monitor de tráfico en vivo (disponible solo en compilaciones con TCI habilitado).
3. En la vista **Connection Details**, localice el grupo **Audio Playback**.
4. Lea **RX Buffer Now** para ver cuántos bytes (y milisegundos) de audio se mantienen actualmente en el búfer de reproducción.
5. Lea **RX Buffer Peak** para ver el llenado más alto del búfer registrado desde que se abrió el diálogo.
6. Lea **Underruns (total)** para ver el conteo acumulado de subruns del búfer desde que se inició el motor de audio.
7. Lea **Underruns (last sec)** para ver cuántos subruns ocurrieron en la ventana de un segundo más reciente. Un valor distinto de cero aquí mientras el audio se transmite activamente indica un problema en curso.
8. Lea **Audio Arrival Gap** para ver el intervalo de llegada entre paquetes actual. Un valor significativamente mayor que el período esperado de paquetes indica entrega irregular.
9. Lea **Max Arrival Gap** para ver el peor intervalo de llegada registrado desde que se abrió el diálogo.
10. Lea **Network Jitter** para ver la estimación suavizada de fluctuación para el flujo de audio.
11. En la vista **Connection Details**, localice la sección **Adaptive Frame-Rate Throttle** para ver el Estado Actual, el Levantamiento Pendiente y las Sesiones de Esta Ejecución del regulador.
12. Si los subruns aumentan pero **RX Buffer Now** se mantiene cerca de cero, el búfer se está agotando — consulte los consejos a continuación.
13. Haga clic en **Close** cuando termine.

## Qué hace cada control

### Navegación y búsqueda

| Control                    | Tipo        | Predeterminado | Comportamiento                                                                                                                                 |
|----------------------------|-------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Navigation tree**        | Widget de árbol | –         | Barra lateral izquierda que enumera todas las vistas de diagnóstico (Overview, Connection Details, Latency, Rates, Packet Loss, Audio, Logs, TCI Clients). Haga clic en un elemento para cambiar de vista. El elemento del árbol tiene una altura mínima de 38px y se resalta con el color de acento cuando está seleccionado. |
| **Search**                 | Entrada de texto | –         | Cuadro de búsqueda con filtro en la parte superior del diálogo. El estilo de enfoque muestra un borde de acento brillante. Escriba texto para filtrar la información mostrada. |
| **Timeframe**              | Cuadro combinado | 5 minutes | Selecciona cuánto tiempo atrás muestran los gráficos de series de tiempo su historial. Opciones: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week. Se muestra en la esquina superior derecha del diálogo; oculto cuando la vista Logs o TCI Clients está activa. |

### Vistas

| Vista                  | Comportamiento                                                                                                                                       |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| **Overview**          | Muestra cuatro tarjetas de salud (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series de tiempo (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). |
| **Connection Details**| Cuadrícula desplazable con valores etiquetados para Network Status, Incoming Stream Rates, Packet Loss, Audio Playback y la sección Adaptive Frame-Rate Throttle. Incluye una acción Read-Only Clipboard Copy para copiar todo el resumen de diagnóstico. |
| **Latency**           | Gráfico de series de tiempo de ancho completo de RTT, intervalo de llegada y fluctuación en ms. |
| **Rates**             | Gráfico de series de tiempo a escala logarítmica de ancho completo de velocidades de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps. |
| **Packet Loss**       | Gráfico de series de tiempo de ancho completo del % de pérdida de paquetes por categoría de flujo. |
| **Audio**             | Gráfico de series de tiempo de ancho completo del llenado del búfer de reproducción (ms) y subruns/s. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, el déficit, los paquetes tardíos, el código de clase de paquete y la salud del flujo para cada flujo de audio activo. |
| **Logs**              | Cola en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector de Timeframe se oculta mientras esta vista está activa. |
| **TCI Clients**       | Lista los clientes TCI conectados con un monitor de tráfico en vivo (Pause/Save log/Clear), controles de supresión de comandos de respuesta y detalles por cliente. El selector de Timeframe se oculta en esta página. Disponible solo en compilaciones con TCI habilitado. |

### Controles

| Control                    | Tipo        | Predeterminado | Comportamiento                                                                                                                                 |
|----------------------------|-------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Filter Categories (Logs)** | Casillas de verificación | –         | Las casillas de verificación por categoría filtran la vista de registro. Incluyen una categoría General (predeterminada) más todas las categorías registradas de LogManager. |
| **Select All (Logs)**      | Botón pulsador | –         | Muestra todas las categorías de registro en el visor. |
| **Deselect All (Logs)**    | Botón pulsador | –         | Oculta todas las categorías de registro del visor. |
| **Live / Paused (Logs)**   | Botón de alternancia | Live    | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta a la cola. |
| **Close**                  | Botón pulsador | –         | Cierra el diálogo. |
| **Page Title**             | Etiqueta       | –         | Muestra el nombre de la vista seleccionada actualmente en el área de contenido principal. La fuente es de 20px en negrita con el color de texto primario. |

### Indicadores

Todos los indicadores se actualizan una vez por segundo.

| Indicador               | Significado                                                                                                  |
|--------------------------|----------------------------------------------------------------------------------------------------------|
| **Status**              | Calidad general del enlace, codificada por color verde → rojo. Estados: Excellent, Very Good, Good, Fair, Poor. |
| **Target Radio IP**     | IP de la radio conectada, o "Not connected". |
| **Selected Source**     | NIC local/ruta de enlace utilizada para la conexión. |
| **Local TCP**           | Punto final TCP local. |
| **Local UDP**           | Punto final UDP local. |
| **First UDP Packet**    | Si el primer paquete UDP se ha recibido desde la conexión. Estados: Yes, No. |
| **Latency (RTT)**       | Tiempo de ida y vuelta actual. Muestra "not measured on this link" cuando el transporte no tiene un viaje de ida y vuelta que medir. |
| **Max Latency (RTT)**   | RTT más alto visto desde la conexión. Muestra "not measured on this link" cuando el transporte no tiene un viaje de ida y vuelta que medir. |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Tasa de ingreso por categoría en kbps. Muestra "n/a" cuando el transporte no admite estadísticas por categoría de flujo. |
| **Total RX / Total TX** | Bytes agregados por segundo en cada dirección. |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Conteos y porcentaje de paquetes descartados por categoría. Muestra "n/a" cuando el transporte no admite estadísticas por categoría de flujo. |
| **RX Buffer Now / Peak**| Llenado actual y máximo del búfer de audio en bytes y ms. |
| **Underruns (total / last sec)** | Contadores de subruns de audio. |
| **Audio Arrival Gap / Max Arrival Gap** | Sincronización de llegada entre paquetes. Muestra "not measured on this link" cuando los datos de sincronización no están disponibles. |
| **Network Jitter**      | Estimación suavizada de fluctuación del flujo de audio en ms. Muestra "not measured on this link" cuando los datos de sincronización no están disponibles. |
| **Log path label**      | Muestra la ruta completa del archivo de registro que se está siguiendo. |
| **Feed Rate**           | Tasa de alimentación de audio actual para cada flujo activo. |
| **Deficit**             | Déficit de audio actual para cada flujo activo. |
| **Late Packets**        | Conteo de paquetes tardíos para cada flujo de audio activo. |
| **Packet Class Code**   | Código de clase de paquete para cada flujo de audio activo. |
| **Stream Health**       | Estado de salud para cada flujo de audio activo. |
| **Adaptive Frame-Rate Throttle: Current State** | Estado actual del regulador adaptativo. |
| **Adaptive Frame-Rate Throttle: Pending Lift** | Si un levantamiento del regulador está pendiente. |
| **Adaptive Frame-Rate Throttle: Sessions This Run** | Número de sesiones del regulador desde que comenzó la conexión. |

## Uso de la vista Logs

La vista Logs proporciona una cola en vivo del archivo de registro de AetherSDR directamente dentro del diálogo de Diagnóstico de Red.

1. Haga clic en **Logs** en el árbol de navegación. El selector **Timeframe** en la esquina superior derecha se oculta mientras esta vista está activa.
2. La ruta del registro se muestra en la parte superior de la vista. Esta es la ruta completa del archivo que se está siguiendo.
3. Use las casillas de verificación **Filter Categories (Logs)** para incluir o excluir categorías de registro específicas. La categoría General está disponible por defecto; categorías adicionales aparecen según LogManager las registra.
4. Haga clic en **Select All (Logs)** para habilitar todas las categorías a la vez. Haga clic en **Deselect All (Logs)** para ocultar todas las categorías.
5. El visor está en modo **Live** por defecto y se desplaza automáticamente a la salida más reciente. Desplácese hacia arriba para pausar el desplazamiento automático; el botón cambia a **Paused**. Haga clic en **Live** para reanudar y volver a la cola.
6. Las entradas de registro tienen resaltado de sintaxis por nivel de registro (debug, info, warning, critical) y nombre de categoría.

## Uso de la vista TCI Clients

La vista TCI Clients lista los clientes TCI conectados y proporciona un monitor de tráfico en vivo. Esta vista solo está disponible en compilaciones con soporte TCI habilitado.

1. Haga clic en **TCI Clients** en el árbol de navegación. El selector **Timeframe** en la esquina superior derecha se oculta mientras esta vista está activa.
2. Revise la lista de clientes TCI conectados y sus detalles por cliente.
3. Use los controles del monitor de tráfico para **Pause** la vista en vivo, **Save log** en disco o **Clear** los datos de tráfico actuales.
4. Use los controles de supresión de comandos de respuesta para gestionar cómo responde la radio a los comandos de los clientes TCI.

## Comprensión de los ejes de los gráficos

Los gráficos de series de tiempo en todo el diálogo utilizan un escalado de ejes consistente:

- **Escala lineal**: Las marcas del eje Y están espaciadas uniformemente desde el valor mínimo hasta el máximo.
- **Escala logarítmica** (vista Rates): El eje Y utiliza espaciado logarítmico con una línea base de "0" mostrada en la parte inferior. Los valores en o por debajo de 1 unidad se consideran funcionalmente cero.
- **Rango Y fijo**: Algunos gráficos pueden usar un rango Y mínimo y máximo fijo para una comparación consistente entre diferentes marcos de tiempo.
- **Serie no medida**: En transportes que no tienen un viaje de ida y vuelta que medir (como un enlace de flujo único), la serie RTT se omite del gráfico Latency en lugar de dibujarse como una línea plana de 0 ms.

## Comprensión del Adaptive Frame-Rate Throttle

El Adaptive Frame-Rate Throttle reduce las velocidades de fotogramas del panadapter cuando se detecta latencia o pérdida de paquetes, ayudando a mantener un flujo de audio estable en condiciones de red degradadas.

1. Abra la vista **Connection Details**.
2. Localice la sección **Adaptive Frame-Rate Throttle**. Esta sección está oculta hasta que los datos del regulador estén disponibles.
3. Lea **Current State** para ver si el regulador está activo o inactivo.
4. Lea **Pending Lift** para ver si un levantamiento del regulador está pendiente.
5. Lea **Sessions This Run** para ver cuántas sesiones del regulador han ocurrido desde que comenzó la conexión.

## Comprensión de "not measured on this link"

En v26.8.4, ciertos indicadores de latencia y sincronización muestran "not measured on this link" cuando el transporte actual no puede producir esa medición. Esto es distinto de un valor de "0" o "< 1 ms": significa que la medición no existe para este tipo de enlace, no que el valor sea cero.

- **Latency (RTT)** y **Max Latency (RTT)** muestran "not measured on this link" cuando el transporte no tiene un viaje de ida y vuelta que medir.
- **Audio Arrival Gap**, **Max Arrival Gap** y **Network Jitter** muestran "not measured on this link" hasta que la primera ventana de sincronización de entrega se haya cerrado (un backend se considera "reportado" desde su primer tick, un segundo antes de que cierre su primera ventana de sincronización).

## Consejos

- **Subruns en aumento, búfer cerca de cero:** El flujo de audio no está llegando lo suficientemente rápido para mantener el búfer lleno. Verifique la tasa **Audio** en el grupo **Incoming Stream Rates** y compárela con la velocidad de bits esperada. Una tasa de Audio muy baja o cero significa que los pa
