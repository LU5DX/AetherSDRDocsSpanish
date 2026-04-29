# Reduzca el brillo agudo de la cola con Damp

El control **Damp** determina con qué rapidez se atenúan las frecuencias altas dentro de la cola de reverberación. Aumentarlo elimina el brillo aéreo y cristalino que puede hacer que la reverberación de voz suene artificial en el aire.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. Si no lo está, el applet Aetherial FreeVerb permanece oculto y Damp no tiene efecto.
- El applet Aetherial FreeVerb o su editor flotante debe estar visible. Consulte [Descripción general de Aetherial FreeVerb](overview.md) si aún no lo ha abierto.

## Pasos

1. Abra el editor de Aetherial FreeVerb haciendo doble clic en la etapa VERB en el widget CHAIN. Se abre la ventana sin marco titulada "Aetherial FreeVerb — TX".
2. Localice el control **Damp** — tercer control desde la izquierda en la fila de cinco controles.
3. Gire **Damp** en sentido horario para aumentar la amortiguación. Los valores más altos hacen que las frecuencias altas decaigan más rápido, reduciendo el brillo en la cola.
4. Gire **Damp** en sentido antihorario para que las frecuencias altas persistan más tiempo, produciendo una cola más brillante y abierta.
5. Suelte el control. El valor se guarda inmediatamente en `ClientReverbTxDamping`.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave persistida | Comportamiento |
|---------|----------------|-------|------------------|----------------|
| Damp | 50 % | 0 % – 100 % | `ClientReverbTxDamping` | Los valores más altos amortiguan las frecuencias altas más rápido en la cola de reverberación. Mapeo lineal. |

## Consejos

- Un valor alrededor de 50–70 % es adecuado para la mayoría de los trabajos con voz. Suaviza la cola sin que la reverberación suene apagada.
- Si la cola suena opaca o difusa, reduzca **Damp** hacia 20–30 % para permitir que pase más contenido de alta frecuencia.
- **Damp** interactúa con **Decay**: un decay largo con poca amortiguación produce una cola brillante y prolongada que puede enmascarar la voz. Aumente **Damp** si también aumenta Decay.

## Temas relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste el decay a su gusto sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Configure un Mix sutil — 10-15 % es lo habitual para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omita la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
