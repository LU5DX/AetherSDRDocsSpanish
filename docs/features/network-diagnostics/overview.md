# Descripción general de Diagnósticos de red

El diálogo Network Diagnostics le ofrece una vista en tiempo real, por segundo, del enlace de red entre AetherSDR y su FLEX-8600. Úselo para confirmar los extremos de la conexión, medir la latencia, inspeccionar las tasas de datos por flujo y diagnosticar problemas en el búfer de audio.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo puede abrirse con o sin una radio conectada, pero la mayoría de los indicadores estarán vacíos hasta que se establezca una conexión.

## Cómo funciona

Abra el diálogo con `Settings > Network...`. Todos los indicadores se actualizan automáticamente una vez por segundo. Haga clic en Close cuando termine.

El diálogo está dividido en cuatro grupos:

### Network Status

Ruta de conexión y latencia TCP. Confirma qué ruta está utilizando AetherSDR para alcanzar la radio.

| Indicador | Lo que muestra |
|---|---|
| Status | Estado general del enlace. |
| Target Radio IP | Dirección IP de la radio conectada. Muestra "Not connected" cuando no hay ninguna radio vinculada. |
| Selected Source | Interfaz de red local o ruta de enlace utilizada para la conexión. |
| Local TCP | Extremo TCP local (dirección y puerto). |
| Local UDP | Extremo UDP local (dirección y puerto). |
| First UDP Packet | Si el primer paquete UDP ha sido recibido desde la conexión ("Yes" o "No"). |
| Latency (RTT) | Tiempo de ida y vuelta actual en milisegundos. Muestra "< 1 ms" cuando es inferior a 1 ms. |
| Max Latency (RTT) | RTT más alto medido desde que se conectó la radio. |

### Incoming Stream Rates

Tasas de entrada por categoría y totales agregados. Grandes variaciones indican entrega irregular incluso cuando no se pierden paquetes.

| Indicador | Lo que muestra |
|---|---|
| Audio | Tasa del flujo de audio entrante en kbps. |
| FFT | Tasa del flujo FFT entrante en kbps. |
| Waterfall | Tasa del flujo de cascada (waterfall) entrante en kbps. |
| Meters | Tasa del flujo de medidores entrante en kbps. |
| DAX | Tasa del flujo DAX entrante en kbps. |
| Total RX | Tasa de entrada agregada de todos los flujos en kbps. |
| Total TX | Tasa de salida agregada en kbps. |

### Packet Loss (Sequence Gaps)

Conteos de pérdida inferidos a partir de números de secuencia VITA-49 faltantes. Un conteo en cero aquí no descarta problemas de jitter o ráfagas de entrega tardía.

| Indicador | Lo que muestra |
|---|---|
| Audio | Paquetes descartados / total de paquetes (porcentaje) para el flujo de audio. |
| FFT | Paquetes descartados / total de paquetes (porcentaje) para el flujo FFT. |
| Waterfall | Paquetes descartados / total de paquetes (porcentaje) para el flujo de cascada. |
| Meters | Paquetes descartados / total de paquetes (porcentaje) para el flujo de medidores. |
| DAX | Paquetes descartados / total de paquetes (porcentaje) para el flujo DAX. |

### Audio Playback

Estado del búfer en el lado del altavoz. Si los subdesbordamientos (underruns) aumentan mientras el búfer permanece cerca de cero, la reproducción está sin datos suficientes. El intervalo de llegada y el jitter miden la temporización, no la pérdida de paquetes.

| Indicador | Lo que muestra |
|---|---|
| RX Buffer Now | Llenado actual del búfer de recepción de audio, en bytes y milisegundos. |
| RX Buffer Peak | Llenado máximo del búfer observado desde la conexión, en bytes y milisegundos. |
| Underruns (total) | Conteo acumulado de subdesbordamientos del búfer de audio desde la conexión. |
| Underruns (last sec) | Subdesbordamientos del búfer de audio ocurridos en el intervalo de un segundo más reciente. |
| Audio Arrival Gap | Intervalo de tiempo entre paquetes de audio entrantes consecutivos. |
| Max Arrival Gap | Mayor intervalo de llegada observado desde la conexión. |
| Network Jitter | Estimación de jitter suavizada del flujo de audio entrante. |

## Controles

| Control | Comportamiento |
|---|---|
| Close | Cierra el diálogo. |

## Consejos

- El diálogo puede permanecer abierto mientras opera. Todos los valores se actualizan cada segundo sin necesidad de ninguna interacción.
- Los conteos de pérdida de paquetes en el grupo Packet Loss son acumulativos desde que se abrió el diálogo; cierre y vuelva a abrir el diálogo para restablecer la línea de base.
- La pérdida de paquetes en cero combinada con subdesbordamientos crecientes apunta a un problema de jitter o temporización en lugar de pérdida real — en ese caso, revise Audio Arrival Gap y Network Jitter.

## Relacionado

- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
- [Medir el RTT y la pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar las tasas de datos por categoría (audio, FFT, cascada, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Observar la marca de tiempo del primer paquete UDP tras la conexión](../../getting-started/setup/watch-the-first-udp-packet-timestamp-after-connect.md)
