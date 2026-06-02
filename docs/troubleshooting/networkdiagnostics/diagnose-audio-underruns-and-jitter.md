# Diagnosticar subejecuciones de audio y fluctuación

Use el cuadro de diálogo Diagnóstico de Red para leer indicadores en vivo de salud del búfer de audio, recuentos de subejecuciones, temporización de intervalos de llegada y estimaciones de fluctuación. Esto ayuda a identificar si las interrupciones de audio son causadas por un búfer insuficiente, entrega de paquetes en ráfagas o fluctuación de red.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. El cuadro de diálogo no requiere una conexión de radio activa, pero los indicadores de audio solo son significativos mientras una radio está conectada y transmitiendo audio.
- Reproduzca el problema de audio antes de abrir el cuadro de diálogo para que los contadores y valores pico reflejen la condición de falla.
- La geometría de la ventana del cuadro de diálogo se guarda y restaura automáticamente entre sesiones.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el cuadro de diálogo Diagnóstico de Red.
2. Use la barra de pestañas en la parte superior para seleccionar la vista que necesite:
   - **Overview** – Tarjetas de estado y gráficos resumidos de series temporales.
   - **Details** – Cuadrícula desplazable de todas las métricas etiquetadas.
   - **Latency** – Gráfico de RTT, intervalo de llegada y fluctuación.
   - **Rates** – Gráfico de tasa de bits entrante por flujo.
   - **Packet Loss** – Gráfico de porcentaje de pérdida de paquetes por categoría.
   - **Audio** – Gráfico de llenado del búfer de reproducción y tasa de subejecuciones. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y salud del flujo para cada flujo de audio activo.
   - **Logs** – Visualización en vivo del archivo de registro de AetherSDR.
3. En la pestaña **Details**, localice el grupo **Audio Playback**.
4. Lea **RX Buffer Now** para ver cuántos bytes (y milisegundos) de audio se mantienen actualmente en el búfer de reproducción.
5. Lea **RX Buffer Peak** para ver el llenado máximo del búfer registrado desde que se abrió el cuadro de diálogo.
6. Lea **Underruns (total)** para ver el recuento acumulativo de subejecuciones del búfer desde que se inició el motor de audio.
7. Lea **Underruns (last sec)** para ver cuántas subejecuciones ocurrieron en la ventana de un segundo más reciente. Un valor distinto de cero aquí mientras el audio se está transmitiendo activamente indica un problema en curso.
8. Lea **Audio Arrival Gap** para ver el intervalo de llegada actual entre paquetes. Un valor significativamente mayor que el período esperado de paquetes indica entrega en ráfagas.
9. Lea **Max Arrival Gap** para ver el peor caso de intervalo de llegada registrado desde que se abrió el cuadro de diálogo.
10. Lea **Network Jitter** para ver la estimación de fluctuación suavizada para el flujo de audio.
11. Si las subejecuciones están aumentando pero **RX Buffer Now** se mantiene cerca de cero, el búfer está insuficiente; consulte los consejos a continuación.
12. Haga clic en **Close** para finalizar.

## Qué hace cada control

### Pestañas

| Pestaña         | Comportamiento                                                                                                                                                     |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Overview**    | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). |
| **Details**     | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                |
| **Latency**     | Gráfico de series temporales de ancho completo de RTT, intervalo de llegada y fluctuación en ms.                                                                  |
| **Rates**       | Gráfico de series temporales de ancho completo en escala logarítmica de tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps. |
| **Packet Loss** | Gráfico de series temporales de ancho completo del % de pérdida de paquetes por categoría de flujo.                                                                |
| **Audio**       | Gráfico de series temporales de ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y salud del flujo para cada flujo de audio activo. |
| **Logs**        | Visualización en vivo del archivo de registro de AetherSDR, filtrada por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. El selector de marco temporal se oculta mientras esta pestaña está activa. |

### Controles

| Control                          | Tipo            | Valor predeterminado | Comportamiento                                                                                                                                                  |
|----------------------------------|-----------------|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Timeframe**                    | Cuadro combinado | 5 minutes            | Selecciona cuánto tiempo atrás muestran los gráficos de series temporales el historial. Opciones: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week. Se muestra en la esquina superior derecha de la barra de pestañas; oculto cuando la pestaña Logs está activa. |
| **Filter Categories (Logs)**     | Casillas de verificación | –             | Las casillas de verificación por categoría filtran la vista de registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager. |
| **Select All (Logs)**            | Botón           | –                    | Muestra todas las categorías de registro en el visor.                                                                                                           |
| **Deselect All (Logs)**          | Botón           | –                    | Oculta todas las categorías de registro del visor.                                                                                                              |
| **Live / Paused (Logs)**         | Botón de alternancia | Live               | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final. |
| **Close**                        | Botón           | –                    | Cierra el cuadro de diálogo.                                                                                                                                    |

### Indicadores

Todos los indicadores se actualizan una vez por segundo.

