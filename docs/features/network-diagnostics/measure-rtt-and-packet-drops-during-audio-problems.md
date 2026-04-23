# Medir RTT y pérdida de paquetes durante problemas de audio

Use el diálogo Network Diagnostics para leer el tiempo de ida y vuelta actual hacia el radio y verificar si se están descartando paquetes UDP — ambos son primeros pasos útiles cuando el audio se corta o suena distorsionado.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión activa con el radio, pero los contadores de RTT y pérdida solo mostrarán valores significativos cuando haya conexión.

## Pasos

1. Haga clic en `Settings > Network...`.
2. En la sección **Network Status**, lea **Latency (RTT)** para obtener el tiempo de ida y vuelta actual en milisegundos.
3. Lea **Max Latency (RTT)** para ver el RTT más alto registrado desde que se estableció la conexión.
4. En la sección **Packet Loss (Sequence Gaps)**, lea el contador **Audio**. El valor se muestra como `<dropped> / <total> (<percent>%)`.
5. Revise los contadores **FFT**, **Waterfall**, **Meters** y **DAX** en la misma sección si desea confirmar si la pérdida se limita al flujo de audio o afecta a todos los flujos.
6. Deje el diálogo abierto durante al menos 30 segundos mientras se reproduce el problema. Los valores se actualizan cada segundo.
7. Haga clic en **Close** cuando termine.

## Qué muestra cada indicador

| Indicador | Qué muestra |
|---|---|
| **Status** | Estado general del enlace. |
| **Latency (RTT)** | Tiempo de ida y vuelta actual en ms. Muestra `< 1 ms` cuando es inferior a 1 ms. |
| **Max Latency (RTT)** | RTT más alto registrado desde la conexión. Se reinicia al reconectar. |
| **Audio** (Packet Loss) | Paquetes de audio descartados frente al total recibido, con un porcentaje. Se infiere a partir de números de secuencia VITA faltantes. |
| **FFT** (Packet Loss) | La misma métrica para el flujo FFT. |
| **Waterfall** (Packet Loss) | La misma métrica para el flujo waterfall. |
| **Meters** (Packet Loss) | La misma métrica para el flujo de medidores. |
| **DAX** (Packet Loss) | La misma métrica para el flujo de audio DAX. |

## Consejos

- Pérdida cero en la sección **Packet Loss (Sequence Gaps)** no descarta el problema. El jitter o las ráfagas de paquetes que llegan tarde pueden causar interrupciones en el audio sin generar saltos en los números de secuencia. Si los descartes son cero pero el audio sigue cortándose, revise **Audio Arrival Gap**, **Max Arrival Gap** y **Jitter Estimate** en la sección **Audio Playback**.
- Grandes variaciones en la tasa **Audio** bajo **Incoming Stream Rates** indican una entrega irregular incluso cuando no se contabiliza ningún paquete como perdido.
- **Max Latency (RTT)** acumula valores desde el momento de la conexión. Si abrió el diálogo después de que comenzara el problema, el valor pico puede no reflejar el peor momento.

## Solución de problemas

- **Todos los campos RTT muestran `< 1 ms` y los descartes permanecen en `0 / 0`** — El radio no está conectado. Conéctese primero mediante `Settings > Connect to Radio...` y luego vuelva a abrir `Settings > Network...`.
- **Los descartes de audio son distintos de cero pero el RTT parece estable** — La pérdida ocurre en la capa UDP sin afectar el tiempo de ping TCP. Verifique si hay interferencia en Wi-Fi, configuraciones de QoS en los switches u otro tráfico que compita en el mismo segmento de LAN.

## Temas relacionados

- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Verificar la dirección IP del radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
