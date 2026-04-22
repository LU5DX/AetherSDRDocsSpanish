# Descripción general de Reverb

El applet Reverb añade una cola de reverberación basada en Freeverb al audio que usted transmite. Úselo para agregar una sutil ambientación de sala o recinto a las transmisiones de voz antes de que la señal salga del cliente.

## Antes de comenzar

- La etapa Reverb debe habilitarse mediante el widget CHAIN o el editor flotante de Reverb antes de que aparezca el applet. El applet permanece oculto hasta que la etapa esté activa.
- Reverb es un efecto TX del lado del cliente. Procesa el audio en su computadora, no en el radio.

## Cómo funciona

El applet Reverb aparece como un subcontenedor con la etiqueta **REVERB** dentro del contenedor principal PooDoo Audio (TXDSP). Presenta una fila compacta de cinco mandos — **Size**, **Decay**, **Damp**, **Pre** y **Mix** — que en conjunto dan forma al carácter de la cola de reverberación aplicada a su audio saliente.

Los valores de los mandos se sincronizan con el editor flotante de Reverb a aproximadamente 30 Hz. Los cambios realizados en el applet o en el editor flotante se reflejan en ambos lugares de forma inmediata.

Para abrir el editor flotante de Reverb, haga doble clic en la etapa Reverb dentro del widget CHAIN. Para flotar, desprender u ocultar el subcontenedor **REVERB**, haga clic derecho en su barra de título.

No se requiere conexión con el radio para ajustar los parámetros de Reverb.

## Qué hace cada control

| Mando | Valor predeterminado | Rango válido | Configuración persistida | Comportamiento |
|-------|----------------------|--------------|--------------------------|----------------|
| **Size** | 50 % | 0 – 100 % | `ClientReverbTxSize` | Define el tamaño del recinto modelado. Mapeo lineal. |
| **Decay** | 1.20 s | 0.3 – 5.0 s | `ClientReverbTxDecayS` | Define la longitud de la cola de reverberación. Mapeo exponencial; incrementos pequeños en el extremo inferior tienen más efecto que el mismo movimiento en el extremo superior. |
| **Damp** | 50 % | 0 – 100 % | `ClientReverbTxDamping` | Controla la rapidez con que las frecuencias altas se atenúan en la cola. Valores más altos atenúan las frecuencias altas con mayor velocidad, produciendo una reverberación más cálida y oscura. Mapeo lineal. |
| **Pre** | 20 ms | 0 – 100 ms | `ClientReverbTxPreDelayMs` | Define el predelay entre la señal seca y las primeras reflexiones. Mapeo lineal. |
| **Mix** | 15 % | 0 – 100 % | `ClientReverbTxMix` | Define el balance seco/húmedo. Mapeo lineal. |

El estado habilitado/deshabilitado de la etapa de reverberación se persiste en `ClientReverbTxEnabled`.

## Consejos

- Un Mix de 10–15 % es típico para voz. Valores más altos se vuelven perceptibles rápidamente y pueden deteriorar la inteligibilidad del habla.
- Valores cortos de Decay (0.3–0.8 s) con un Size pequeño producen un efecto de sala reducida. Valores más largos de Decay con un Size grande aproximan un recinto de tipo sala de conciertos.
- Aumentar Damp puede ayudar a suavizar la dureza en la cola de reverberación sin necesidad de reducir el Mix.

## Relacionados

- [Omitir la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
- [Ajustar un Mix sutil — 10–15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Separar las reflexiones de la señal seca con Pre](offset-reflections-from-the-dry-signal-with-pre.md)
- [Reducir el brillo en las frecuencias altas de la cola con Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Definir el tamaño del recinto para una sensación de sala pequeña o grande](set-room-size-for-a-small-or-large-hall-feel.md)
- [Ajustar el Decay al gusto sin ensuciar el habla](tune-decay-to-taste-without-muddying-speech.md)
