# Descripción general de Diagnósticos de red

El diálogo Network Diagnostics le ofrece una vista en tiempo real, actualizada de forma continua, del enlace entre AetherSDR y su FLEX-8600. Úselo para confirmar detalles de conectividad, medir la latencia, observar las tasas de datos por flujo e identificar la causa de problemas de audio como underruns y jitter.

## Antes de comenzar

- No se requiere conexión a la radio para abrir el diálogo, pero la mayoría de los indicadores estarán vacíos o mostrarán "Not connected" a menos que AetherSDR esté conectado a una radio.

## Cómo funciona

Abra el diálogo mediante `Settings > Network...`. Todos los indicadores se actualizan automáticamente una vez por segundo. Haga clic en Close cuando termine.

El diálogo está dividido en cuatro grupos:

**Network Status** — ruta de conexión y latencia TCP.

**Incoming Stream Rates** — tasas de bits actuales por tipo de flujo, más totales acumulados.

**Packet Loss (Sequence Gaps)** — conteos de paquetes perdidos inferidos a partir de números de secuencia VITA-49 faltantes.

**Audio Playback** — estado del búfer del lado del altavoz, contadores de underruns y métricas de temporización.

## Qué hace cada control

### Network Status

| Indicador | Qué muestra |
|---|---|
| Status | Estado general del enlace reportado por el modelo de radio. |
| Target Radio IP | Dirección IP de la radio conectada. Muestra "Not connected" cuando no hay ninguna radio vinculada. |
| Selected Source | Interfaz de red local o ruta de enlace usada para la conexión. |
| Local TCP | Extremo TCP local (dirección y puerto). |
| Local UDP | Extremo UDP local (dirección y puerto). |
| First UDP Packet | Indica si el primer paquete UDP se ha recibido desde la conexión ("Yes" o "No"). |
| Latency (RTT) | Tiempo de ida y vuelta actual en milisegundos. Muestra "< 1 ms" cuando está por debajo de 1 ms. |
| Max Latency (RTT) | RTT más alto registrado desde que se estableció la conexión actual. |

### Incoming Stream Rates

| Indicador | Qué muestra |
|---|---|
| Audio | Tasa de bits de entrada del flujo de audio, en kbps. |
| FFT | Tasa de bits de entrada del flujo FFT, en kbps. |
| Waterfall | Tasa de bits de entrada del flujo de cascada (waterfall), en kbps. |
| Meters | Tasa de bits de entrada del flujo de medidores, en kbps. |
| DAX | Tasa de bits de entrada del flujo DAX, en kbps. |
| Total RX | Bytes de entrada acumulados por segundo en todos los flujos, en kbps. |
| Total TX | Bytes de salida acumulados por segundo, en kbps. |

Grandes variaciones en las tasas de flujos individuales pueden indicar entrega irregular incluso cuando no se pierde ningún paquete.

### Packet Loss (Sequence Gaps)

| Indicador | Qué muestra |
|---|---|
| Audio | Paquetes perdidos frente al total del flujo de audio, con porcentaje. |
| FFT | Paquetes perdidos frente al total del flujo FFT, con porcentaje. |
| Waterfall | Paquetes perdidos frente al total del flujo de cascada, con porcentaje. |
| Meters | Paquetes perdidos frente al total del flujo de medidores, con porcentaje. |
| DAX | Paquetes perdidos frente al total del flujo DAX, con porcentaje. |

Una pérdida de cero aquí no descarta jitter ni ráfagas de paquetes tardíos.

### Audio Playback

| Indicador | Qué muestra |
|---|---|
| RX Buffer Now | Nivel de llenado actual del búfer de recepción de audio, en bytes y milisegundos. |
| RX Buffer Peak | Nivel de llenado más alto del búfer registrado desde la conexión, en bytes y milisegundos. |
| Underruns (total) | Conteo acumulado de underruns del búfer de audio desde la conexión. |
| Underruns (last sec) | Underruns ocurridos en el intervalo de un segundo más reciente. |
| Audio Arrival Gap | Tiempo entre paquetes de audio entrantes consecutivos. |
| Max Arrival Gap | Mayor intervalo de llegada entre paquetes registrado desde la conexión. |
| Network Jitter | Estimación de jitter suavizada para el flujo de audio. |

Si los underruns aumentan mientras RX Buffer Now permanece cerca de cero, la ruta de audio está sin datos suficientes. Audio Arrival Gap y Network Jitter miden la temporización, no la pérdida de paquetes.

### Botón

| Control | Comportamiento |
|---|---|
| Close | Cierra el diálogo. |

## Consejos

- El diálogo no requiere una radio conectada para abrirse. Puede abrirlo antes de conectarse para confirmar que no hay valores obsoletos presentes.
- Todos los indicadores restablecen sus valores pico y acumulados cuando se establece una nueva conexión.
- Una pérdida de paquetes de cero en el grupo Packet Loss no garantiza un audio limpio. Compruebe también Network Jitter y Underruns (last sec).

## Relacionados

- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Comprobar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar underruns de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Observar la marca de tiempo del primer paquete UDP tras la conexión](../../getting-started/setup/watch-the-first-udp-packet-timestamp-after-connect.md)
