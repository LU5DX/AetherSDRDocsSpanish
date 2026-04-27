# Diagnosticar subdesbordamientos de audio y jitter

Use el diálogo Network Diagnostics para leer en tiempo real el estado del búfer de audio, el conteo de subdesbordamientos, los intervalos de llegada de paquetes y las estimaciones de jitter. Esto le ayuda a identificar si los cortes de audio se deben a un búfer sin datos suficientes, a una entrega irregular de paquetes o a jitter de red.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión activa con el radio, pero los indicadores de audio solo son significativos mientras el radio está conectado y transmitiendo audio.
- Reproduzca el problema de audio antes de abrir el diálogo para que los contadores y los valores máximos reflejen la condición de falla.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. Ubique el grupo **Audio Playback** en la parte inferior derecha del diálogo.
3. Lea **RX Buffer Now** para ver cuántos bytes (y milisegundos) de audio se almacenan actualmente en el búfer de reproducción.
4. Lea **RX Buffer Peak** para ver el nivel máximo de llenado del búfer registrado desde que se abrió el diálogo.
5. Lea **Underruns (total)** para ver el conteo acumulado de subdesbordamientos del búfer desde que se inició el motor de audio.
6. Lea **Underruns (last sec)** para ver cuántos subdesbordamientos ocurrieron en la ventana de un segundo más reciente. Un valor distinto de cero mientras el audio se transmite activamente indica un problema en curso.
7. Lea **Audio Arrival Gap** para ver el intervalo actual de llegada entre paquetes consecutivos. Un valor significativamente mayor que el período de paquete esperado indica una entrega irregular.
8. Lea **Max Arrival Gap** para ver el peor intervalo de llegada registrado desde que se abrió el diálogo.
9. Lea **Network Jitter** para ver la estimación de jitter suavizada para el flujo de audio.
10. Si los subdesbordamientos aumentan pero **RX Buffer Now** permanece cerca de cero, el búfer está sin datos suficientes — consulte los consejos a continuación.
11. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Indicador | Significado |
|---|---|
| **RX Buffer Now** | Nivel actual de llenado del búfer de audio, mostrado en bytes y milisegundos. |
| **RX Buffer Peak** | Mayor nivel de llenado del búfer visto desde que se abrió el diálogo. |
| **Underruns (total)** | Conteo acumulado de subdesbordamientos del búfer de audio desde que se inició el motor de audio. |
| **Underruns (last sec)** | Número de subdesbordamientos ocurridos en el último intervalo de un segundo. |
| **Audio Arrival Gap** | Tiempo entre llegadas consecutivas de paquetes de audio entrantes. |
| **Max Arrival Gap** | Mayor intervalo de llegada registrado desde que se abrió el diálogo. |
| **Network Jitter** | Estimación suavizada del jitter del flujo de audio. |

Todos los indicadores se actualizan una vez por segundo.

## Consejos

- **Subdesbordamientos en aumento, búfer cerca de cero:** El flujo de audio no llega con suficiente rapidez para mantener el búfer lleno. Verifique la tasa **Audio** en el grupo **Incoming Stream Rates** y compárela con la tasa de bits esperada. Una tasa de Audio muy baja o cero significa que los paquetes no están llegando en absoluto.
- **Sin pérdida de paquetes pero con subdesbordamientos:** El grupo **Packet Loss (Sequence Gaps)** contabiliza únicamente los números de secuencia VITA faltantes. Los paquetes que llegan tarde en lugar de perderse no incrementan el contador de descartes, pero igualmente causan jitter y subdesbordamientos. Use **Audio Arrival Gap** y **Network Jitter** para detectar esta condición.
- **Max Arrival Gap grande con intervalo promedio bajo:** Esto indica ráfagas ocasionales de paquetes retrasados en lugar de pérdida sostenida. Aísle la ruta de red hacia el radio y verifique si existe tráfico competidor.
- **RX Buffer Peak es muy bajo:** El búfer nunca acumuló una reserva útil. Esto hace que el flujo sea sensible a cualquier variación en la entrega. Verifique la ruta de red y considere si otro tráfico intenso compite en el mismo enlace.

## Resolución de problemas

- **Todos los indicadores de audio muestran cero o sin datos** — El radio no está transmitiendo audio. Confirme que el radio está conectado y que hay un slice receptor activo.
- **Underruns (last sec) es distinto de cero pero Underruns (total) es pequeño** — El problema es intermitente. Deje el diálogo abierto y espere un período de observación más prolongado. Observe **Max Arrival Gap** para detectar evidencia de ráfagas periódicas.
- **Network Jitter es alto pero los cortes de audio muestran cero** — Los paquetes están llegando tarde en lugar de perderse. El jitter reduce directamente el margen efectivo del búfer. Verifique si hay otro tráfico UDP compitiendo en la misma interfaz.

## Relacionado

- [Descripción general de Network Diagnostics](../../features/network-diagnostics/overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](../../features/network-diagnostics/check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
