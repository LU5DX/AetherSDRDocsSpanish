# Verificar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)

El diálogo Network Diagnostics muestra las tasas de entrada en tiempo real para cada categoría de flujo — Audio, FFT, Waterfall, Meters y DAX — actualizado una vez por segundo. Úselo para identificar qué tipo de flujo está consumiendo ancho de banda o no está recibiendo datos durante problemas de recepción.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo se abre independientemente de si hay una radio conectada, pero las tasas mostrarán 0 kbps hasta que se establezca una conexión.

## Pasos

1. Haga clic en `Settings > Network...`.
2. Localice el grupo **Incoming Stream Rates** en el lado derecho del diálogo.
3. Lea los valores por categoría: **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX** muestran cada uno la tasa actual en kbps, actualizada cada segundo.
4. Para verificar cuántos paquetes se perdieron en cada categoría, localice el grupo **Packet Loss (Sequence Gaps)** en la parte inferior izquierda. Muestra los conteos de pérdida de **Audio**, **FFT**, **Waterfall**, **Meters** y **DAX** en el formato `errors / total packets (%)`.
5. Al terminar, haga clic en Close.

## Qué hace cada control

| Indicador | Ubicación | Significado |
|---|---|---|
| **Audio** (tasa) | Incoming Stream Rates | Tasa de entrada del flujo de audio de recepción, en kbps. |
| **FFT** (tasa) | Incoming Stream Rates | Tasa de entrada de los datos FFT del panadapter, en kbps. |
| **Waterfall** (tasa) | Incoming Stream Rates | Tasa de entrada de los datos de teselas del waterfall, en kbps. |
| **Meters** (tasa) | Incoming Stream Rates | Tasa de entrada de los datos de medidores, en kbps. |
| **DAX** (tasa) | Incoming Stream Rates | Tasa de entrada de los flujos de audio DAX, en kbps. |
| **Total RX** | Incoming Stream Rates | Tasa de entrada agregada de todos los flujos, en kbps. |
| **Total TX** | Incoming Stream Rates | Tasa de salida agregada, en kbps. |
| **Audio** (pérdidas) | Packet Loss (Sequence Gaps) | Errores de paquetes de audio frente al total de paquetes recibidos, con porcentaje. |
| **FFT** (pérdidas) | Packet Loss (Sequence Gaps) | Errores de paquetes FFT frente al total de paquetes recibidos, con porcentaje. |
| **Waterfall** (pérdidas) | Packet Loss (Sequence Gaps) | Errores de paquetes de waterfall frente al total de paquetes recibidos, con porcentaje. |
| **Meters** (pérdidas) | Packet Loss (Sequence Gaps) | Errores de paquetes de medidores frente al total de paquetes recibidos, con porcentaje. |
| **DAX** (pérdidas) | Packet Loss (Sequence Gaps) | Errores de paquetes DAX frente al total de paquetes recibidos, con porcentaje. |

Las tasas se expresan en kbps y se recalculan a partir de las diferencias de conteo de bytes cada segundo. Los conteos de pérdida se deducen a partir de los números de secuencia VITA-49 faltantes.

## Consejos

- Una categoría que muestra 0 kbps mientras la radio está conectada y ese flujo debería estar activo indica un problema de configuración o enrutamiento en ese flujo específico, no un fallo general de red.
- Grandes variaciones en la tasa de una categoría de segundo a segundo pueden indicar entrega irregular incluso cuando el conteo de pérdidas es cero. Verifique las tasas de **Waterfall** y **FFT** juntas: si el waterfall es irregular pero el FFT es estable, el problema probablemente se debe a la programación de teselas del waterfall y no a la ruta de red.
- El porcentaje de pérdida solo es significativo una vez que el **total de paquetes** sea distinto de cero. Un valor de `0 / 0` significa que aún no se han recibido paquetes para esa categoría.

## Solución de problemas

- **Todas las tasas muestran 0 kbps** — La radio no está conectada o no se han iniciado flujos. Confirme el estado de la conexión en el grupo **Network Status**: **Target Radio IP** debe mostrar una dirección IP, no "Not connected".
- **La tasa de DAX muestra 0 kbps pero otros flujos están activos** — Es posible que el puente de audio DAX no esté habilitado. Verifique `Settings > Autostart DAX with AetherSDR` o inicie DAX manualmente desde el panel de applets.
- **El conteo de pérdidas sube en una categoría mientras las demás permanecen en cero** — La pérdida es específica de ese tipo de flujo. Esto puede indicar que la radio está enviando más datos de los que la ruta de red puede sostener para ese flujo en particular; intente reducir la tasa de actualización del FFT o del waterfall en la configuración de la radio.

## Relacionado

- [Descripción general de Network Diagnostics](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
