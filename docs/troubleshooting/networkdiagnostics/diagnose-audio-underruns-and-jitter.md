# Diagnosticar subdesbordamientos de audio y jitter

Use el diálogo Network Diagnostics para leer en tiempo real los indicadores del búfer de audio y el jitter, e identifique la causa de clics, interrupciones o audio entrecortado.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión de radio activa, pero los indicadores de audio solo son significativos mientras esté conectado y recibiendo audio.
- Reproduzca el problema de audio antes de leer los indicadores — los contadores acumulan valores desde la última conexión y las tasas se actualizan cada segundo.

## Pasos

1. Abra `Settings > Network...`. El diálogo Network Diagnostics se abre.
2. Localice el grupo **Audio Playback** en la zona inferior derecha del diálogo.
3. Lea **RX Buffer Now**. Muestra el nivel actual de llenado del búfer de audio en bytes y milisegundos. Si este valor está cerca de cero mientras los subdesbordamientos aumentan, la reproducción está sin datos suficientes.
4. Lea **RX Buffer Peak**. Muestra el nivel máximo de llenado del búfer registrado desde la conexión. Un pico muy bajo junto con subdesbordamientos frecuentes confirma que el búfer nunca acumula un margen adecuado.
5. Lea **Underruns (total)**. Es el recuento acumulado de subdesbordamientos de audio desde la conexión.
6. Lea **Underruns (last sec)**. Muestra cuántos subdesbordamientos ocurrieron en la ventana de un segundo más reciente. Un valor distinto de cero aquí indica que el problema está activo en este momento.
7. Lea **Audio Arrival Gap** y **Max Arrival Gap**. Muestran el intervalo de llegada entre paquetes. Un **Max Arrival Gap** grande en relación con un **Audio Arrival Gap** normal indica ráfagas ocasionales de paquetes tardíos en lugar de un flujo constante.
8. Lea **Network Jitter**. Es la estimación de jitter suavizada para el flujo de audio. Un jitter alto combinado con un valor bajo de **RX Buffer Now** es el indicador principal de que el búfer de recepción es demasiado pequeño para absorber la variación de temporización en esta ruta de red.
9. Verifique el grupo **Packet Loss (Sequence Gaps)**. Observe la fila de caídas **Audio**. Cero caídas con jitter alto significa que los paquetes llegan, pero no a tiempo. Caídas de audio distintas de cero indican que los paquetes se están perdiendo realmente.
10. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Indicador | Significado |
|---|---|
| **RX Buffer Now** | Nivel actual de llenado del búfer de audio, mostrado en bytes y milisegundos. |
| **RX Buffer Peak** | Nivel máximo de llenado del búfer registrado desde la conexión. |
| **Underruns (total)** | Recuento acumulado de subdesbordamientos de audio desde la conexión. |
| **Underruns (last sec)** | Subdesbordamientos observados en el último intervalo de un segundo. |
| **Audio Arrival Gap** | Intervalo típico de llegada entre paquetes para el flujo de audio. |
| **Max Arrival Gap** | Mayor intervalo individual entre paquetes registrado desde la conexión. |
| **Network Jitter** | Estimación de jitter suavizada para el flujo de audio. |
| **Audio** (fila Packet Loss) | Paquetes de audio descartados inferidos a partir de saltos en la secuencia VITA, mostrados como errores / paquetes totales y porcentaje. |

## Consejos

- El diálogo se actualiza cada segundo. Observe **Underruns (last sec)** en lugar de **Underruns (total)** para determinar si el problema es actual o histórico.
- Cero pérdida de paquetes en el grupo **Packet Loss** no descarta el jitter. Los paquetes pueden llegar tarde — causando subdesbordamientos — sin ser contados como caídas.
- Grandes variaciones en la tasa **Audio** del grupo **Incoming Stream Rates** pueden indicar una entrega en ráfagas, incluso cuando no se detectan saltos de secuencia.

## Solución de problemas

- **Underruns (last sec) es distinto de cero pero Audio drops muestra cero** — Los paquetes están llegando en ráfagas. El jitter de red está consumiendo el búfer. Revise su switch, la calidad del cableado o cualquier configuración de QoS en la ruta entre su computadora y la radio.
- **Tanto los subdesbordamientos como las caídas de Audio están aumentando** — Los paquetes se pierden antes de llegar. Consulte [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md) para seguir los pasos adicionales.
- **RX Buffer Peak es muy bajo** — El búfer nunca acumuló un margen significativo. Esto puede ocurrir si el audio comenzó a recibirse inmediatamente después de la conexión antes de que el búfer se inicializara; desconéctese y vuelva a conectarse, luego monitoree nuevamente.

## Relacionado

- [Descripción general de Network Diagnostics](../../features/network-diagnostics/overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](../../features/network-diagnostics/check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
