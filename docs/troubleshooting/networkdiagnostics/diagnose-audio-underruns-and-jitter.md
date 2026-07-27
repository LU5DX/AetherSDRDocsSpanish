# Diagnosticar subejecuciones de audio y fluctuación

Use el cuadro de diálogo Diagnóstico de Red para leer indicadores en vivo de salud del búfer de audio, contadores de subejecuciones, temporización de intervalo de llegada y estimaciones de fluctuación. Esto le ayuda a identificar si los cortes de audio son causados por un búfer insuficiente, entrega de paquetes en ráfagas o fluctuación de red.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El cuadro de diálogo no requiere una conexión de radio activa, pero los indicadores de audio solo son significativos mientras una radio está conectada y transmitiendo audio.
- Reproduzca el problema de audio antes de abrir el cuadro de diálogo para que los contadores y valores pico reflejen la condición de falla.
- La geometría de la ventana del cuadro de diálogo se guarda y restaura automáticamente entre sesiones.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el cuadro de diálogo Diagnóstico de Red.
2. Use el árbol de navegación a la izquierda para seleccionar la vista que necesita:
   - **Overview** – Tarjetas de salud y gráficos de series temporales resumidos.
   - **Details** – Cuadrícula desplazable de todas las métricas etiquetadas.
   - **Latency** – Gráfico de RTT, intervalo de llegada y fluctuación.
   - **Rates** – Gráfico de tasa de bits entrante por flujo.
   - **Packet Loss** – Gráfico de porcentaje de pérdida de paquetes por categoría.
   - **Audio** – Gráfico de llenado del búfer de reproducción y tasa de subejecuciones. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y salud del flujo para cada flujo de audio activo.
   - **Logs** – Visualización en vivo del archivo de registro de AetherSDR.
3. En la vista **Details**, localice el grupo **Audio Playback**.
4. Lea **RX Buffer Now** para ver cuántos bytes (y milisegundos) de audio se mantienen actualmente en el búfer de reproducción.
5. Lea **RX Buffer Peak** para ver el llenado de búfer más alto registrado desde que se abrió el cuadro de diálogo.
6. Lea **Underruns (total)** para ver el recuento acumulativo de subejecuciones de búfer desde que se inició el motor de audio.
7. Lea **Underruns (last sec)** para ver cuántas subejecuciones ocurrieron en la ventana de un segundo más reciente. Un valor distinto de cero aquí mientras el audio se transmite activamente indica un problema en curso.
8. Lea **Audio Arrival Gap** para ver el intervalo de llegada entre paquetes actual. Un valor significativamente mayor que el período de paquete esperado indica entrega en ráfagas.
9. Lea **Max Arrival Gap** para ver el peor intervalo de llegada registrado desde que se abrió el cuadro de diálogo.
10. Lea **Network Jitter** para ver la estimación de fluctuación suavizada para el flujo de audio.
11. Si las subejecuciones aumentan pero **RX Buffer Now** permanece cerca de cero, el búfer se está quedando sin datos; consulte los consejos a continuación.
12. Haga clic en **Close** cuando termine.

## Qué hace cada control

### Navegación y búsqueda

| Control                     | Tipo          | Predeterminado | Comportamiento                                                                                                                                          |
|-----------------------------|---------------|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Navigation tree**         | Widget de árbol | –              | Barra lateral izquierda que lista todas las vistas de diagnóstico (Overview, Details, Latency, Rates, Packet Loss, Audio, Logs). Haga clic en un elemento para cambiar de vista. El elemento del árbol tiene una altura mínima de 38 px y se resalta con el color de acento cuando está seleccionado. |
| **Search**                  | Entrada de texto | –              | Cuadro de búsqueda de filtro en la parte superior del cuadro de diálogo. El estilo de enfoque muestra un borde de acento brillante. Introduzca texto para filtrar la información mostrada. |
| **Timeframe**               | Cuadro combinado | 5 minutos      | Selecciona cuánto tiempo atrás muestran el historial los gráficos de series temporales. Opciones: 1 minuto, 5 minutos, 15 minutos, 1 hora, 1 día, 1 semana. Se muestra en la esquina superior derecha del cuadro de diálogo; oculto cuando la vista Logs está activa. |

### Vistas

