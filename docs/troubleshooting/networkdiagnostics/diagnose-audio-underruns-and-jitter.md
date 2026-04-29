# Diagnóstico de interrupciones de audio y jitter

Use el diálogo Network Diagnostics para leer en tiempo real el estado del búfer de audio, el conteo de interrupciones, el tiempo entre llegadas de paquetes y las estimaciones de jitter. Esto le ayuda a identificar si las caídas de audio se deben a un búfer sin datos, a una entrega irregular de paquetes o a jitter de red.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión de radio activa, pero los indicadores de audio solo son significativos mientras una radio está conectada y transmitiendo audio.
- Reproduzca el problema de audio antes de abrir el diálogo para que los contadores y los valores máximos reflejen la condición de falla.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. Localice el grupo **Audio Playback** en la zona inferior derecha del diálogo.
3. Lea **RX Buffer Now** para ver cuántos bytes (y milisegundos) de audio se encuentran actualmente en el búfer de reproducción.
4. Lea **RX Buffer Peak** para ver el mayor llenado de búfer registrado desde que se abrió el diálogo.
5. Lea **Underruns (total)** para ver el conteo acumulado de interrupciones del búfer desde que se inició el motor de audio.
6. Lea **Underruns (last sec)** para ver cuántas interrupciones ocurrieron en la ventana de un segundo más reciente. Un valor distinto de cero mientras el audio se está transmitiendo activamente indica un problema en curso.
7. Lea **Audio Arrival Gap** para ver el intervalo actual de llegada entre paquetes consecutivos. Un valor significativamente mayor que el período de paquete esperado indica una entrega irregular.
8. Lea **Max Arrival Gap** para ver el peor intervalo de llegada registrado desde que se abrió el diálogo.
9. Lea **Network Jitter** para ver la estimación de jitter suavizada del flujo de audio.
10. Si las interrupciones aumentan pero **RX Buffer Now** permanece cerca de cero, el búfer se está quedando sin datos — consulte los consejos a continuación.
11. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Indicador | Significado |
|---|---|
| **RX Buffer Now** | Llenado actual del búfer de audio, mostrado en bytes y milisegundos. |
| **RX Buffer Peak** | Mayor llenado del búfer observado desde que se abrió el diálogo. |
| **Underruns (total)** | Conteo acumulado de interrupciones del búfer de audio desde que se inició el motor de audio. |
| **Underruns (last sec)** | Número de interrupciones ocurridas en el último intervalo de un segundo. |
| **Audio Arrival Gap** | Tiempo entre llegadas consecutivas de paquetes de audio entrantes. |
| **Max Arrival Gap** | Mayor intervalo de llegada registrado desde que se abrió el diálogo. |
| **Network Jitter** | Estimación suavizada del jitter del flujo de audio. |

Todos los indicadores se actualizan una vez por segundo.

## Consejos

- **Interrupciones en aumento, búfer cerca de cero:** El flujo de audio no está llegando con suficiente rapidez para mantener el búfer lleno. Revise la tasa **Audio** en el grupo **Incoming Stream Rates** y compárela con la tasa de bits esperada. Una tasa de Audio muy baja o en cero significa que los paquetes no están llegando en absoluto.
- **Sin pérdida de paquetes pero aún con interrupciones:** El grupo **Packet Loss (Sequence Gaps)** solo cuenta los números de secuencia VITA faltantes. Los paquetes que llegan tarde, en lugar de perderse, no incrementan el contador de descarte pero igualmente causan jitter e interrupciones. Use **Audio Arrival Gap** y **Network Jitter** para detectar esta condición.
- **Max Arrival Gap alto con intervalo promedio bajo:** Esto indica ráfagas ocasionales de paquetes retrasados en lugar de pérdida sostenida. Aísle la ruta de red hacia la radio y compruebe si hay tráfico competidor.
- **RX Buffer Peak es muy bajo:** El búfer nunca acumuló una reserva útil. Esto hace que el flujo sea sensible a cualquier variación en la entrega. Verifique la ruta de red y considere si otro tráfico intenso está compitiendo en el mismo enlace.

## Solución de problemas

- **Todos los indicadores de audio muestran cero o sin datos** — La radio no está transmitiendo audio. Confirme que la radio está conectada y que hay un slice receptor activo.
- **Underruns (last sec) es distinto de cero pero Underruns (total) es pequeño** — El problema es intermitente. Deje el diálogo abierto y espere un período de observación más prolongado. Observe **Max Arrival Gap** para detectar evidencia de ráfagas periódicas.
- **Network Jitter es alto pero las caídas de audio muestran cero** — Los paquetes están llegando tarde en lugar de perderse. El jitter reduce directamente el margen efectivo del búfer. Compruebe si hay otro tráfico UDP compitiendo en la misma interfaz.

## Relacionado

- [Descripción general de Network Diagnostics](../../features/network-diagnostics/overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar tasas de datos por categoría (audio, FFT, waterfall, metros, DAX)](../../features/network-diagnostics/check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
