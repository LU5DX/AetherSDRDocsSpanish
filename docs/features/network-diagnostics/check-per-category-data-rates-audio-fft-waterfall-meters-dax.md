# Verificar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)

El diálogo Network Diagnostics muestra las tasas de entrada en vivo para cada categoría de flujo — Audio, FFT, Waterfall, Meters y DAX — actualizadas cada segundo. Use esta vista para confirmar que cada tipo de flujo está activo y para identificar qué categoría consume ancho de banda cuando el enlace está bajo presión.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo se abre independientemente de si hay una radio conectada, pero las tasas mostrarán cero hasta que haya una conexión activa.
- Se recomienda tener una radio conectada para que los campos de tasa se pueblen con datos en vivo.

## Pasos

1. Haga clic en `Settings > Network...`.
2. Se abre el diálogo **Network Diagnostics**. Localice el grupo **Incoming Stream Rates** en el lado derecho del diálogo.
3. Lea los campos de tasa por categoría: **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX**. Cada valor se expresa en kbps y se actualiza una vez por segundo.
4. Revise **Total RX** para obtener la tasa de entrada agregada de todas las categorías.
5. Revise **Total TX** para obtener la tasa de salida agregada.
6. Para verificar si alguna categoría está perdiendo paquetes junto con su tasa, observe la fila correspondiente en el grupo **Packet Loss (Sequence Gaps)**: los contadores de caída de **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX** aparecen ahí como `errors / total packets (%)`.
7. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Indicador | Qué muestra |
|---|---|
| **Audio** (Incoming Stream Rates) | Tasa de entrada del flujo de audio de recepción, en kbps. |
| **FFT** (Incoming Stream Rates) | Tasa de entrada de los datos FFT del panadapter, en kbps. |
| **Waterfall** (Incoming Stream Rates) | Tasa de entrada de los datos de mosaico del waterfall, en kbps. |
| **Meters** (Incoming Stream Rates) | Tasa de entrada de los datos de medidores, en kbps. |
| **DAX** (Incoming Stream Rates) | Tasa de entrada de los flujos de audio DAX, en kbps. |
| **Total RX** | Bytes de entrada por segundo agregados de todas las categorías, en kbps. |
| **Total TX** | Bytes de salida por segundo agregados, en kbps. |
| **Audio** (Packet Loss) | Paquetes de audio descartados mostrados como `errors / total (%)`. |
| **FFT** (Packet Loss) | Paquetes FFT descartados mostrados como `errors / total (%)`. |
| **Waterfall** (Packet Loss) | Paquetes de waterfall descartados mostrados como `errors / total (%)`. |
| **Meters** (Packet Loss) | Paquetes de medidores descartados mostrados como `errors / total (%)`. |
| **DAX** (Packet Loss) | Paquetes DAX descartados mostrados como `errors / total (%)`. |

## Consejos

- Las tasas se calculan a partir del cambio en el conteo de bytes durante cada intervalo de actualización de un segundo. Grandes variaciones entre segundos pueden indicar una entrega intermitente incluso cuando los contadores de caída permanecen en cero.
- Una tasa DAX de 0 kbps cuando se espera que DAX esté activo es una señal temprana útil de que el puente DAX no está en ejecución o no está recibiendo datos de la radio.
- Un conteo de caídas en cero no descarta jitter o ráfagas que llegan tarde. Si la calidad de audio es deficiente a pesar de contar con contadores de caída limpios, revise el grupo **Audio Playback** para obtener datos de subdesbordamiento (underrun) y jitter.

## Solución de problemas

- **Todas las tasas muestran 0 kbps** — La radio no está conectada o no se han iniciado flujos. Verifique la conexión mediante `Settings > Connect to Radio...` y compruebe el campo **Status** en el grupo **Network Status**.
- **La tasa DAX es 0 kbps pero otras categorías muestran tráfico** — Es posible que DAX no esté habilitado. Verifique si el inicio automático de DAX está activo mediante `Settings > Autostart DAX with AetherSDR`.
- **El porcentaje de caída es distinto de cero en FFT o Waterfall pero el audio suena bien** — Las caídas en flujos visuales son generalmente menos perceptibles que las caídas de audio. Monitoree con el tiempo; una pérdida sostenida superior a unos pocos por ciento justifica investigar la ruta de red.

## Relacionados

- [Descripción general de Network Diagnostics](overview.md)
- [Medir el RTT y las caídas de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
