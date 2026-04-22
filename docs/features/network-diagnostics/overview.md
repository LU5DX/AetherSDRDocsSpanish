# Descripción general del Diagnóstico de red

El diálogo Network Diagnostics le ofrece una vista en tiempo real y de solo lectura del enlace entre AetherSDR y su FLEX-8600. Úselo para confirmar la IP del radio y la ruta de conexión, medir la latencia, verificar las tasas de datos por flujo y diagnosticar problemas de audio como subdesbordamientos de búfer (underruns) y jitter.

## Antes de comenzar

- No se requiere conexión con el radio para abrir el diálogo, pero la mayoría de los indicadores estarán vacíos o mostrarán "Not connected" hasta que se conecte a un radio.

## Cómo funciona

Abra el diálogo con `Settings > Network...`. Todos los indicadores se actualizan una vez por segundo. Haga clic en Close cuando haya terminado.

El diálogo está dividido en cuatro secciones.

### Network Status

Confirma la ruta de conexión y la latencia TCP.

| Indicador | Qué muestra |
|---|---|
| Status | Estado general del enlace. |
| Target Radio IP | Dirección IP del radio conectado, o "Not connected". |
| Selected Source | NIC local o ruta de enlace usada para la conexión. |
| Local TCP | Extremo TCP local. |
| Local UDP | Extremo UDP local. |
| First UDP Packet | "Yes" o "No" — indica si se recibió un paquete UDP desde la conexión. |
| Latency (RTT) | Tiempo de ida y vuelta actual en ms. Los valores inferiores a 1 ms se muestran como "< 1 ms". |
| Max Latency (RTT) | RTT más alto registrado desde la conexión. |

### Incoming Stream Rates

Muestra la tasa de bits de recepción y transmisión actual para cada tipo de flujo. Variaciones grandes pueden indicar entrega intermitente incluso cuando no se pierden paquetes.

| Indicador | Qué muestra |
|---|---|
| Audio | Tasa de entrada del flujo de audio, en kbps. |
| FFT | Tasa de entrada del flujo FFT, en kbps. |
| Waterfall | Tasa de entrada del flujo de cascada (waterfall), en kbps. |
| Meters | Tasa de entrada del flujo de medidores, en kbps. |
| DAX | Tasa de entrada del flujo DAX, en kbps. |
| Total RX | Bytes entrantes agregados por segundo. |
| Total TX | Bytes salientes agregados por segundo. |

### Packet Loss (Sequence Gaps)

Reporta la pérdida de paquetes inferida a partir de números de secuencia VITA faltantes. Un conteo de cero aquí no descarta jitter ni ráfagas de paquetes tardíos.

| Indicador | Qué muestra |
|---|---|
| Audio | Paquetes descartados / total de paquetes (porcentaje) del flujo de audio. |
| FFT | Paquetes descartados / total de paquetes (porcentaje) del flujo FFT. |
| Waterfall | Paquetes descartados / total de paquetes (porcentaje) del flujo de cascada. |
| Meters | Paquetes descartados / total de paquetes (porcentaje) del flujo de medidores. |
| DAX | Paquetes descartados / total de paquetes (porcentaje) del flujo DAX. |

### Audio Playback

Refleja el estado del búfer en el lado del altavoz. Si los underruns aumentan mientras el búfer se mantiene cerca de cero, la reproducción está sin datos suficientes. El intervalo de llegada y el jitter miden irregularidades de temporización, no pérdida de paquetes.

| Indicador | Qué muestra |
|---|---|
| RX Buffer Now | Llenado actual del búfer de audio, en bytes y ms. |
| RX Buffer Peak | Llenado máximo del búfer de audio registrado desde la conexión, en bytes y ms. |
| Underruns (total) | Conteo acumulado de subdesbordamientos del búfer de audio. |
| Underruns (last sec) | Subdesbordamientos ocurridos en el intervalo de un segundo más reciente. |
| Audio Arrival Gap | Tiempo de llegada entre paquetes, en ms. |
| Max Arrival Gap | Mayor intervalo de llegada entre paquetes registrado, en ms. |
| Jitter Estimate | Jitter suavizado del flujo de audio, en ms. |

## Consejos

- El diálogo puede permanecer abierto mientras opera. Mantenerlo visible durante un problema de audio le permite observar las cuatro secciones simultáneamente.
- Cero pérdidas en la sección Packet Loss no significa que el enlace esté libre de problemas. Revise Jitter Estimate y Max Arrival Gap para detectar irregularidades de temporización que pueden causar artefactos de audio sin descartar paquetes.

## Relacionados

- [Verificar la IP del radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
- [Medir el RTT y la pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar las tasas de datos por categoría (audio, FFT, cascada, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Observar la marca de tiempo del primer paquete UDP tras la conexión](../../getting-started/setup/watch-the-first-udp-packet-timestamp-after-connect.md)
