# Reduzca el brillo agudo de la cola con Damp

El control **Damp** regula la velocidad con la que las frecuencias altas se atenúan dentro de la cola de reverberación. Al aumentarlo, se elimina el brillo aéreo y brillante que puede hacer que la reverberación de voz suene poco natural en el aire.

## Antes de comenzar

- La etapa de reverberación debe estar habilitada en el widget CHAIN. Si no lo está, el applet Aetherial FreeVerb permanece oculto y Damp no tiene efecto.
- El applet Aetherial FreeVerb o su editor flotante deben estar visibles. Consulte [Descripción general de Aetherial FreeVerb](overview.md) si aún no lo ha abierto.

## Pasos

1. Abra el editor de Aetherial FreeVerb haciendo doble clic en la etapa VERB del widget CHAIN. Se abre la ventana sin marco titulada "Aetherial FreeVerb — TX".
2. Localice el control **Damp** — el tercer control desde la izquierda en la fila de cinco controles.
3. Gire **Damp** en sentido horario para aumentar el amortiguamiento. Los valores más altos hacen que las frecuencias altas decaigan más rápido, reduciendo el brillo en la cola.
4. Gire **Damp** en sentido antihorario para permitir que las frecuencias altas persistan más tiempo, generando una cola más brillante y abierta.
5. Suelte el control. El valor se guarda inmediatamente en `ClientReverbTxDamping`.

## Qué hace cada control

| Control | Valor predeterminado | Rango | Clave de persistencia | Comportamiento |
|---------|----------------------|-------|-----------------------|----------------|
| Damp | 50 % | 0 % – 100 % | `ClientReverbTxDamping` | Los valores más altos amortiguan las frecuencias altas más rápido en la cola de reverberación. Mapeo lineal. |

## Consejos

- Un valor alrededor de 50–70 % es adecuado para la mayoría del trabajo con voz. Suaviza la cola sin hacer que la reverberación suene apagada.
- Si la cola suena opaca o indefinida, reduzca **Damp** hacia 20–30 % para dejar pasar más contenido de alta frecuencia.
- **Damp** interactúa con **Decay**: un decaimiento largo con amortiguamiento bajo produce una cola brillante y prolongada que puede enmascarar la voz. Aumente **Damp** si también aumenta Decay.

## Temas relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste el decaimiento a su gusto sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Configure una mezcla sutil — 10–15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omita la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
