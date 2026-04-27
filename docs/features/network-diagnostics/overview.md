# Descripción general del Diagnóstico de Red

El diálogo Network Diagnostics le ofrece una vista en tiempo real, actualizada cada segundo, del enlace de red entre AetherSDR y su FLEX-8600. Úselo para confirmar los extremos de la conexión, medir la latencia, inspeccionar las tasas de datos por flujo y diagnosticar problemas en el búfer de audio.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo puede abrirse con o sin una radio conectada, pero la mayoría de los indicadores estarán vacíos hasta que se establezca una conexión.

## Cómo funciona

Abra el diálogo con `Settings > Network...`. Todos los indicadores se actualizan automáticamente una vez por segundo. Haga clic en Close cuando termine.

El diálogo está dividido en cuatro grupos:

### Network Status

Ruta de conexión y latencia TCP. Confirma qué ruta utiliza AetherSDR para alcanzar la radio.

| Indicador | Qué muestra |
|---|---|
| Status | Estado general del enlace. |
| Target Radio IP | Dirección IP de la radio conectada. Muestra "Not connected" cuando no hay ninguna radio vinculada. |
| Selected Source | Interfaz de red local o ruta de enlace usada para la conexión. |
| Local TCP | Extremo TCP local (dirección y puerto). |
| Local UDP | Extremo UDP local (dirección y puerto). |
| First UDP Packet | Indica si el primer paquete UDP fue recibido desde la conexión ("Yes" o "No"). |
| Latency (RTT) | Tiempo de ida y vuelta actual en milisegundos. Muestra "< 1 ms" cuando es inferior a 1 ms. |
| Max Latency (RTT) | Mayor RTT medido desde que la radio se conectó. |

### Incoming Stream Rates

Tasas de entrada por categoría y totales agregados. Variaciones grandes indican entrega irregular incluso cuando no se pierden paquetes.

| Indicador | Qué muestra |
|---|---|
| Audio | Tasa del flujo de audio entrante en kbps. |
| FFT | Tasa del flujo FFT entrante en kbps. |
| Waterfall | Tasa del flujo de cascada (waterfall) entrante en kbps. |
| Meters | Tasa del flujo de medidores entrante en kbps. |
| DAX | Tasa del flujo DAX entrante en kbps. |
| Total RX | Tasa de entrada agregada en todos los flujos en kbps. |
| Total TX | Tasa de salida agregada en kbps. |

### Packet Loss (Sequence Gaps)

Conteo de paquetes perdidos inferido a partir de números de secuencia VITA faltantes. Un conteo en cero aquí no descarta jitter ni ráfagas de entrega tardía.

| Indicador | Qué muestra |
|---|---|
| Audio | Paquetes perdidos / paquetes totales (porcentaje) del flujo de audio. |
| FFT | Paquetes perdidos / paquetes totales (porcentaje) del flujo FFT. |
| Waterfall | Paquetes perdidos / paquetes totales (porcentaje) del flujo de cascada. |
| Meters | Paquetes perdidos / paquetes totales (porcentaje) del flujo de medidores. |
| DAX | Paquetes perdidos / paquetes totales (porcentaje) del flujo DAX. |

### Audio Playback

Estado del búfer en el lado del altavoz. Si los subdesbordamientos (underruns) aumentan mientras el búfer permanece cerca de cero, la reproducción está sufriendo inanición de datos. El intervalo de llegada y el jitter miden la temporización, no la pérdida de paquetes.

| Indicador | Qué muestra |
|---|---|
| RX Buffer Now | Nivel actual de llenado del búfer de recepción de audio, en bytes y milisegundos. |
| RX Buffer Peak | Mayor nivel de llenado del búfer observado desde la conexión, en bytes y milisegundos. |
| Underruns (total) | Conteo acumulado de subdesbordamientos del búfer de audio desde la conexión. |
| Underruns (last sec) | Subdesbordamientos del búfer de audio ocurridos en el intervalo de un segundo más reciente. |
| Audio Arrival Gap | Intervalo de tiempo entre paquetes de audio entrantes consecutivos. |
| Max Arrival Gap | Mayor intervalo de llegada observado desde la conexión. |
| Network Jitter | Estimación suavizada del jitter del flujo de audio entrante. |

## Controles

| Control | Comportamiento |
|---|---|
| Close | Cierra el diálogo. |

## Consejos

- El diálogo puede permanecer abierto mientras opera. Todos los valores se actualizan cada segundo sin necesidad de ninguna interacción.
- Los conteos de pérdida de paquetes en el grupo Packet Loss son acumulativos desde que se abrió el diálogo; cierre y vuelva a abrirlo para restablecer la línea base.
- Pérdida de paquetes en cero combinada con subdesbordamientos crecientes apunta a un problema de jitter o temporización, y no a pérdida directa de paquetes — en ese caso, revise Audio Arrival Gap y Network Jitter.

## Relacionado

- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
- [Medir el RTT y la pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Revisar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Observar la marca de tiempo del primer paquete UDP tras la conexión](../../getting-started/setup/watch-the-first-udp-packet-timestamp-after-connect.md)
