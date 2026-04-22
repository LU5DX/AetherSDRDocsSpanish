# Verificar tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)

El diálogo Network Diagnostics muestra las tasas de entrada en tiempo real para cada categoría de flujo — Audio, FFT, Waterfall, Meters y DAX — actualizadas cada segundo. Úselo para confirmar que el radio está entregando datos en cada flujo y para detectar tráfico errático o ausente antes de que cause problemas de audio o de visualización.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo está disponible tanto si hay un radio conectado como si no, pero las tasas mostrarán cero hasta que haya una conexión activa.
- Si desea observar las tasas bajo carga, active al menos un panadapter y un receptor antes de abrir el diálogo.

## Pasos

1. Haga clic en `Settings > Network...`.
2. En el diálogo **Network Diagnostics**, localice el grupo **Incoming Stream Rates** en el lado derecho de la ventana.
3. Lea los valores de tasa por categoría: **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX**. Cada valor se muestra en kbps y se actualiza una vez por segundo.
4. Lea **Total RX** y **Total TX** debajo de las filas de categorías para ver el rendimiento agregado en ambas direcciones.
5. Haga clic en Close cuando termine.

## Qué hace cada control

| Indicador | Qué muestra |
|---|---|
| **Audio** (Incoming Stream Rates) | Tasa de entrada del flujo de audio de recepción, en kbps. |
| **FFT** (Incoming Stream Rates) | Tasa de entrada del flujo de datos FFT del panadapter, en kbps. |
| **Waterfall** (Incoming Stream Rates) | Tasa de entrada del flujo de datos del waterfall, en kbps. |
| **Meters** (Incoming Stream Rates) | Tasa de entrada del flujo de datos de los medidores, en kbps. |
| **DAX** (Incoming Stream Rates) | Tasa de entrada del flujo de audio DAX, en kbps. |
| **Total RX** | Bytes por segundo agregados recibidos desde el radio, en kbps. |
| **Total TX** | Bytes por segundo agregados enviados al radio, en kbps. |
| **Audio** (Packet Loss) | Paquetes descartados inferidos a partir de números de secuencia VITA-49 faltantes, mostrados como errores / total de paquetes (%). |
| **FFT** (Packet Loss) | Lo mismo, para el flujo FFT. |
| **Waterfall** (Packet Loss) | Lo mismo, para el flujo del waterfall. |
| **Meters** (Packet Loss) | Lo mismo, para el flujo de medidores. |
| **DAX** (Packet Loss) | Lo mismo, para el flujo DAX. |

Todos los valores de tasa se recalculan a partir de deltas de conteo de bytes una vez por segundo. Los conteos de descarte son acumulativos desde que se estableció la conexión.

## Consejos

- Una tasa de 0 kbps en una categoría mientras el radio está conectado indica que ese flujo no está activo o no está suscrito. Por ejemplo, DAX mostrará 0 kbps si el audio DAX no está habilitado.
- Grandes variaciones en la tasa de una categoría de segundo a segundo pueden indicar entrega errática incluso cuando los contadores de descarte muestran cero pérdidas. La nota en el diálogo para este grupo indica: "Large swings can indicate bursty delivery even when no packets are lost."
- Los conteos de descarte se muestran como `errors / total packets (%)`. Un valor de `0 / 0` significa que aún no se han contado paquetes para esa categoría.

## Solución de problemas

- **Todas las tasas de categoría muestran 0 kbps** — No hay una conexión de radio activa, o la conexión se perdió. Verifique **Status** y **Target Radio IP** en el grupo **Network Status**.
- **La tasa DAX muestra 0 kbps pero otros flujos están activos** — El audio DAX no está habilitado. Habilite DAX desde el panel de applets o verifique `Settings > Autostart DAX with AetherSDR`.
- **El conteo de descarte es distinto de cero para una categoría** — Se detectaron paquetes con números de secuencia VITA-49 faltantes en ese flujo. Esto apunta a pérdida de paquetes de red en ese tipo de flujo específico. Consulte [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md) para pasos adicionales.

## Relacionados

- [Descripción general de Network Diagnostics](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnosticar subconsumos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificar la IP del radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
