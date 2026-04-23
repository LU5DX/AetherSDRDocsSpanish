# Descripción general de Diagnósticos de red

El diálogo Network Diagnostics ofrece una vista en tiempo real del enlace entre AetherSDR y su radio Flex: puntos finales de conexión, latencia de ida y vuelta, tasas de datos por flujo, conteos de pérdida de paquetes y estado del búfer de audio. Úselo para confirmar que la ruta de red es estable o para aislar la causa de interrupciones de audio y parpadeos en el waterfall.

## Cómo funciona

Abra el diálogo con `Settings > Network...`. No requiere una conexión de radio activa, aunque la mayoría de los indicadores mostrarán valores de marcador de posición hasta que se conecte.

Todos los valores se actualizan automáticamente una vez por segundo. El diálogo es de solo lectura — no se modifica ninguna configuración aquí. Haga clic en Close cuando haya terminado.

El diálogo está organizado en cuatro grupos.

### Estado de red

Ruta de conexión y latencia TCP. Confirma qué ruta utiliza AetherSDR para llegar a la radio.

| Indicador | Qué muestra |
|---|---|
| Status | Estado general del enlace. |
| Target Radio IP | Dirección IP de la radio conectada. Muestra "Not connected" cuando no hay ninguna radio presente. |
| Selected Source | Interfaz de red local o ruta de enlace utilizada para la conexión. |
| Local TCP | Punto final TCP local (dirección y puerto). |
| Local UDP | Punto final UDP local (dirección y puerto). |
| First UDP Packet | Si se ha recibido un paquete UDP desde la conexión (Yes / No). |
| Latency (RTT) | Tiempo de ida y vuelta actual en milisegundos. Muestra "< 1 ms" cuando es inferior a 1 ms. |
| Max Latency (RTT) | Mayor RTT registrado desde la última conexión. |

### Tasas de flujo entrante

Tasas de bits de recepción y transmisión actuales por tipo de flujo, en kbps. Variaciones grandes pueden indicar una entrega irregular incluso cuando no se pierden paquetes.

| Indicador | Qué muestra |
|---|---|
| Audio | Tasa de entrada para el flujo de audio. |
| FFT | Tasa de entrada para el flujo FFT (panadapter). |
| Waterfall | Tasa de entrada para el flujo del waterfall. |
| Meters | Tasa de entrada para el flujo de medidores. |
| DAX | Tasa de entrada para el flujo de audio DAX. |
| Total RX | Bytes de entrada agregados por segundo en todos los flujos. |
| Total TX | Bytes de salida agregados por segundo. |

### Pérdida de paquetes (saltos de secuencia)

Pérdida de paquetes inferida a partir de números de secuencia VITA-49 faltantes. Cada entrada muestra paquetes descartados, total de paquetes y un porcentaje. Una pérdida de cero aquí no descarta la presencia de jitter o ráfagas tardías.

| Indicador | Qué muestra |
|---|---|
| Audio | Conteo de descarte y tasa para el flujo de audio. |
| FFT | Conteo de descarte y tasa para el flujo FFT. |
| Waterfall | Conteo de descarte y tasa para el flujo del waterfall. |
| Meters | Conteo de descarte y tasa para el flujo de medidores. |
| DAX | Conteo de descarte y tasa para el flujo DAX. |

### Reproducción de audio

Estado del búfer en el lado del altavoz. Si los subdesbordamientos aumentan mientras el búfer permanece cerca de cero, la reproducción está en inanición. El intervalo de llegada y el jitter miden el tiempo, no la pérdida de paquetes.

| Indicador | Qué muestra |
|---|---|
| RX Buffer Now | Nivel de llenado actual del búfer de audio, en bytes y milisegundos. |
| RX Buffer Peak | Mayor nivel de llenado del búfer registrado desde la conexión. |
| Underruns (total) | Conteo acumulado de subdesbordamientos de audio. |
| Underruns (last sec) | Subdesbordamientos registrados en la ventana de un segundo más reciente. |
| Audio Arrival Gap | Intervalo de llegada entre paquetes para el paquete de audio más reciente. |
| Max Arrival Gap | Mayor intervalo de llegada entre paquetes observado desde la conexión. |
| Jitter Estimate | Jitter suavizado del flujo de audio entrante. |

## Controles

| Control | Comportamiento |
|---|---|
| Close | Cierra el diálogo. |

## Consejos

- El diálogo puede dejarse abierto mientras se opera. Como se actualiza cada segundo, tiene un impacto insignificante en la interfaz.
- Cero descartados en el grupo Packet Loss no garantiza audio limpio. Compruebe Jitter Estimate y Max Arrival Gap para detectar problemas relacionados con el tiempo incluso cuando la pérdida es cero.
- Max Latency (RTT) se acumula desde el momento de la conexión. Reconéctese a la radio para reiniciarlo.

## Relacionados

- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
- [Medir el RTT y los descartados de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Comprobar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Observar la marca de tiempo del primer paquete UDP tras la conexión](../../getting-started/setup/watch-the-first-udp-packet-timestamp-after-connect.md)