| Vista              | Comportamiento                                                                                                                                    |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| **Overview**       | Muestra cuatro tarjetas de salud (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). |
| **Details**        | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.               |
| **Latency**        | Gráfico de series temporales de ancho completo de RTT, intervalo de llegada y fluctuación en ms.                                                  |
| **Rates**          | Gráfico de series temporales de ancho completo con escala logarítmica de tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps. |
| **Packet Loss**    | Gráfico de series temporales de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.                                      |
| **Audio**          | Gráfico de series temporales de ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y salud del flujo para cada flujo de audio activo. |
| **Logs**           | Visualización en vivo del archivo de registro de AetherSDR, filtrada por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector de Timeframe está oculto mientras esta vista está activa. |

### Controles

| Control                       | Tipo            | Predeterminado | Comportamiento                                                                                                                                    |
|-------------------------------|-----------------|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| **Filter Categories (Logs)**  | Casillas de verificación | –      | Casillas de verificación por categoría que filtran la vista de registros. Incluye una categoría General (predeterminada) más todas las categorías registradas por LogManager. |
| **Select All (Logs)**         | Botón pulsador  | –              | Muestra todas las categorías de registro en el visor.                                                                                             |
| **Deselect All (Logs)**       | Botón pulsador  | –              | Oculta todas las categorías de registro del visor.                                                                                                |
| **Live / Paused (Logs)**      | Botón de alternancia | Live       | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final. |
| **Close**                     | Botón pulsador  | –              | Cierra el cuadro de diálogo.                                                                                                                      |
| **Page Title**                | Etiqueta        | –              | Muestra el nombre de la vista actualmente seleccionada en el área de contenido principal. La fuente es de 20 px en negrita con color de texto primario. |

### Indicadores

Todos los indicadores se actualizan una vez por segundo.

| Indicador                  | Significado                                                                                                    |
|----------------------------|----------------------------------------------------------------------------------------------------------------|
| **Status**                 | Calidad general del enlace, codificada por color verde → rojo. Estados: Excellent, Very Good, Good, Fair, Poor. |
| **Target Radio IP**        | IP de la radio conectada, o "Not connected".                                                                  |
| **Selected Source**        | NIC local/ruta de enlace utilizada para la conexión.                                                           |
| **Local TCP**              | Extremo TCP local.                                                                                             |
| **Local UDP**              | Extremo UDP local.                                                                                             |
| **First UDP Packet**       | Indica si se ha recibido el primer paquete UDP desde la conexión. Estados: Yes, No.                            |
| **Latency (RTT)**          | Tiempo de ida y vuelta actual.                                                                                 |
| **Max Latency (RTT)**      | RTT más alto visto desde la conexión.                                                                          |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Tasa de ingreso por categoría en kbps.                                                      |
| **Total RX / Total TX**    | Bytes agregados por segundo en cada dirección.                                                                 |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Recuentos y porcentaje de paquetes descartados por categoría.                              |
| **RX Buffer Now / Peak**   | Llenado actual y máximo del búfer de audio en bytes y ms.                                                      |
| **Underruns (total / last sec)** | Contadores de subejecuciones de audio.                                                               |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización de llegada entre paquetes.                                                    |
| **Network Jitter**         | Estimación de fluctuación suavizada del flujo de audio en ms.                                                  |
| **Log path label**         | Muestra la ruta completa del archivo de registro que se está siguiendo.                                         |
| **Feed Rate**              | Tasa de alimentación de audio actual para cada flujo activo.                                                   |
| **Deficit**                | Déficit de audio actual para cada flujo activo.                                                                |
| **Late Packets**           | Recuento de paquetes tardíos para cada flujo de audio activo.                                                  |
| **Packet Class Code**      | Código de clase de paquete para cada flujo de audio activo.                                                    |
| **Stream Health**          | Estado de salud para cada flujo de audio activo.                                                               |

## Uso de la vista Logs

La vista Logs proporciona una visualización en vivo del archivo de registro de AetherSDR directamente dentro del cuadro de diálogo Diagnóstico de Red.

