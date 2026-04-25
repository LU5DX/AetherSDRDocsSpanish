# Descripción general de Diagnósticos de red

El diálogo Network Diagnostics le ofrece una vista en tiempo real del enlace entre AetherSDR y su FLEX-8600. Úselo para inspeccionar los extremos TCP/UDP, el tiempo de ida y vuelta, las tasas de datos por categoría, la pérdida de paquetes y el estado del búfer de audio — todo actualizado una vez por segundo sin necesidad de una conexión de radio activa.

## Cómo funciona

Abra el diálogo desde `Settings > Network...`. Se actualiza automáticamente cada segundo. Todos los indicadores son de solo lectura; no hay nada que configurar aquí. Haga clic en Close cuando haya terminado.

El diálogo está dividido en cuatro grupos:

### Network Status

Confirma qué ruta de red está usando AetherSDR y su capacidad de respuesta.

| Indicador | Qué muestra |
|---|---|
| Status | Estado general del enlace. |
| Target Radio IP | Dirección IP de la radio conectada, o "Not connected". |
| Selected Source | NIC local o ruta de enlace utilizada para la conexión. |
| Local TCP | Extremo TCP local (dirección y puerto). |
| Local UDP | Extremo UDP local (dirección y puerto). |
| First UDP Packet | Si se ha recibido el primer paquete UDP entrante ("Yes" o "No"). |
| Latency (RTT) | Tiempo de ida y vuelta actual en milisegundos, mostrado como "< 1 ms" cuando es inferior a 1 ms. |
| Max Latency (RTT) | RTT más alto registrado desde la última conexión. |

### Incoming Stream Rates

Muestra las tasas de bits de recepción y transmisión actuales, desglosadas por tipo de flujo. Variaciones grandes pueden indicar entrega en ráfagas incluso cuando no se pierden paquetes.

| Indicador | Qué muestra |
|---|---|
| Audio | Tasa de entrada del flujo de audio, en kbps. |
| FFT | Tasa de entrada de datos FFT, en kbps. |
| Waterfall | Tasa de entrada de datos de cascada (waterfall), en kbps. |
| Meters | Tasa de entrada de datos de medidores, en kbps. |
| DAX | Tasa de entrada de audio DAX, en kbps. |
| Total RX | Tasa de entrada agregada de todos los flujos, en kbps. |
| Total TX | Tasa de salida agregada, en kbps. |

### Packet Loss (Sequence Gaps)

Informa la pérdida de paquetes inferida a partir de números de secuencia VITA-49 faltantes. Un valor de cero aquí no descarta la presencia de jitter o ráfagas de paquetes tardíos.

| Indicador | Qué muestra |
|---|---|
| Audio | Paquetes descartados / paquetes totales (porcentaje) del flujo de audio. |
| FFT | Descartados / total para datos FFT. |
| Waterfall | Descartados / total para datos de cascada (waterfall). |
| Meters | Descartados / total para datos de medidores. |
| DAX | Descartados / total para audio DAX. |

### Audio Playback

Informa el estado del búfer en el lado del altavoz. Un número creciente de subdesbordamientos (underruns) combinado con un búfer casi vacío indica que la canalización de reproducción está sin datos. El gap de llegada y el jitter miden la temporización de los paquetes, no la pérdida de paquetes.

| Indicador | Qué muestra |
|---|---|
| RX Buffer Now | Nivel actual de llenado del búfer de audio, en bytes y milisegundos. |
| RX Buffer Peak | Nivel máximo de llenado del búfer registrado desde la conexión, en bytes y milisegundos. |
| Underruns (total) | Recuento acumulado de subdesbordamientos del búfer de audio. |
| Underruns (last sec) | Subdesbordamientos ocurridos en el intervalo de un segundo más reciente. |
| Audio Arrival Gap | Gap medido entre llegadas consecutivas de paquetes de audio entrantes. |
| Max Arrival Gap | Mayor gap de llegada registrado desde la conexión. |
| Network Jitter | Estimación de jitter suavizada para el flujo de audio. |

## Controles

| Control | Comportamiento |
|---|---|
| Close | Cierra el diálogo. |

## Consejos

- El diálogo no requiere una conexión de radio activa para abrirse, pero la mayoría de los indicadores mostrarán valores de marcador de posición hasta que se establezca una conexión.
- Los indicadores de pérdida de paquetes cuentan los saltos en los números de secuencia de los flujos VITA-49. Un recuento de cero no garantiza una entrega limpia — use el grupo Audio Playback para verificar los problemas de temporización de forma independiente.
- "< 1 ms" en los campos RTT significa que el valor medido está por debajo de 1 ms, no que la medición haya fallado.

## Relacionados

- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
- [Medir el RTT y la pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar las tasas de datos por categoría (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Observar la marca de tiempo del primer paquete UDP tras la conexión](../../getting-started/setup/watch-the-first-udp-packet-timestamp-after-connect.md)
