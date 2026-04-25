# Verificar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)

El diálogo Network Diagnostics muestra las tasas de entrada en tiempo real y el conteo de paquetes perdidos para cada categoría de flujo — Audio, FFT, Waterfall, Meters y DAX — actualizados una vez por segundo. Utilícelo para identificar qué tipo de flujo está consumiendo ancho de banda o perdiendo paquetes durante un problema.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión activa con la radio, pero los campos de tasa mostrarán 0 kbps hasta que la radio esté conectada y transmitiendo datos.

## Pasos

1. Haga clic en `Settings > Network...`.
2. Se abre el diálogo **Network Diagnostics**. Localice el grupo **Incoming Stream Rates** en la parte superior derecha del diálogo.
3. Lea los campos de tasa por categoría: **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX**. Cada uno muestra la tasa de entrada actual en kbps, recalculada cada segundo.
4. Localice el grupo **Packet Loss (Sequence Gaps)** en la parte inferior izquierda. Lea los campos correspondientes de **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX**. Cada uno muestra los paquetes descartados, el total de paquetes y el porcentaje de pérdida.
5. Observe ambos grupos durante varios segundos para verificar si las tasas son estables o fluctúan. Variaciones grandes pueden indicar una entrega irregular incluso cuando no se pierden paquetes.
6. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Indicador | Ubicación | Significado |
|---|---|---|
| **Audio** (Incoming Stream Rates) | Grupo Incoming Stream Rates | Tasa de entrada del flujo de audio, en kbps. |
| **FFT** (Incoming Stream Rates) | Grupo Incoming Stream Rates | Tasa de entrada de datos FFT (espectro del panadapter), en kbps. |
| **Waterfall** (Incoming Stream Rates) | Grupo Incoming Stream Rates | Tasa de entrada de datos de mosaicos del waterfall, en kbps. |
| **Meters** (Incoming Stream Rates) | Grupo Incoming Stream Rates | Tasa de entrada de datos de medidores, en kbps. |
| **DAX** (Incoming Stream Rates) | Grupo Incoming Stream Rates | Tasa de entrada de datos de audio DAX, en kbps. |
| **Total RX** | Grupo Incoming Stream Rates | Tasa de entrada agregada de todos los flujos, en kbps. |
| **Total TX** | Grupo Incoming Stream Rates | Tasa de salida agregada, en kbps. |
| **Audio** (Packet Loss) | Grupo Packet Loss (Sequence Gaps) | Paquetes de audio descartados / totales y porcentaje, inferidos a partir de brechas en la secuencia VITA. |
| **FFT** (Packet Loss) | Grupo Packet Loss (Sequence Gaps) | Paquetes FFT descartados / totales y porcentaje. |
| **Waterfall** (Packet Loss) | Grupo Packet Loss (Sequence Gaps) | Paquetes de waterfall descartados / totales y porcentaje. |
| **Meters** (Packet Loss) | Grupo Packet Loss (Sequence Gaps) | Paquetes de medidores descartados / totales y porcentaje. |
| **DAX** (Packet Loss) | Grupo Packet Loss (Sequence Gaps) | Paquetes DAX descartados / totales y porcentaje. |

Las tasas se calculan a partir del delta de bytes durante el intervalo de un segundo anterior y se expresan en kbps. Los porcentajes de pérdida son acumulativos desde que se abrió el diálogo.

## Consejos

- Cero pérdidas en el grupo **Packet Loss (Sequence Gaps)** no descarta la presencia de jitter o ráfagas de paquetes tardíos. Si el audio se interrumpe con cero pérdidas, revise el grupo **Audio Playback** para ver las cifras de subdesbordamiento (underrun) y jitter.
- Una tasa DAX de 0 kbps mientras DAX está habilitado puede indicar que el puente DAX aún no se ha iniciado o no está enrutando audio. Verifique el estado de inicio automático en `Settings > Autostart DAX with AetherSDR`.

## Relacionado

- [Descripción general de Network Diagnostics](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