1. Haga clic en **Logs** en el árbol de navegación. El selector **Timeframe** en la esquina superior derecha está oculto mientras esta vista está activa.
2. La ruta del registro se muestra en la parte superior de la vista. Esta es la ruta completa del archivo que se está siguiendo.
3. Use las casillas de verificación **Filter Categories (Logs)** para incluir o excluir categorías de registro específicas. La categoría General está disponible de forma predeterminada; aparecen categorías adicionales a medida que LogManager las registra.
4. Haga clic en **Select All (Logs)** para habilitar todas las categorías a la vez. Haga clic en **Deselect All (Logs)** para ocultar todas las categorías.
5. El visor está en modo **Live** de forma predeterminada y se desplaza automáticamente a la salida más reciente. Desplácese hacia arriba para pausar el desplazamiento automático; el botón cambia a **Paused**. Haga clic en **Live** para reanudar y saltar al final.
6. Las entradas de registro tienen resaltado de sintaxis por nivel de registro (debug, info, warning, critical) y nombre de categoría.

## Comprensión de los ejes de los gráficos

Los gráficos de series temporales en todo el cuadro de diálogo usan un escalado de ejes consistente:

- **Escala lineal**: Las marcas del eje Y están espaciadas uniformemente desde el valor mínimo hasta el máximo.
- **Escala logarítmica** (vista Rates): El eje Y usa un espaciado logarítmico con una línea base de "0" mostrada en la parte inferior. Los valores en o por debajo de 1 unidad se consideran funcionalmente cero.
- **Rango Y fijo**: Algunos gráficos pueden usar un rango Y mínimo y máximo fijo para una comparación consistente en diferentes marcos de tiempo.

## Consejos

- **Subejecuciones aumentando, búfer cerca de cero:** El flujo de audio no llega lo suficientemente rápido para mantener el búfer lleno. Verifique la tasa de **Audio** en el grupo **Incoming Stream Rates** y compárela con la tasa de bits esperada. Una tasa de Audio muy baja o cero significa que los paquetes no llegan en absoluto.
- **Pérdida de paquetes cero pero aún aparecen subejecuciones:** El grupo **Packet Loss (Sequence Gaps)** solo cuenta los números de secuencia VITA faltantes. Los paquetes que llegan tarde en lugar de faltantes no incrementarán el contador de descartes, pero aún causarán fluctuación y subejecuciones. Use **Audio Arrival Gap** y **Network Jitter** para detectar esta condición.
- **Max Arrival Gap grande con gap promedio bajo:** Esto indica ráfagas ocasionales de paquetes retrasados en lugar de pérdida sostenida. Aísle la ruta de red hacia la radio y verifique si hay tráfico en competencia.
- **RX Buffer Peak es muy bajo:** El búfer nunca acumuló una reserva útil. Esto hace que el flujo sea sensible a cualquier variación en la entrega. Verifique la ruta de red y considere si otro tráfico pesado compite en el mismo enlace.
- **Investigando desconexiones o errores inesperados:** Abra la vista **Logs** y active las categorías de LogManager relevantes. Use **Filter Categories (Logs)** para enfocarse en la categoría de interés, luego reproduzca la falla mientras el visor está en modo **Live**.
- **Diagnósticos de audio RX por flujo:** En la vista **Audio**, revise la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y salud del flujo para cada flujo de audio activo. Esto ayuda a identificar problemas de flujo individuales que pueden no afectar a otros flujos.

## Solución de problemas

- **Todos los indicadores de audio muestran cero o ningún dato** — La radio no está transmitiendo audio. Confirme que la radio está conectada y que un receptor (slice) está activo.
- **Underruns (last sec) es distinto de cero pero Underruns (total) es pequeño** — El problema es intermitente. Deje el cuadro de diálogo abierto y espere un período de observación más largo. Observe **Max Arrival Gap** para encontrar evidencia de ráfagas periódicas.
- **Network Jitter es alto pero Audio drops muestra cero** — Los paquetes llegan tarde en lugar de perderse. La fluctuación reduce directamente el margen efectivo del búfer. Verifique si hay otro tráfico UDP compitiendo en la misma interfaz.
- **La vista Logs no muestra salida** — Confirme que la ruta del archivo de registro que se muestra en la parte superior de la vista es accesible. Si no hay categorías marcadas, haga clic en **Select All (Logs)** para restaurar la visibilidad.

## Relacionados

- [Descripción general de Diagnóstico de Red](../../features/network-diagnostics/overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar tasas de datos por categoría (audio, FFT, waterfall, meters, DAX)](../../features/network-diagnostics/check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
