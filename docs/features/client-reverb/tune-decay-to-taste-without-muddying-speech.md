# Ajuste el decay a su gusto sin enturbiar la voz

El control **Decay** determina cuánto tiempo resuena la cola de reverberación tras cada sílaba. Un valor demasiado alto emborrana la voz; esta página muestra cómo encontrar un valor que añada presencia sin afectar la inteligibilidad.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. El subcontenedor "Aetherial FreeVerb" permanece oculto hasta que la etapa esté activa.
- Abra los controles de reverberación: ubique el subcontenedor "Aetherial FreeVerb" dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets, o haga doble clic en la etapa VERB del widget CHAIN para abrir el editor flotante titulado "Aetherial FreeVerb — TX".

## Pasos

1. Localice el control **Decay**. Muestra un valor con el formato `X.XX s`.
2. Gire **Decay** hacia abajo hasta `0.30 s` y transmita una muestra de voz. En este extremo, la cola apenas es audible.
3. Aumente **Decay** lentamente mientras habla o monitorea una grabación. Deténgase cuando la cola se vuelva audible entre sílabas.
4. Retroceda ligeramente hasta que las sílabas dejen de mezclarse entre sí. Para la mayoría del trabajo de voz, valores entre `0.5 s` y `1.5 s` mantienen la voz clara.
5. Si la cola aún suena turbia, aumente **Damp** para atenuar la energía de alta frecuencia en la cola; esto suele reducir la percepción de emborronamiento sin necesidad de acortar más el Decay.
6. Verifique que **Mix** no esté demasiado alto. Un Mix de `10 %` a `15 %` es típico para voz; un exceso de señal wet amplifica el efecto de cualquier valor de Decay.

## Qué hace cada control

| Etiqueta | Valor predeterminado | Rango | Clave persistida | Comportamiento |
|----------|----------------------|-------|------------------|----------------|
| Decay | 1.20 s | 0.3 a 5.0 s | `ClientReverbTxDecayS` | Establece la longitud de la cola de reverberación. Utiliza mapeo exponencial en su rango (~16.7× de mínimo a máximo). |
| Damp | 50 % | 0.0 a 1.0 (mostrado como %) | `ClientReverbTxDamping` | Valores más altos hacen que las frecuencias altas decaigan más rápido en la cola, reduciendo el brillo y el emborronamiento percibido. |
| Mix | 15 % | 0.0 a 1.0 (mostrado como %) | `ClientReverbTxMix` | Balance seco/wet. Un valor de Mix alto amplifica el impacto audible de todos los demás parámetros. |

## Consejos

- Como Decay usa un mapeo exponencial, el control es mucho más sensible en la parte baja de su recorrido. Realice ajustes pequeños cuando trabaje por debajo de `1.0 s`.
- Los controles del applet y el editor flotante "Aetherial FreeVerb — TX" se mantienen sincronizados a aproximadamente 30 Hz. Los ajustes realizados en uno se reflejan inmediatamente en el otro.
- Haga doble clic en el control **Decay** para restablecerlo al valor predeterminado de `1.20 s`.

## Solución de problemas

- **La voz suena apagada incluso con valores cortos de Decay** — Verifique **Mix**. Si Mix supera `30 %`, la señal wet domina independientemente de la longitud de la cola. Reduzca Mix a `10–15 %` primero y luego reevalúe Decay.
- **El control Decay no produce ningún efecto audible** — Es posible que la etapa Reverb no esté habilitada. Confirme que la etapa VERB esté activa en el widget CHAIN. El applet está oculto y el procesador se omite cuando la etapa está desactivada.

## Relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Reduzca el brillo en las frecuencias altas de la cola con Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Configure un Mix sutil — 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omita la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
