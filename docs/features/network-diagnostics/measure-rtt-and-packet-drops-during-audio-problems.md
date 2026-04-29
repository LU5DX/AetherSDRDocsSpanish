# Medir el RTT y la pérdida de paquetes durante problemas de audio

Use el diálogo Network Diagnostics para leer el tiempo de ida y vuelta en vivo y los contadores de pérdida de paquetes por categoría mientras ocurren problemas de audio. Esto le permite distinguir la pérdida de red de otras causas, como el agotamiento del búfer o el jitter.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión de radio activa, pero los contadores de RTT y pérdida solo son significativos mientras hay conexión.
- Reproduzca o espere a que ocurra el problema de audio antes de leer los contadores — los conteos de pérdida se acumulan desde la conexión y el RTT refleja el momento actual.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. Lea `Latency (RTT)` para conocer el tiempo de ida y vuelta actual hacia la radio.
3. Lea `Max Latency (RTT)` para conocer el RTT más alto registrado desde que se estableció la conexión.
4. En la sección **Packet Loss (Sequence Gaps)**, lea el contador de pérdida `Audio`. El valor muestra los paquetes descartados, el total de paquetes y el porcentaje de pérdida.
5. Verifique las filas de pérdida `FFT`, `Waterfall`, `Meters` y `DAX` en la misma sección para determinar si la pérdida está aislada en el audio o afecta a todos los flujos.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Indicador | Significado |
|---|---|
| `Latency (RTT)` | Tiempo de ida y vuelta actual hacia la radio. Muestra `< 1 ms` cuando está por debajo de 1 ms. |
| `Max Latency (RTT)` | RTT más alto registrado desde la conexión. Muestra `< 1 ms` cuando está por debajo de 1 ms. |
| `Audio` (Packet Loss) | Paquetes descartados / total de paquetes (% de pérdida) para el flujo de audio, inferido a partir de números de secuencia VITA-49 faltantes. |
| `FFT` (Packet Loss) | La misma métrica para el flujo FFT. |
| `Waterfall` (Packet Loss) | La misma métrica para el flujo del waterfall. |
| `Meters` (Packet Loss) | La misma métrica para el flujo de medidores. |
| `DAX` (Packet Loss) | La misma métrica para el flujo DAX. |
| `Status` | Estado general del enlace. |

Todos los contadores se actualizan una vez por segundo.

## Consejos

- Una pérdida de cero en la sección Packet Loss no descarta el problema. El jitter y la entrega tardía en ráfagas pueden causar interrupciones de audio sin generar brechas en los números de secuencia. Si los contadores de pérdida son cero pero el audio sigue fallando, verifique `Underruns (total)`, `Underruns (last sec)`, `Audio Arrival Gap`, `Max Arrival Gap` y `Jitter Estimate` en la sección **Audio Playback**.
- `Max Latency (RTT)` es más útil que el RTT actual para detectar picos transitorios que ya han pasado.
- La pérdida que aparece simultáneamente en todas las categorías de flujos apunta a un problema en la ruta de red compartida, en lugar de un problema específico del audio.

## Solución de problemas

- **Todos los contadores de pérdida muestran 0 / 0** — No se han recibido paquetes VITA en esa categoría. Confirme que la radio está conectada y transmitiendo los flujos correspondientes.
- **El RTT muestra `< 1 ms` pero el audio falla** — La latencia de red no es la causa. Consulte la sección Audio Playback para obtener datos de subdesbordamiento y jitter.

## Relacionados

- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Descripción general de Network Diagnostics](overview.md)
- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
