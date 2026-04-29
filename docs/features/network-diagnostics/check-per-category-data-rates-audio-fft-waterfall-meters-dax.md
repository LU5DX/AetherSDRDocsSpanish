# Verificar tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)

El diálogo Network Diagnostics muestra tasas de entrada en tiempo real para cada categoría de flujo — Audio, FFT, Waterfall, Meters y DAX — actualizadas cada segundo. Utilícelo para confirmar que cada flujo entrega datos a la tasa esperada y para identificar qué categoría está consumiendo ancho de banda o descartando paquetes.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo se abre independientemente de si hay una radio conectada, pero los valores de tasa solo son significativos cuando hay conexión activa.

## Pasos

1. Haga clic en `Settings > Network...`.
2. Localice el grupo **Incoming Stream Rates** en el lado derecho del diálogo.
3. Lea los indicadores de tasa por categoría: **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX**. Cada uno muestra la tasa de entrada actual en kbps, recalculada una vez por segundo.
4. Localice el grupo **Packet Loss (Sequence Gaps)** debajo de la columna izquierda.
5. Lea los indicadores de descarte correspondientes: **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX**. Cada uno muestra los paquetes descartados, el total de paquetes y un porcentaje de pérdida con el formato `errors / total (pct%)`.
6. Cuando termine, haga clic en Close.

## Qué hace cada control

| Indicador | Grupo | Significado |
|---|---|---|
| **Audio** (tasa) | Incoming Stream Rates | Tasa de entrada del flujo de audio del receptor, en kbps. |
| **FFT** (tasa) | Incoming Stream Rates | Tasa de entrada de los datos FFT del panadapter, en kbps. |
| **Waterfall** (tasa) | Incoming Stream Rates | Tasa de entrada de los datos del waterfall, en kbps. |
| **Meters** (tasa) | Incoming Stream Rates | Tasa de entrada de los datos de medidores, en kbps. |
| **DAX** (tasa) | Incoming Stream Rates | Tasa de entrada de los datos de audio DAX, en kbps. |
| **Total RX** | Incoming Stream Rates | Tasa de recepción agregada de todas las categorías de flujo, en kbps. |
| **Total TX** | Incoming Stream Rates | Tasa de transmisión agregada, en kbps. |
| **Audio** (descartes) | Packet Loss (Sequence Gaps) | Paquetes de audio descartados frente al total, con porcentaje de pérdida. |
| **FFT** (descartes) | Packet Loss (Sequence Gaps) | Paquetes FFT descartados frente al total, con porcentaje de pérdida. |
| **Waterfall** (descartes) | Packet Loss (Sequence Gaps) | Paquetes de waterfall descartados frente al total, con porcentaje de pérdida. |
| **Meters** (descartes) | Packet Loss (Sequence Gaps) | Paquetes de medidores descartados frente al total, con porcentaje de pérdida. |
| **DAX** (descartes) | Packet Loss (Sequence Gaps) | Paquetes DAX descartados frente al total, con porcentaje de pérdida. |

Todos los valores de tasa se calculan a partir del delta de bytes durante el intervalo de un segundo anterior y se expresan en kbps. Los conteos de descartes se infieren a partir de números de secuencia VITA-49 faltantes.

## Consejos

- Una tasa de 0 kbps en una categoría que debería estar activa (por ejemplo, **Audio** mientras hay un slice abierto) indica que el flujo ha dejado de llegar. Verifique primero el indicador **Status** en el grupo **Network Status**.
- Variaciones grandes en la tasa de una categoría de segundo a segundo pueden indicar entrega irregular (bursty), incluso cuando el conteo de descartes permanece en cero.
- Cero descartes en el grupo **Packet Loss** no descarta jitter ni ráfagas con llegada tardía. Si el audio tiene interrupciones pero los descartes muestran cero, revise el grupo **Audio Playback** para detectar underruns y jitter.

## Solución de problemas

- **Todas las tasas por categoría muestran 0 kbps** — La radio no está transmitiendo flujos. Confirme que la conexión está activa verificando **Status** y **Target Radio IP** en el grupo **Network Status**. Si es necesario, vuelva a conectarse mediante `Settings > Connect to Radio...`.
- **La tasa de DAX muestra 0 kbps cuando se espera actividad DAX** — Es posible que el streaming DAX no esté habilitado. Verifique que DAX esté iniciado; en las plataformas compatibles, revise `Settings > Autostart DAX with AetherSDR`.
- **El porcentaje de pérdida es distinto de cero en una sola categoría** — La pérdida está aislada en ese flujo. Esto puede indicar que la radio está sobrecargada para ese tipo de datos específico, o que una cola de red está descartando preferentemente paquetes UDP de ese tamaño.

## Relacionados

- [Descripción general de Network Diagnostics](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnosticar underruns de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
