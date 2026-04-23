# Diagnóstico de interrupciones y jitter de audio

Use el cuadro de diálogo Network Diagnostics para leer el estado del búfer de audio, los contadores de interrupciones y los indicadores de jitter que identifican la causa del audio recibido entrecortado o interrumpido.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El cuadro de diálogo no requiere una conexión de radio activa, pero los indicadores de audio solo son significativos mientras haya una radio conectada y transmitiendo audio.
- Reproduzca el problema de audio antes de abrir el cuadro de diálogo para que los contadores acumulen datos durante la falla.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el cuadro de diálogo Network Diagnostics.
2. Deje que la pantalla se actualice durante al menos 10–15 segundos mientras el problema de audio esté ocurriendo. El cuadro de diálogo se actualiza cada segundo.
3. Observe el grupo **Audio Playback** en la parte inferior derecha del cuadro de diálogo. Lea estos indicadores en orden:

   a. **RX Buffer Now** — nivel de llenado actual del búfer de reproducción de audio, mostrado en bytes y milisegundos. Un valor cercano a cero mientras las interrupciones aumentan significa que la reproducción está sin datos suficientes.

   b. **RX Buffer Peak** — mayor nivel de llenado del búfer registrado desde que se abrió el cuadro de diálogo. Un valor máximo muy bajo combinado con interrupciones confirma que el búfer nunca ha acumulado suficiente margen.

   c. **Underruns (total)** — conteo acumulado de interrupciones del búfer de reproducción desde que se inició el motor de audio.

   d. **Underruns (last sec)** — interrupciones ocurridas en la ventana de un segundo más reciente. Un valor distinto de cero aquí significa que el problema está activo en este momento.

   e. **Audio Arrival Gap** — intervalo de llegada actual entre paquetes del flujo de audio.

   f. **Max Arrival Gap** — mayor intervalo de llegada observado desde la conexión. Un intervalo máximo grande en relación con un intervalo de llegada normal apunta a retrasos en ráfagas en lugar de pérdida continua.

   g. **Jitter Estimate** — medida suavizada de la variación de temporización en el flujo de audio. El aumento del jitter con un nivel de búfer bajo es una causa común de interrupciones.

4. Verifique el grupo **Packet Loss (Sequence Gaps)**. Lea la fila **Audio** de pérdidas. Si el conteo de pérdidas es cero pero las interrupciones aumentan, el problema es la temporización de entrega o la falta de datos en el búfer, no la pérdida de paquetes.
5. Verifique el grupo **Incoming Stream Rates**. Lea la fila de tasa **Audio**. Las grandes variaciones de un segundo al siguiente indican una entrega en ráfagas incluso cuando no se pierden paquetes.
6. Haga clic en Close cuando termine.

## Qué muestra cada control

| Indicador | Qué muestra |
|---|---|
| **RX Buffer Now** | Nivel de llenado actual del búfer de reproducción de audio, en bytes y milisegundos. |
| **RX Buffer Peak** | Mayor nivel de llenado del búfer registrado desde que se abrió el cuadro de diálogo. |
| **Underruns (total)** | Total de interrupciones del búfer de audio desde que se inició el motor de audio. |
| **Underruns (last sec)** | Interrupciones en el intervalo de un segundo más reciente. |
| **Audio Arrival Gap** | Temporización de llegada entre paquetes actual del flujo de audio. |
| **Max Arrival Gap** | Mayor intervalo de llegada entre paquetes observado desde la conexión. |
| **Jitter Estimate** | Jitter suavizado del flujo de audio entrante. |

Ninguno de estos indicadores tiene claves de configuración persistentes. Son mediciones en tiempo real de solo lectura.

## Consejos

- La pérdida de paquetes cero en la fila **Audio** no descarta las interrupciones. Los paquetes pueden llegar en ráfagas que agotan el búfer sin que existan brechas en la secuencia.
- La nota del cuadro de diálogo para el grupo Audio Playback indica: "If underruns rise while the buffer stays near zero, playback is starving." Revise **RX Buffer Now** y **Underruns (last sec)** juntos, no por separado.
- El intervalo de llegada y el jitter miden la temporización, no la pérdida de paquetes. Un **Max Arrival Gap** grande con un **Jitter Estimate** bajo sugiere una única ráfaga aislada en lugar de un problema crónico de jitter.

## Solución de problemas

- **Underruns (last sec) es distinto de cero pero el conteo de pérdidas de Audio es cero** — los paquetes están llegando pero no a tiempo. La ruta de red está introduciendo ráfagas o jitter. Investigue el switch, el cable o el segmento Wi-Fi entre el host y el radio Flex.
- **RX Buffer Now muestra un valor cercano a cero constantemente** — el búfer no se está llenando. Verifique que el flujo de audio esté activo y que la tasa de **Audio** en el grupo Incoming Stream Rates sea distinta de cero.
- **Max Arrival Gap es grande pero el Audio Arrival Gap actual es normal** — ocurrió un único evento de ráfaga en algún momento desde la conexión. Vuelva a abrir el cuadro de diálogo y monitoree durante un período más largo para determinar si se repite.

## Relacionados

- [Descripción general de Network Diagnostics](../../features/network-diagnostics/overview.md)
- [Medición de RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificación de tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](../../features/network-diagnostics/check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
