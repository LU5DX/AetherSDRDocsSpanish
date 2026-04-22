# Medir RTT y pérdida de paquetes durante problemas de audio

Use el diálogo Network Diagnostics para leer en tiempo real el tiempo de ida y vuelta (RTT) y los contadores de pérdida de paquetes por categoría mientras ocurre un problema de audio. Esto le ayuda a distinguir entre pérdida en la red y inanición de audio local.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión activa con la radio, pero los datos significativos de RTT y pérdida solo aparecen después de que la radio esté conectada.
- Reproduzca o mantenga el problema de audio para que los contadores se actualicen activamente en el momento de la lectura.

## Pasos

1. Haga clic en `Settings > Network...`. Se abre el diálogo Network Diagnostics.
2. Observe el indicador **Latency (RTT)**. Muestra el tiempo de ida y vuelta actual hacia la radio en milisegundos. Los valores inferiores a 1 ms se muestran como `< 1 ms`.
3. Observe **Max Latency (RTT)**. Muestra el RTT más alto medido desde que se estableció la conexión. Una diferencia grande entre **Latency (RTT)** y **Max Latency (RTT)** indica que el enlace ha tenido picos.
4. En el grupo **Packet Loss (Sequence Gaps)**, lea el indicador de pérdida **Audio**. El valor se muestra como `errors / total packets (%)`. Cualquier conteo de errores distinto de cero durante problemas de audio apunta a pérdida de paquetes en la red sobre el flujo de audio.
5. Revise las filas de pérdida restantes — **FFT**, **Waterfall**, **Meters** y **DAX** — para determinar si la pérdida se limita al audio o afecta a todas las categorías de flujo. La pérdida en todas las categorías sugiere un problema general del enlace y no uno específico del audio.
6. Anote el indicador **Status** para el estado general del enlace.
7. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Indicador | Dónde aparece | Significado |
|---|---|---|
| **Status** | Grupo Network Status | Estado general del enlace reportado por el modelo de radio. |
| **Latency (RTT)** | Grupo Network Status | Tiempo de ida y vuelta actual, actualizado cada segundo. Se muestra en ms; aparece como `< 1 ms` cuando es inferior a 1 ms. |
| **Max Latency (RTT)** | Grupo Network Status | RTT más alto registrado desde la conexión. Se reinicia al reconectar. |
| **Audio** (Packet Loss) | Grupo Packet Loss (Sequence Gaps) | Paquetes de audio descartados inferidos a partir de números de secuencia VITA faltantes, mostrados como `errors / total (%)`. |
| **FFT** (Packet Loss) | Grupo Packet Loss (Sequence Gaps) | Misma métrica para el flujo FFT. |
| **Waterfall** (Packet Loss) | Grupo Packet Loss (Sequence Gaps) | Misma métrica para el flujo waterfall. |
| **Meters** (Packet Loss) | Grupo Packet Loss (Sequence Gaps) | Misma métrica para el flujo de medidores. |
| **DAX** (Packet Loss) | Grupo Packet Loss (Sequence Gaps) | Misma métrica para el flujo DAX. |

Todos los indicadores se actualizan cada segundo. Este diálogo no guarda ninguna configuración de forma persistente.

## Consejos

- Cero pérdida de paquetes en el grupo **Packet Loss (Sequence Gaps)** no descarta el problema. El jitter y las ráfagas tardías pueden causar subdesbordamientos de audio sin producir brechas en los números de secuencia. Si los contadores de pérdida son cero pero el audio sigue fallando, revise el grupo **Audio Playback** en su lugar.
- Grandes variaciones en el grupo **Incoming Stream Rates** — incluso sin paquetes descartados — pueden indicar una entrega en ráfagas que degrada el audio.
- **Max Latency (RTT)** acumula valores desde el momento de la conexión. Si se conectó mucho antes de que comenzara el problema de audio, el pico puede ser anterior al problema actual. Desconecte y vuelva a conectar para reiniciarlo y, a continuación, reproduzca el problema.

## Solución de problemas

- **Todos los indicadores muestran guiones o cero sin radio conectada** — Los datos de RTT y pérdida requieren una conexión activa con la radio. Conéctese a la radio primero y luego vuelva a abrir el diálogo.
- **Los contadores de pérdida de audio son cero pero el audio sigue cortándose** — La pérdida en la red no es la causa. Consulte [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md) para el análisis de búfer y jitter.

## Relacionado

- [Descripción general de Network Diagnostics](overview.md)
- [Verificar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
