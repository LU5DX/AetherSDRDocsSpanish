# Ajuste el tiempo de decaimiento a su gusto sin enturbiar el audio de voz

El control **Decay** determina cuánto tiempo resuena la cola de reverberación tras cada sonido. Esta página explica cómo ajustarlo a un valor que aporte presencia sin deteriorar la inteligibilidad de la voz.

## Antes de comenzar

- La etapa de reverberación debe estar habilitada en el widget CHAIN. El subcontenedor REVERB permanece oculto hasta que la etapa esté activa.
- Abra el subcontenedor REVERB dentro del contenedor principal PooDoo Audio (TXDSP), o haga doble clic en la etapa Reverb en el widget CHAIN para abrir el editor flotante de Reverb.

## Pasos

1. Localice el control **Decay** en la fila REVERB de cinco mandos.
2. Arrastre el control hacia arriba para aumentar el tiempo de decaimiento, o hacia abajo para reducirlo. Mantenga presionado Shift mientras arrastra para un control más fino.
3. Observe la etiqueta debajo del control — muestra el valor actual en segundos, con el formato `X.XX s`.
4. Para voz, comience cerca del valor predeterminado de 1.20 s y redúzcalo hacia 0.3 s si las consonantes empiezan a difuminarse.
5. Si desea una cola más larga para lograr un efecto particular, aumente hacia 2.0–3.0 s y luego verifique la inteligibilidad en una grabación o en un monitor.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistente | Comportamiento |
|---------|----------------------|--------------|-------------------|----------------|
| Decay | 1.20 s | 0.3 a 5.0 s | `ClientReverbTxDecayS` | Establece la longitud de la cola de reverberación. Utiliza un mapeo exponencial a lo largo del recorrido del control (~16.7× de rango entre el mínimo y el máximo). |
| Damp | 50 % | 0.0 a 1.0 | `ClientReverbTxDamping` | Valores más altos atenúan las frecuencias altas más rápidamente en la cola, suavizando el carácter de los decaimientos largos. |
| Mix | 15 % | 0.0 a 1.0 | `ClientReverbTxMix` | Balance seco/húmedo. Un valor de Mix más bajo reduce la contribución de la cola a la señal transmitida. |

## Consejos

- Los tiempos de decaimiento cortos (0.3–0.8 s) funcionan mejor para SSB conversacional — la cola es audible pero se despeja antes de la siguiente sílaba.
- Si un Decay más largo sigue siendo inteligible pero suena áspero, aumente **Damp** para suavizar la energía de alta frecuencia en la cola sin acortarla.
- Reducir **Mix** es una alternativa a acortar el Decay — la longitud de la cola permanece igual, pero su nivel baja dentro de la señal general.
- El control utiliza un mapeo exponencial, por lo que la primera mitad del recorrido cubre de 0.3 a aproximadamente 1.2 s. La mayoría de los ajustes útiles para voz se encuentran en la mitad inferior del rango del control.

## Solución de problemas

- **Los cambios en Decay no tienen efecto audible** — confirme que la etapa Reverb esté habilitada y que **Mix** (`ClientReverbTxMix`) esté por encima de 0 %. Un Mix de 0 % pasa únicamente la señal seca, independientemente del valor de Decay.
- **La cola no se despeja entre palabras** — reduzca Decay hacia 0.3 s, o aumente **Damp** para acelerar el decaimiento de las frecuencias altas. Verifique también que **Pre** (`ClientReverbTxPreDelayMs`) no esté ajustado a un valor tan alto que las reflexiones persistan hasta la siguiente palabra.

## Temas relacionados

- [Reduzca el brillo de las frecuencias altas en la cola con Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Ajuste un Mix sutil — entre 10 y 15 % es lo habitual para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Desplace las reflexiones respecto a la señal seca con Pre](offset-reflections-from-the-dry-signal-with-pre.md)
- [Omita la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
