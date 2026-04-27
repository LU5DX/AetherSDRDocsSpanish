# Verificar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)

El diálogo Network Diagnostics muestra las tasas de entrada en tiempo real para cada categoría de flujo — Audio, FFT, Waterfall, Meters y DAX — actualizadas cada segundo. Úselo para confirmar que cada flujo entrega datos a la tasa esperada e identificar qué categoría consume ancho de banda o pierde paquetes.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo se abre independientemente de si hay una radio conectada, pero los valores de tasa solo son significativos cuando hay conexión activa.

## Pasos

1. Haga clic en `Settings > Network...`.
2. Localice el grupo **Incoming Stream Rates** en el lado derecho del diálogo.
3. Lea los indicadores de tasa por categoría: **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX**. Cada uno muestra la tasa de entrada actual en kbps, recalculada una vez por segundo.
4. Localice el grupo **Packet Loss (Sequence Gaps)** debajo de la columna izquierda.
5. Lea los indicadores de pérdida correspondientes: **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX**. Cada uno muestra los paquetes descartados, los paquetes totales y un porcentaje de pérdida en la forma `errors / total (pct%)`.
6. Cuando termine, haga clic en Close.

## Qué hace cada control

| Indicador | Grupo | Significado |
|---|---|---|
| **Audio** (tasa) | Incoming Stream Rates | Tasa de entrada del flujo de audio del receptor, en kbps. |
| **FFT** (tasa) | Incoming Stream Rates | Tasa de entrada de los datos FFT del panadapter, en kbps. |
| **Waterfall** (tasa) | Incoming Stream Rates | Tasa de entrada de los datos del waterfall, en kbps. |
| **Meters** (tasa) | Incoming Stream Rates | Tasa de entrada de los datos de los medidores, en kbps. |
| **DAX** (tasa) | Incoming Stream Rates | Tasa de entrada de los datos de audio DAX, en kbps. |
| **Total RX** | Incoming Stream Rates | Tasa de recepción agregada en todas las categorías de flujo, en kbps. |
| **Total TX** | Incoming Stream Rates | Tasa de transmisión agregada, en kbps. |
| **Audio** (pérdidas) | Packet Loss (Sequence Gaps) | Paquetes de audio descartados frente al total, con porcentaje de pérdida. |
| **FFT** (pérdidas) | Packet Loss (Sequence Gaps) | Paquetes FFT descartados frente al total, con porcentaje de pérdida. |
| **Waterfall** (pérdidas) | Packet Loss (Sequence Gaps) | Paquetes de waterfall descartados frente al total, con porcentaje de pérdida. |
| **Meters** (pérdidas) | Packet Loss (Sequence Gaps) | Paquetes de medidores descartados frente al total, con porcentaje de pérdida. |
| **DAX** (pérdidas) | Packet Loss (Sequence Gaps) | Paquetes DAX descartados frente al total, con porcentaje de pérdida. |

Todos los valores de tasa se calculan a partir del delta de bytes durante el intervalo de un segundo anterior y se expresan en kbps. Los conteos de pérdida se infieren a partir de los números de secuencia VITA-49 faltantes.

## Consejos

- Una tasa de 0 kbps en una categoría que debería estar activa (por ejemplo, **Audio** mientras hay un slice abierto) indica que el flujo ha dejado de llegar. Revise primero el indicador **Status** en el grupo **Network Status**.
- Variaciones grandes en la tasa de una categoría de segundo a segundo pueden indicar una entrega irregular, incluso cuando el conteo de pérdidas permanece en cero.
- Cero pérdidas en el grupo **Packet Loss** no descarta jitter ni ráfagas con retardo. Si el audio es entrecortado pero las pérdidas muestran cero, revise el grupo **Audio Playback** para detectar subdesbordamientos (underruns) y jitter.

## Solución de problemas

- **Todas las tasas por categoría muestran 0 kbps** — La radio no está enviando flujos. Confirme que la conexión está activa revisando **Status** y **Target Radio IP** en el grupo **Network Status**. Si es necesario, vuelva a conectar mediante `Settings > Connect to Radio...`.
- **La tasa de DAX muestra 0 kbps cuando se espera actividad DAX** — Es posible que el flujo DAX no esté habilitado. Verifique que DAX esté iniciado; en las plataformas compatibles, revise `Settings > Autostart DAX with AetherSDR`.
- **El porcentaje de pérdida es distinto de cero en una sola categoría** — La pérdida está aislada a ese flujo. Esto puede indicar que la radio está sobrecargada para ese tipo de dato específico, o que una cola de red descarta preferentemente paquetes UDP de ese tamaño.

## Relacionado

- [Descripción general de Network Diagnostics](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
