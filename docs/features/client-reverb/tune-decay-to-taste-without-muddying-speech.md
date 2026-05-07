# Ajuste la caída al gusto sin ensuciar la voz

El mando **Decay** controla cuánto tiempo persiste la cola de la reverberación después de cada sílaba. Un valor demasiado alto emborrona el habla; esta página muestra cómo encontrar un valor que añada presencia sin perjudicar la inteligibilidad.

## Antes de empezar

- La etapa Reverb debe estar habilitada en el widget CHAIN. El subcontenedor "Aetherial FreeVerb" permanece oculto hasta que la etapa esté activa.
- Abra los controles de reverberación: localice el subcontenedor "Aetherial FreeVerb" dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets, o haga doble clic en la etapa VERB en el widget CHAIN para abrir el editor flotante titulado "Aetherial FreeVerb — TX".

## Pasos

1. Localice el mando **Decay**. Muestra un valor en el formato `X,XX s`.
2. Gire **Decay** hacia abajo hasta `0,30 s` y transmita una muestra de voz. En este extremo, la cola es apenas audible.
3. Aumente **Decay** lentamente mientras habla o monitorea una grabación. Deténgase cuando la cola se vuelva audible entre las sílabas.
4. Reduzca ligeramente hasta que las sílabas ya no se difuminen entre sí. Para la mayoría de los trabajos de voz, los valores en el rango de `0,5 s` a `1,5 s` mantienen el habla clara.
5. Si la cola aún suena turbia, aumente **Damp** para atenuar la energía de alta frecuencia en la cola, lo que a menudo reduce la percepción de emborronamiento sin acortar más **Decay**.
6. Verifique que **Mix** no esté demasiado alto. Un Mix de `10 %` a `15 %` es típico para voz; un exceso de señal húmeda amplifica el efecto de cualquier valor de **Decay**.

## Qué hace cada control

| Etiqueta | Valor predeterminado | Rango | Clave persistida | Comportamiento |
|----------|----------------------|-------|------------------|----------------|
| Size | 50 % | 0,0 a 1,0 (mostrado como %) | `ClientReverbTxSize` | Define el tamaño de la sala modelada. Usa mapeo lineal. |
| Decay | 1,20 s | 0,3 a 5,0 s | `ClientReverbTxDecayS` | Define la longitud de la cola de reverberación. Usa mapeo exponencial en todo su rango (~16,7× desde el mínimo hasta el máximo). |
| Damp | 50 % | 0,0 a 1,0 (mostrado como %) | `ClientReverbTxDamping` | Los valores más altos hacen que las altas frecuencias decaigan más rápido en la cola, reduciendo el brillo y el emborronamiento percibido. |
| Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Predelay entre la señal seca y las primeras reflexiones. Usa mapeo lineal. La etiqueta muestra `X ms`. |
| Mix | 15 % | 0,0 a 1,0 (mostrado como %) | `ClientReverbTxMix` | Balance seco/húmedo. Un valor alto de Mix amplifica el impacto audible de todos los demás parámetros. |

## Visualización en vivo

A partir de v0.9.7, el panel de applets y el editor flotante "Aetherial FreeVerb — TX" muestran un diagrama de forma de onda compacto (90 px de alto) que se actualiza en tiempo real al mover cualquier mando. El diagrama utiliza tres capas codificadas por colores:

- **Cian** — el paquete de señal seca, con degradado hacia la derecha. Su amplitud disminuye a medida que aumenta **Mix**.
- **Amarillo** — reflexiones de primer orden. El espaciado y la cantidad responden a **Size**; la amplitud por reflexión disminuye con valores más altos de **Damp**.
- **Magenta** — la cola reverberante. Su longitud horizontal refleja **Decay**, su atenuación de alta frecuencia refleja **Damp**, y su amplitud general refleja **Mix**.

La visualización es solo orientativa; no representa una medición precisa de respuesta al impulso. Use sus oídos para realizar los ajustes finales.

## Consejos

- Debido a que **Decay** usa un mapeo exponencial, el mando es mucho más sensible en el extremo inferior de su recorrido. Realice pequeños ajustes cuando trabaje por debajo de `1,0 s`.
- Los mandos del applet y el editor flotante "Aetherial FreeVerb — TX" se mantienen sincronizados a aproximadamente 30 Hz. Los ajustes realizados en uno se reflejan inmediatamente en el otro.
- Haga doble clic en el mando **Decay** para restablecerlo al valor predeterminado de `1,20 s`.

## Solución de problemas

- **El habla suena lavada incluso con valores cortos de Decay** — Revise **Mix**. Si **Mix** supera el `30 %`, la señal húmeda domina independientemente de la longitud de la cola. Reduzca **Mix** primero a `10–15 %` y luego reevalúe **Decay**.
- **El mando Decay no tiene efecto audible** — La etapa Reverb puede no estar habilitada. Confirme que la etapa VERB esté activa en el widget CHAIN. El applet está oculto y el procesador está en bypass cuando la etapa está desactivada.

## Relacionados

- [Aetherial FreeVerb overview](overview.md)
- [Reduce the high-end sparkle of the tail with Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Dial in a subtle Mix — 10-15 % is typical for voice](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Bypass reverb from the chain](bypass-reverb-from-the-chain.md)
