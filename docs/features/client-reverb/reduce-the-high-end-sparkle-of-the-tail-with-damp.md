# Reduzca el brillo excesivo de la cola con Damp

El control **Damp** determina con qué rapidez se atenúan las frecuencias altas en la cola de reverberación. Al aumentarlo se elimina la calidad brillante y aérea de las decaídas largas — útil cuando la reverberación suena demasiado metálica o dura en voz.

## Antes de comenzar

- El applet Reverb debe estar visible. Permanece oculto hasta que la etapa Reverb se habilita mediante el widget CHAIN o el editor flotante Reverb. Consulte [Omitir la reverberación desde la cadena](bypass-reverb-from-the-chain.md) si necesita habilitar la etapa primero.
- El contenedor principal TXDSP (PooDoo Audio) debe estar abierto en el panel de applets para que el subcontenedor REVERB sea accesible.

## Pasos

1. Localice el subcontenedor **REVERB** dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. Encuentre el control **Damp** — el tercer control de la fila de cinco (Size, Decay, Damp, Pre, Mix).
3. Arrastre el control **Damp** hacia arriba para aumentar el amortiguamiento. La etiqueta muestra el valor actual como porcentaje.
4. Transmita y escuche. Los valores más altos hacen que las frecuencias altas de la cola decaigan más rápido, produciendo una reverberación más cálida y oscura.
5. Ajuste hasta que la cola se mezcle naturalmente con su voz sin sonar apagada.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Configuración persistida | Comportamiento |
|---------|---------------|--------------|--------------------------|----------------|
| Damp | 50 % | 0 % a 100 % | `ClientReverbTxDamping` | Lineal. Los valores más altos amortiguan las frecuencias altas más rápido en la cola de reverberación. El 0 % deja la cola sin filtrar; el 100 % suprime fuertemente el contenido de alta frecuencia a lo largo de toda la cola. |

## Consejos

- Comience con el valor predeterminado de 50 % y auméntelo en incrementos pequeños. Para la mayoría del trabajo de voz, los valores entre 50–70 % eliminan la dureza sin que la cola suene turbia.
- Si la cola todavía suena demasiado brillante después de aumentar Damp, acorte también Decay. Ambos controles funcionan en conjunto: un Decay largo con Damp bajo produce la mayor energía en frecuencias altas a lo largo del tiempo.
- Haga doble clic en el control **Damp** para restablecerlo a su valor predeterminado de 50 %.

## Relacionados

- [Ajuste la decaída a su gusto sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Configure el tamaño de sala para una sensación de sala pequeña o grande](set-room-size-for-a-small-or-large-hall-feel.md)
- [Establezca una mezcla sutil — 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omitir la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
