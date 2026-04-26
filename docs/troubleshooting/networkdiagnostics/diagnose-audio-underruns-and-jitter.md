# Diagnosticar subdesbordamientos de búfer de audio y jitter

Use esta página para leer los indicadores de búfer de audio y jitter en Network Diagnostics, e identificar por qué el audio recibido suena entrecortado, silencioso o con fallas.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión de radio activa, pero los indicadores de audio solo tienen sentido cuando hay una radio conectada y transmitiendo audio.
- Abra el diálogo y déjelo visible mientras reproduce el problema de audio.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. Localice el grupo **Audio Playback** en la zona inferior derecha del diálogo.
3. Observe **RX Buffer Now** y **RX Buffer Peak**. Los valores se muestran en bytes y milisegundos. Un búfer que se mantiene cerca de cero mientras los subdesbordamientos aumentan indica que el hilo de reproducción no recibe datos suficientes.
4. Observe **Underruns (total)** y **Underruns (last sec)**. **Underruns (last sec)** se reinicia cada segundo, por lo que un valor distinto de cero sostenido aquí significa que el problema está ocurriendo en ese momento y no es histórico.
5. Observe **Audio Arrival Gap** y **Max Arrival Gap**. Estos muestran el tiempo de llegada entre paquetes. Un **Max Arrival Gap** grande en relación con **Audio Arrival Gap** indica ráfagas de paquetes tardíos, aunque no se haya descartado ningún paquete.
6. Observe **Network Jitter**. Es una estimación suavizada de la variación de temporización en el flujo de audio. Un jitter en aumento junto con subdesbordamientos crecientes apunta a un problema de entrega en la red, no a un problema con el dispositivo de audio local.
7. Verifique el grupo **Packet Loss (Sequence Gaps)**. Busque la fila **Audio** dentro de ese grupo. Un contador de descartes distinto de cero confirma pérdida real de paquetes, además de cualquier jitter.
8. Haga clic en Close cuando termine.

## Qué hace cada control

| Indicador | Significado |
|---|---|
| **RX Buffer Now** | Nivel de llenado actual del búfer de audio, en bytes y milisegundos. |
| **RX Buffer Peak** | Mayor nivel de llenado del búfer registrado desde que se abrió el diálogo. |
| **Underruns (total)** | Contador acumulado de subdesbordamientos del búfer de audio desde la conexión. |
| **Underruns (last sec)** | Subdesbordamientos contados en el intervalo de un segundo más reciente. |
| **Audio Arrival Gap** | Intervalo de llegada típico entre paquetes, en milisegundos. |
| **Max Arrival Gap** | Mayor intervalo individual entre paquetes registrado, en milisegundos. |
| **Network Jitter** | Estimación suavizada del jitter para el flujo de audio, en milisegundos. |

Todos los indicadores se actualizan cada segundo.

## Consejos

- Una pérdida de paquetes de cero en la fila de descartes de **Audio** no descarta el jitter. Los paquetes pueden llegar tarde en ráfagas sin ser descartados, y **Max Arrival Gap** reflejará eso donde el contador de descartes no lo hará.
- Si **Underruns (last sec)** es cero pero **Underruns (total)** es distinto de cero, el problema fue transitorio y puede haberse resuelto por sí solo.
- Si **RX Buffer Peak** es alto pero **RX Buffer Now** está cerca de cero y los subdesbordamientos aumentan, el búfer se llenó brevemente al conectar y luego se vació. Esto puede indicar que el dispositivo de salida de audio está consumiendo datos más rápido que la tasa de llegada del flujo entrante.

## Solución de problemas

- **Subdesbordamientos en aumento, RX Buffer Now cerca de cero, Network Jitter bajo** — La red está entregando audio a tiempo, pero el dispositivo de salida de audio local puede estar consumiendo datos más rápido de lo que llegan los paquetes. Verifique la frecuencia de muestreo de salida de audio y la configuración del dispositivo en `Settings > Radio Setup...`.
- **Subdesbordamientos en aumento, Max Arrival Gap mucho mayor que Audio Arrival Gap** — Los paquetes están llegando en ráfagas. La ruta de red tiene retardo variable. Reduzca el tráfico en la red local o cambie a una conexión por cable.
- **Contador de descartes de Audio distinto de cero en el grupo Packet Loss** — Los paquetes se están perdiendo en tránsito, no solo retrasando. Verifique si hay interferencia inalámbrica o cambie de interfaz de red. Consulte [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md).
- **Network Jitter en aumento constante** — La ruta de red es cada vez más inestable. Verifique **Latency (RTT)** y **Max Latency (RTT)** en el grupo **Network Status** para obtener evidencia corroborante.

## Relacionado

- [Descripción general de Network Diagnostics](../../features/network-diagnostics/overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](../../features/network-diagnostics/check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