| Indicador                        | Significado                                                                                                                         |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| **Status**                       | Calidad general del enlace, codificada por color verde → rojo. Estados: Excellent, Very Good, Good, Fair, Poor.                     |
| **Target Radio IP**              | IP de la radio conectada, o "Not connected".                                                                                        |
| **Selected Source**              | NIC local/ruta de enlace utilizada para la conexión.                                                                                |
| **Local TCP**                    | Punto final TCP local.                                                                                                              |
| **Local UDP**                    | Punto final UDP local.                                                                                                              |
| **First UDP Packet**             | Si el primer paquete UDP se ha recibido desde la conexión. Estados: Yes, No.                                                        |
| **Latency (RTT)**                | Tiempo de ida y vuelta actual.                                                                                                      |
| **Max Latency (RTT)**            | RTT más alto visto desde la conexión.                                                                                               |
| **Rates de Audio / FFT / Waterfall / Meters / DAX** | Tasa de ingreso por categoría en kbps.                                                                              |
| **Total RX / Total TX**          | Bytes agregados por segundo en cada dirección.                                                                                      |
| **Drops de Audio / FFT / Waterfall / Meters / DAX** | Conteos de paquetes descartados y porcentaje por categoría.                                                      |
| **RX Buffer Now / Peak**         | Llenado actual y máximo del búfer de audio en bytes y ms.                                                                           |
| **Underruns (total / last sec)** | Contadores de subejecuciones de audio.                                                                                              |
| **Audio Arrival Gap / Max Arrival Gap** | Temporización de llegada entre paquetes.                                                                                     |
| **Network Jitter**               | Estimación de fluctuación suavizada del flujo de audio en ms.                                                                       |
| **Etiqueta de ruta de registro** | Muestra la ruta completa del archivo de registro que se está monitoreando.                                                          |
| **Feed Rate**                    | Tasa de alimentación de audio actual para cada flujo activo.                                                                        |
| **Deficit**                      | Déficit de audio actual para cada flujo activo.                                                                                     |
| **Late Packets**                 | Conteo de paquetes tardíos para cada flujo de audio activo.                                                                         |
| **Packet Class Code**            | Código de clase de paquete para cada flujo de audio activo.                                                                         |
| **Stream Health**                | Estado de salud para cada flujo de audio activo.                                                                                    |

## Uso de la pestaña Logs

La pestaña Logs proporciona una visualización en vivo del archivo de registro de AetherSDR directamente dentro del cuadro de diálogo Diagnóstico de Red.

1. Haga clic en la pestaña **Logs**. El selector **Timeframe** en la esquina superior derecha se oculta mientras esta pestaña está activa.
2. La ruta del registro se muestra en la parte superior de la pestaña. Esta es la ruta completa del archivo que se está monitoreando.
3. Use las casillas de verificación **Filter Categories (Logs)** para incluir o excluir categorías de registro específicas. La categoría General está disponible de forma predeterminada; aparecen categorías adicionales a medida que LogManager las registra.
4. Haga clic en **Select All (Logs)** para habilitar todas las categorías a la vez. Haga clic en **Deselect All (Logs)** para ocultar todas las categorías.
5. El visor está en modo **Live** de forma predeterminada y se desplaza automáticamente a la salida más reciente. Desplácese hacia arriba para pausar el desplazamiento automático; el botón cambia a **Paused**. Haga clic en **Live** para reanudar y saltar de nuevo al final.
6. Las entradas de registro tienen resaltado de sintaxis por nivel de registro (debug, info, warning, critical) y nombre de categoría.

## Consejos

- **Subejecuciones aumentando, búfer cerca de cero:** El flujo de audio no llega lo suficientemente rápido para mantener el búfer lleno. Verifique la tasa **Audio** en el grupo **Incoming Stream Rates** y compárela con la tasa de bits esperada. Una tasa de Audio muy baja o cero significa que los paquetes no llegan en absoluto.
- **Pérdida de paquetes cero pero aún hay subejecuciones:** El grupo **Packet Loss (Sequence Gaps)** solo cuenta números de secuencia VITA faltantes. Los paquetes que llegan tarde en lugar de faltar no incrementarán el contador de caídas, pero seguirán causando fluctuación y subejecuciones. Use **Audio Arrival Gap** y **Network Jitter** para detectar esta condición.
- **Max Arrival Gap grande con gap promedio bajo:** Esto indica ráfagas ocasionales de paquetes retrasados en lugar de pérdida sostenida. Aísle la ruta de red hacia la radio y verifique si hay tráfico en competencia.
- **RX Buffer Peak es muy bajo:** El búfer nunca acumuló una reserva útil. Esto hace que el flujo sea sensible a cualquier variación en la entrega. Verifique la ruta de red y considere si otro tráfico pesado compite en el mismo enlace.
- **Investigando desconexiones o errores inesperados:** Abra la pestaña **Logs** y habilite las categorías relevantes de LogManager. Use **Filter Categories (Logs)** para enfocarse en la categoría de interés, luego reproduzca la falla mientras el visor está en modo **Live**.
- **Diagnósticos de audio RX por flujo:** En la pestaña **Audio**, revise la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y salud del flujo para cada flujo de audio activo. Esto ayuda a identificar problemas de flujo individuales que pueden no afectar a otros flujos.

## Solución de problemas

- **Todos los indicadores de audio muestran cero o sin datos** — La radio no está transmitiendo audio. Confirme que la radio está conectada y que un slice receptor está activo.
- **Underruns (last sec) es distinto de cero pero Underruns (total) es pequeño** — El problema es intermitente. Deje el cuadro de diálogo abierto y espere un período de observación más largo. Observe **Max Arrival Gap** en busca de evidencia de ráfagas periódicas.
- **Network Jitter es alto pero Audio drops muestra cero** — Los paquetes llegan tarde en lugar de perderse. La fluctuación reduce directamente el margen efectivo del búfer. Verifique si hay otro tráfico UDP compitiendo en la misma interfaz.
- **La pestaña Logs no muestra salida** — Confirme que la ruta del archivo de registro que se muestra en la parte superior de la pestaña sea accesible. Si no hay categorías marcadas, haga clic en **Select All (Logs)** para restaurar la visibilidad.

## Relacionado

- [Network Diagnostics overview](../../features/network-diagnostics/overview.md)
- [Measure RTT and packet drops during audio problems](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](../../features/network-diagnostics/check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
