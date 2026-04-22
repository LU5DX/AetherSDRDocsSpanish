# Diagnóstico de interrupciones de audio y jitter

Use el diálogo Network Diagnostics para observar en tiempo real el búfer de audio, los contadores de interrupciones, el intervalo de llegada de paquetes y la estimación de jitter. Esto le ayuda a identificar si los fallos de audio se deben a un búfer de reproducción sin datos suficientes, a una entrega irregular de paquetes, o a ambos.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión de radio activa, pero los indicadores de audio solo son significativos mientras la radio está transmitiendo audio.
- Reproduzca o espere a que ocurra el problema de audio mientras el diálogo está abierto, para que los contadores acumulen datos.

## Pasos

1. Haga clic en `Settings > Network...`. Se abre el diálogo Network Diagnostics.
2. Localice el grupo **Audio Playback** en la parte inferior derecha del diálogo.
3. Lea **RX Buffer Now** para ver el nivel de llenado actual del búfer de reproducción en bytes y milisegundos. Un valor cercano a cero mientras se reproduce audio indica que el búfer se está quedando sin datos.
4. Lea **RX Buffer Peak** para ver el nivel de llenado más alto registrado desde que se abrió el diálogo.
5. Lea **Underruns (total)** para obtener el recuento acumulado de interrupciones del búfer desde la conexión.
6. Lea **Underruns (last sec)** para verificar si las interrupciones están ocurriendo en este momento o son solo un registro histórico.
7. Lea **Audio Arrival Gap** para conocer el intervalo de llegada actual entre paquetes consecutivos. Valores grandes indican ráfagas de paquetes retrasados, incluso cuando no se pierden paquetes.
8. Lea **Max Arrival Gap** para ver el peor intervalo de llegada registrado desde que se abrió el diálogo.
9. Lea **Jitter Estimate** para obtener el jitter suavizado de la señal de audio.
10. Si las interrupciones aumentan pero el búfer está cerca de cero, la señal de audio está sin datos suficientes — revise la fila **Audio** en **Incoming Stream Rates** y **Packet Loss (Sequence Gaps)** para detectar baja tasa de transferencia o pérdida de paquetes en ese flujo.
11. Si el búfer tiene un nivel de llenado adecuado pero las interrupciones siguen ocurriendo, el jitter elevado o los intervalos de llegada grandes son la causa probable — compare **Jitter Estimate** y **Max Arrival Gap** con **Latency (RTT)** en el grupo **Network Status**.
12. Haga clic en Close cuando haya terminado.

## Función de cada control

| Indicador | Significado |
|---|---|
| **RX Buffer Now** | Nivel de llenado actual del búfer de reproducción de audio, mostrado en bytes y milisegundos. |
| **RX Buffer Peak** | Nivel de llenado más alto registrado desde que se abrió el diálogo. |
| **Underruns (total)** | Recuento acumulado de interrupciones del búfer de audio desde que la radio se conectó. |
| **Underruns (last sec)** | Número de interrupciones ocurridas en la ventana de un segundo más reciente. |
| **Audio Arrival Gap** | Tiempo actual entre llegadas consecutivas de paquetes de audio entrantes. |
| **Max Arrival Gap** | Mayor intervalo de llegada observado desde que se abrió el diálogo. |
| **Jitter Estimate** | Valor de jitter suavizado para la señal de audio. |

Todos los tamaños del búfer de audio se muestran en bytes con una conversión a milisegundos basada en la frecuencia de muestreo activa. Los valores inferiores a 1 ms se muestran como `< 1 ms`.

## Consejos

- El diálogo se actualiza cada segundo. Déjelo abierto al menos 30–60 segundos durante un problema para capturar valores de pico significativos.
- Cero pérdida de paquetes en el grupo **Packet Loss (Sequence Gaps)** no descarta el jitter ni las ráfagas tardías como causa de las interrupciones. Consulte siempre **Audio Arrival Gap** y **Jitter Estimate** junto con los contadores de pérdida.
- Grandes variaciones en la tasa **Audio** mostrada en **Incoming Stream Rates** pueden indicar una entrega en ráfagas, incluso cuando no se detectan saltos en los números de secuencia.

## Solución de problemas

- **Underruns (last sec) es distinto de cero pero Audio drops muestra cero** — Los paquetes llegan en orden pero con un tiempo irregular. Revise **Jitter Estimate** y **Max Arrival Gap**. La causa probable es bufferbloat en la red o tráfico en competencia en el segmento de red local.
- **RX Buffer Now se mantiene cerca de cero** — La tasa de la señal de audio es demasiado baja para mantener el búfer lleno. Revise la fila **Audio** en **Incoming Stream Rates** para detectar un valor de kbps inesperadamente bajo, y revise las pérdidas de **Audio** para detectar saltos de secuencia que indiquen pérdida de paquetes.
- **Max Arrival Gap es grande pero el Audio Arrival Gap actual parece normal** — Ocurrió una ráfaga transitoria antes en la sesión. El valor de pico no se restablece mientras el diálogo está abierto; reconéctese a la radio para borrar los picos históricos.

## Relacionados

- [Descripción general de Network Diagnostics](../../features/network-diagnostics/overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar las tasas de datos por categoría (audio, FFT, waterfall, metros, DAX)](../../features/network-diagnostics/check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
