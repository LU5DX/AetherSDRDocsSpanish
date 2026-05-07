# Resumen de Aetherial FreeVerb

Aetherial FreeVerb agrega una cola de reverberación basada en Freeverb a su audio transmitido, dando a su voz una sensación de ambiente de sala o salón. Se aplica solo a la ruta de transmisión (TX); no tiene contraparte en recepción (RX).

## Antes de comenzar

- La etapa de reverberación debe estar habilitada en el widget CHAIN dentro del applet Aetherial Audio (TXDSP). El subcontenedor "Aetherial FreeVerb" y sus controles permanecen ocultos hasta que la etapa esté habilitada.
- No se requiere una conexión de radio para ajustar los parámetros de reverberación.

## Cómo funciona

Aetherial FreeVerb inserta un procesador de reverberación Freeverb en la cadena de audio TX del lado del cliente, después de cualquier etapa DSP previa. Cuando la etapa VERB está activa, los cinco potenciómetros — Size, Decay, Damp, Pre y Mix — dan forma al carácter y nivel de la cola de reverberación añadida a su voz transmitida.

Los controles aparecen en dos lugares que se mantienen sincronizados a aproximadamente 30 Hz:

- **El subcontenedor "Aetherial FreeVerb"** — una fila compacta de cinco potenciómetros incrustada dentro del contenedor principal Aetherial Audio (TXDSP) en el panel del applet.
- **El editor flotante titulado "Aetherial FreeVerb — TX"** — una versión más grande de los mismos controles, que se abre haciendo doble clic en la etapa VERB en el widget CHAIN. También puede hacer clic derecho en la barra de título del subcontenedor "Aetherial FreeVerb" para flotarlo, sacarlo u ocultarlo.

Girar cualquier potenciómetro en una vista actualiza inmediatamente la otra. La configuración se guarda automáticamente al cambiar un potenciómetro.

### Visualización de reverberación en vivo

El editor flotante incluye una visualización en vivo compacta (90 px de alto) que se actualiza en tiempo real mientras gira los potenciómetros. Muestra tres componentes de señal sobre un fondo de cuadrícula oscura:

- **Cian** — el paquete de señal seca, con degradado desvaneciéndose hacia la derecha.
- **Amarillo** — reflexiones de primer orden, espaciadas y amortiguadas según los valores actuales de Size y Damp.
- **Magenta** — la cola reverberante, cuya longitud y envolvente de caída siguen los potenciómetros Decay y Damp.

El potenciómetro Pre desplaza el punto donde comienzan las reflexiones y la cola en relación con la señal seca. El potenciómetro Mix escala la amplitud tanto de los componentes húmedos como del desvanecimiento del paquete seco. La visualización coincide con el diseño utilizado por el panel de reverberación lateral de la tira, por lo que las dos vistas se leen de manera coherente.

## Qué hace cada control

| Potenciómetro | Valor predeterminado | Rango válido | Comportamiento | Clave de configuración |
|---------------|----------------------|---------------|----------------|-------------------------|
| Size | 50 % | 0–100 % | Establece el tamaño simulado de la sala. Mapeo lineal. | `ClientReverbTxSize` |
| Decay | 1.20 s | 0.3–5.0 s | Establece la longitud de la cola de reverberación. Mapeo exponencial — el potenciómetro va de 0.3 s a 5.0 s con un control más fino en valores cortos. | `ClientReverbTxDecayS` |
| Damp | 50 % | 0–100 % | Valores más altos amortiguan las frecuencias altas más rápido en la cola, produciendo una reverberación más cálida y menos brillante. Mapeo lineal. | `ClientReverbTxDamping` |
| Pre | 20 ms | 0–100 ms | Establece el pre-retardo entre la señal seca y las primeras reflexiones. Mapeo lineal. | `ClientReverbTxPreDelayMs` |
| Mix | 15 % | 0–100 % | Establece el balance seco/húmedo. 0 % es completamente seco; 100 % es completamente húmedo. Mapeo lineal. | `ClientReverbTxMix` |

El estado habilitado/deshabilitado de la etapa se guarda como `ClientReverbTxEnabled`.

## Consejos

- Para voz, un Mix del 10–15 % es típico. El valor predeterminado del 15 % es un punto de partida razonable.
- Los valores altos de Decay (por encima de 3 s) pueden enturbiar el habla. Comience con el valor predeterminado de 1.20 s y aumente solo si el efecto de sala parece demasiado corto.
- Aumentar Damp reduce el brillo de las frecuencias altas en la cola, lo que puede ayudar a que la reverberación se sitúe detrás del habla en lugar de superponerse a ella.
- El editor flotante ("Aetherial FreeVerb — TX") proporciona potenciómetros más grandes y la visualización en vivo para un ajuste preciso. Su posición y tamaño se guardan automáticamente entre sesiones.
- Use la visualización en vivo para obtener una idea aproximada de la longitud de la cola y la densidad de reflexiones antes de transmitir. La longitud de la cola magenta brinda una aproximación visual de cómo interactúan Decay y Damp.

## Relacionados

- [Bypass reverb from the chain](bypass-reverb-from-the-chain.md)
- [Dial in a subtle Mix — 10-15 % is typical for voice](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Tune decay to taste without muddying speech](tune-decay-to-taste-without-muddying-speech.md)
- [Reduce the high-end sparkle of the tail with Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Set room size for a small or large-hall feel](set-room-size-for-a-small-or-large-hall-feel.md)
- [Offset reflections from the dry signal with Pre](offset-reflections-from-the-dry-signal-with-pre.md)
