# Medir RTT y pérdida de paquetes durante problemas de audio

Use el diálogo Network Diagnostics para leer el tiempo de ida y vuelta actual y los conteos de pérdida de paquetes por categoría mientras reproduce un problema de audio. Esto permite distinguir un problema en la ruta de red de un problema de configuración de audio local.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión de radio activa, pero la mayoría de los indicadores estarán vacíos hasta que la radio esté conectada.
- Reproduzca el problema de audio, o esté listo para reproducirlo, de modo que pueda observar los valores en tiempo real.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. Observe **Latency (RTT)** en el grupo Network Status. Muestra el tiempo de ida y vuelta actual hacia la radio en milisegundos. Los valores por debajo de 1 ms se muestran como `< 1 ms`.
3. Observe **Max Latency (RTT)**. Muestra el RTT más alto registrado desde que la radio se conectó. Una brecha amplia entre **Latency (RTT)** y **Max Latency (RTT)** indica picos periódicos en la ruta de red.
4. Observe la fila **Audio** en el grupo Packet Loss (Sequence Gaps). El valor muestra los paquetes descartados frente al total de paquetes y un porcentaje. Cualquier porcentaje distinto de cero durante problemas de audio apunta a pérdida de paquetes en la ruta UDP.
5. Revise las filas de pérdida **FFT**, **Waterfall**, **Meters** y **DAX** en el mismo grupo para determinar si la pérdida es específica del flujo de audio o afecta a todas las categorías.
6. Haga clic en Close cuando termine.

## Qué hace cada control

| Indicador | Grupo | Significado |
|---|---|---|
| **Status** | Network Status | Estado general del enlace. |
| **Target Radio IP** | Network Status | Dirección IP de la radio conectada. Muestra `Not connected` cuando no hay ninguna radio conectada. |
| **Selected Source** | Network Status | Interfaz de red local o ruta de enlace utilizada para la conexión. |
| **Local TCP** | Network Status | Extremo TCP local en uso. |
| **Local UDP** | Network Status | Extremo UDP local en uso. |
| **First UDP Packet** | Network Status | Indica si se ha recibido el primer paquete UDP (`Yes` o `No`). |
| **Latency (RTT)** | Network Status | Tiempo de ida y vuelta actual, actualizado cada segundo. |
| **Max Latency (RTT)** | Network Status | RTT más alto registrado desde la conexión. |
| **Audio** (tasa) | Incoming Stream Rates | Tasa de ingreso del flujo de audio en kbps. |
| **FFT** (tasa) | Incoming Stream Rates | Tasa de ingreso del flujo FFT en kbps. |
| **Waterfall** (tasa) | Incoming Stream Rates | Tasa de ingreso del flujo waterfall en kbps. |
| **Meters** (tasa) | Incoming Stream Rates | Tasa de ingreso del flujo Meters en kbps. |
| **DAX** (tasa) | Incoming Stream Rates | Tasa de ingreso del flujo DAX en kbps. |
| **Total RX** | Incoming Stream Rates | Total de bytes entrantes por segundo en todas las categorías. |
| **Total TX** | Incoming Stream Rates | Total de bytes salientes por segundo. |
| **Audio** (pérdidas) | Packet Loss (Sequence Gaps) | Paquetes de audio descartados / total de paquetes (porcentaje). Se infiere a partir de saltos en el número de secuencia VITA. |
| **FFT** (pérdidas) | Packet Loss (Sequence Gaps) | Paquetes FFT descartados / total de paquetes (porcentaje). |
| **Waterfall** (pérdidas) | Packet Loss (Sequence Gaps) | Paquetes waterfall descartados / total de paquetes (porcentaje). |
| **Meters** (pérdidas) | Packet Loss (Sequence Gaps) | Paquetes Meters descartados / total de paquetes (porcentaje). |
| **DAX** (pérdidas) | Packet Loss (Sequence Gaps) | Paquetes DAX descartados / total de paquetes (porcentaje). |
| **RX Buffer Now** | Audio Playback | Nivel actual del búfer de audio en bytes y milisegundos. |
| **RX Buffer Peak** | Audio Playback | Nivel máximo del búfer de audio desde la conexión. |
| **Underruns (total)** | Audio Playback | Contador acumulado de subdesbordamientos del búfer de audio. |
| **Underruns (last sec)** | Audio Playback | Subdesbordamientos registrados en el intervalo de un segundo más reciente. |
| **Audio Arrival Gap** | Audio Playback | Temporización de llegada entre paquetes en el momento actual. |
| **Max Arrival Gap** | Audio Playback | Mayor intervalo de llegada entre paquetes registrado desde la conexión. |
| **Network Jitter** | Audio Playback | Estimación de jitter suavizada para el flujo de audio. |

Todos los valores se actualizan una vez por segundo.

## Sugerencias

- Un valor de cero en el grupo Packet Loss no descarta el problema. Variaciones grandes en las filas de tasa del grupo Incoming Stream Rates pueden indicar entrega en ráfagas sin saltos en el número de secuencia. Revise **Audio Arrival Gap** y **Network Jitter** en el grupo Audio Playback para detectar problemas de temporización que no se manifiestan como pérdidas.
- Si **Underruns (total)** sigue aumentando mientras **RX Buffer Now** está cerca de cero, el lado de reproducción de audio está siendo privado de datos. Esto apunta a un problema de configuración de audio local más que a pérdida de paquetes en la red. Consulte [Diagnosticar subdesbordamientos y jitter de audio](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md).
- Si aparecen pérdidas en todas las categorías (Audio, FFT, Waterfall, Meters), el problema probablemente se encuentra en la ruta de red y no en el procesamiento de audio del lado de la radio.

## Solución de problemas

- **Todos los indicadores muestran valores vacíos o cero inmediatamente después de abrir el diálogo** — La radio no está conectada. Conéctese a la radio primero y luego vuelva a abrir el diálogo mediante `Settings > Network...`.
- **Latency (RTT) muestra `< 1 ms` pero el audio sigue siendo deficiente** — El RTT refleja la temporización del ping TCP. La temporización de los paquetes de audio UDP es independiente. Revise **Audio Arrival Gap**, **Max Arrival Gap** y **Network Jitter** para detectar problemas de entrega UDP.

## Relacionados

- [Verificar las tasas de datos por categoría (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar subdesbordamientos y jitter de audio](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
- [Descripción general de Network Diagnostics](overview.md)
