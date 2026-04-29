# Descripción general de Aetherial FreeVerb

Aetherial FreeVerb añade una cola de reverberación basada en Freeverb al audio que usted transmite, dando a su voz una sensación de ambiente de sala o auditorio. Se aplica únicamente a la cadena de TX — no existe contraparte en RX.

## Antes de comenzar

- El bloque Reverb debe estar habilitado en el widget CHAIN dentro del applet Aetherial Audio (TXDSP). El sub-contenedor "Aetherial FreeVerb" y sus controles permanecen ocultos hasta que el bloque esté habilitado.
- No se requiere conexión a una radio para ajustar la configuración de reverberación.

## Cómo funciona

Aetherial FreeVerb inserta un procesador de reverberación Freeverb en la cadena de audio TX del lado del cliente, después de cualquier bloque DSP previo. Cuando el bloque VERB está activo, los cinco mandos — Size, Decay, Damp, Pre y Mix — determinan el carácter y el nivel de la cola de reverberación añadida a su voz transmitida.

Los controles aparecen en dos lugares que permanecen sincronizados a aproximadamente 30 Hz:

- **El sub-contenedor "Aetherial FreeVerb"** — una fila compacta de cinco mandos integrada dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
- **El editor flotante titulado "Aetherial FreeVerb — TX"** — una versión ampliada de los mismos controles, que se abre haciendo doble clic en el bloque VERB en el widget CHAIN. También puede hacer clic derecho en la barra de título del sub-contenedor "Aetherial FreeVerb" para flotarlo, extraerlo o ocultarlo.

Girar cualquier mando en cualquiera de las dos vistas actualiza inmediatamente la otra. La configuración se guarda automáticamente al modificar un mando.

## Qué hace cada control

| Mando | Valor por defecto | Rango válido | Comportamiento | Clave de ajuste |
|-------|-------------------|--------------|----------------|-----------------|
| Size | 50 % | 0–100 % | Define el tamaño de sala modelado. Mapeo lineal. | `ClientReverbTxSize` |
| Decay | 1.20 s | 0.3–5.0 s | Define la longitud de la cola de reverberación. Mapeo exponencial — el mando recorre de 0.3 s a 5.0 s con mayor precisión en valores cortos. | `ClientReverbTxDecayS` |
| Damp | 50 % | 0–100 % | Valores más altos atenúan las frecuencias agudas con mayor rapidez en la cola, produciendo una reverberación más cálida y menos brillante. Mapeo lineal. | `ClientReverbTxDamping` |
| Pre | 20 ms | 0–100 ms | Define el pre-retardo entre la señal seca y las primeras reflexiones. Mapeo lineal. | `ClientReverbTxPreDelayMs` |
| Mix | 15 % | 0–100 % | Define el balance seco/húmedo. 0 % es completamente seco; 100 % es completamente húmedo. Mapeo lineal. | `ClientReverbTxMix` |

El estado habilitado/deshabilitado del bloque se guarda como `ClientReverbTxEnabled`.

## Consejos

- Para voz, un Mix de 10–15 % es típico. El valor por defecto de 15 % es un buen punto de partida.
- Valores altos de Decay (por encima de 3 s) pueden enturbian el habla. Comience con el valor por defecto de 1.20 s y auméntelo solo si el efecto de sala suena demasiado corto.
- Aumentar Damp reduce el brillo de altas frecuencias en la cola, lo que puede ayudar a que la reverberación quede detrás de la voz en lugar de encima de ella.
- El editor flotante ("Aetherial FreeVerb — TX") ofrece mandos más grandes para ajustes precisos. Su posición y tamaño se guardan automáticamente entre sesiones.

## Relacionados

- [Omitir la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
- [Ajustar un Mix sutil — 10–15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Ajustar el Decay a gusto sin enturbiar el habla](tune-decay-to-taste-without-muddying-speech.md)
- [Reducir el brillo de altas frecuencias en la cola con Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Establecer el tamaño de sala para sensación de sala pequeña o gran auditorio](set-room-size-for-a-small-or-large-hall-feel.md)
- [Desfasar las reflexiones de la señal seca con Pre](offset-reflections-from-the-dry-signal-with-pre.md)
