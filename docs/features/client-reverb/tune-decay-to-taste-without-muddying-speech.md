# Ajuste la decadencia a su gusto sin enturbiar la voz

El mando Decay controla cuánto tiempo resuena la cola de reverberación tras cada sílaba. Un valor demasiado alto difumina el habla; esta página muestra cómo encontrar un valor que añada presencia sin deteriorar la inteligibilidad.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. El subcontenedor "Aetherial FreeVerb" permanece oculto hasta que la etapa esté activa.
- Abra los controles de reverberación: localice el subcontenedor "Aetherial FreeVerb" dentro del contenedor padre Aetherial Audio (TXDSP) en el panel de applets, o haga doble clic en la etapa VERB del widget CHAIN para abrir el editor flotante titulado "Aetherial FreeVerb — TX".

## Pasos

1. Localice el mando **Decay**. Muestra un valor con el formato `X.XX s`.
2. Gire **Decay** hacia `0.30 s` y transmita una muestra de voz. En este extremo, la cola apenas es audible.
3. Aumente **Decay** lentamente mientras habla o monitorea una grabación. Detenga el ajuste cuando la cola sea audible entre sílabas.
4. Retroceda ligeramente hasta que las sílabas dejen de fusionarse entre sí. Para la mayoría del trabajo de voz, valores en el rango de `0.5 s` a `1.5 s` mantienen la voz clara.
5. Si la cola aún suena turbia, aumente **Damp** para atenuar la energía de alta frecuencia en la cola, lo que generalmente reduce la percepción de difuminado sin acortar aún más Decay.
6. Verifique que **Mix** no esté configurado demasiado alto. Un Mix de `10 %` a `15 %` es típico para voz; un exceso de señal húmeda amplifica el efecto de cualquier valor de Decay.

## Qué hace cada control

| Etiqueta | Valor predeterminado | Rango | Clave persistida | Comportamiento |
|----------|----------------------|-------|------------------|----------------|
| Decay | 1.20 s | 0.3 a 5.0 s | `ClientReverbTxDecayS` | Establece la longitud de la cola de reverberación. Utiliza mapeo exponencial en todo su rango (~16.7× del mínimo al máximo). |
| Damp | 50 % | 0.0 a 1.0 (mostrado en %) | `ClientReverbTxDamping` | Valores más altos hacen que las frecuencias altas decaigan más rápido en la cola, reduciendo el brillo y el difuminado percibido. |
| Mix | 15 % | 0.0 a 1.0 (mostrado en %) | `ClientReverbTxMix` | Balance seco/húmedo. Un valor de Mix alto amplifica el impacto audible de todos los demás parámetros. |

## Consejos

- Dado que Decay usa mapeo exponencial, el mando es mucho más sensible en el extremo inferior de su recorrido. Realice ajustes pequeños cuando trabaje por debajo de `1.0 s`.
- Los mandos del applet y el editor flotante "Aetherial FreeVerb — TX" se mantienen sincronizados a aproximadamente 30 Hz. Los ajustes realizados en uno se reflejan inmediatamente en el otro.
- Haga doble clic en el mando **Decay** para restablecerlo al valor predeterminado de `1.20 s`.

## Solución de problemas

- **La voz suena difuminada incluso con valores cortos de Decay** — Verifique **Mix**. Si Mix supera `30 %`, la señal húmeda domina independientemente de la longitud de la cola. Reduzca Mix a `10–15 %` primero y luego vuelva a evaluar Decay.
- **El mando Decay no tiene efecto audible** — Es posible que la etapa Reverb no esté habilitada. Confirme que la etapa VERB está activa en el widget CHAIN. El applet está oculto y el procesador queda omitido cuando la etapa está desactivada.

## Relacionado

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Reduzca el brillo de alta frecuencia de la cola con Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Configure un Mix sutil — 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omita la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
