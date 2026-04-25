# Medir RTT y pérdida de paquetes durante problemas de audio

Use el diálogo Network Diagnostics para leer en tiempo real el tiempo de ida y vuelta (RTT) y los contadores de pérdida de paquetes por categoría mientras el audio se interrumpe. Esto le ayuda a distinguir una ruta de red con pérdidas de un problema local de búfer o jitter.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión de radio activa, pero los contadores de RTT y pérdida solo mostrarán datos significativos mientras esté conectado.
- Reproduzca o espere a que el problema de audio vuelva a ocurrir para poder observar los contadores en tiempo real.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. Observe el campo **Latency (RTT)**. Se actualiza cada segundo y muestra el tiempo de ida y vuelta actual en milisegundos.
3. Observe el campo **Max Latency (RTT)**. Muestra el RTT más alto registrado desde que se conectó la radio. Un valor significativamente superior al **Latency (RTT)** habitual indica picos de latencia periódicos.
4. En el grupo **Packet Loss (Sequence Gaps)**, revise la fila **Audio**. El valor se muestra como `errors / total packets (%)`. Cualquier porcentaje distinto de cero durante problemas de audio apunta a pérdida de paquetes en la red como causa.
5. Revise las filas de pérdida restantes — **FFT**, **Waterfall**, **Meters** y **DAX** — para determinar si la pérdida se limita al flujo de audio o afecta a todas las categorías. La pérdida en todos los flujos apunta a un problema general en la ruta de red, en lugar de un problema específico del audio.
6. Si los contadores de pérdida son cero pero el audio sigue fallando, vaya al grupo **Audio Playback** y revise **Underruns (total)**, **Underruns (last sec)**, **RX Buffer Now** y **Network Jitter**. Cero pérdidas con underruns en aumento indican un problema local de agotamiento de búfer o jitter, no pérdida de paquetes.
7. Haga clic en Close cuando termine.

## Qué hace cada control

| Indicador | Dónde aparece | Significado |
|---|---|---|
| **Latency (RTT)** | Network Status | Tiempo de ida y vuelta actual hacia la radio, en milisegundos. Los valores inferiores a 1 ms se muestran como `< 1 ms`. |
| **Max Latency (RTT)** | Network Status | RTT más alto observado desde que se conectó la radio. Se reinicia al reconectar. |
| **Audio** (Packet Loss) | Packet Loss (Sequence Gaps) | Paquetes de audio perdidos inferidos a partir de números de secuencia VITA-49 faltantes, mostrados como `errors / total (%)`. |
| **FFT** (Packet Loss) | Packet Loss (Sequence Gaps) | Paquetes FFT perdidos por el mismo método. |
| **Waterfall** (Packet Loss) | Packet Loss (Sequence Gaps) | Paquetes de waterfall perdidos. |
| **Meters** (Packet Loss) | Packet Loss (Sequence Gaps) | Paquetes de medidores perdidos. |
| **DAX** (Packet Loss) | Packet Loss (Sequence Gaps) | Paquetes DAX perdidos. |
| **RX Buffer Now** | Audio Playback | Nivel de llenado actual del búfer de recepción de audio, en bytes y milisegundos. |
| **RX Buffer Peak** | Audio Playback | Nivel máximo de llenado del búfer observado desde la conexión. |
| **Underruns (total)** | Audio Playback | Conteo acumulado de underruns del búfer de audio desde la conexión. |
| **Underruns (last sec)** | Audio Playback | Underruns ocurridos en la ventana de un segundo más reciente. |
| **Audio Arrival Gap** | Audio Playback | Intervalo de llegada entre paquetes, que mide la temporización de entrega. |
| **Max Arrival Gap** | Audio Playback | Mayor intervalo entre paquetes observado desde la conexión. |
| **Network Jitter** | Audio Playback | Estimación suavizada del jitter del flujo de audio. |

## Consejos

- Todos los valores se actualizan automáticamente una vez por segundo. Deje el diálogo abierto durante un período de problemas y observe qué contadores cambian en el momento en que el audio se degrada.
- Cero pérdida de paquetes en el grupo **Packet Loss (Sequence Gaps)** no descarta el jitter. La nota del propio diálogo indica: "Zero loss here does not rule out jitter or late bursts." Revise también **Network Jitter** y **Max Arrival Gap**.
- **Max Latency (RTT)** persiste durante toda la sesión. Si es mucho mayor que **Latency (RTT)** en el momento en que abre el diálogo, ya ocurrió un pico que pudo haber pasado desapercibido.

## Solución de problemas

- **Todos los contadores de pérdida muestran 0 pero el audio sigue fallando** — El problema no es pérdida de paquetes. Revise **Underruns (last sec)** y **Network Jitter** en el grupo Audio Playback. Consulte [Diagnosticar underruns de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md).
- **RTT muestra `< 1 ms` y todos los contadores de pérdida son cero** — Es posible que la radio no esté conectada. Confirme que **Status** y **Target Radio IP** en el grupo Network Status muestren una conexión activa. Consulte [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md).
- **Solo la fila de pérdida de Audio es distinta de cero mientras FFT, Waterfall y Meters muestran cero** — La pérdida es específica del flujo y no una falla general de la ruta de red. Esto puede indicar un comportamiento de QoS o del switch que trata los flujos UDP de forma diferente; el flujo UDP de audio puede estar siendo deprioritizado.

## Relacionado

- [Descripción general de Network Diagnostics](overview.md)
- [Verificar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar underruns de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
