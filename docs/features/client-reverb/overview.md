# Descripción general de Aetherial FreeVerb

Aetherial FreeVerb añade una cola de reverberación basada en Freeverb al audio que usted transmite, dándole a su voz una sensación de ambiente de sala o de salón. Se aplica únicamente a la cadena TX — no existe una contraparte RX.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN dentro del applet Aetherial Audio (TXDSP). El sub-contenedor "Aetherial FreeVerb" y sus controles permanecen ocultos hasta que la etapa esté habilitada.
- No se requiere conexión a una radio para ajustar los parámetros de reverberación.

## Cómo funciona

Aetherial FreeVerb inserta un procesador de reverberación Freeverb en la cadena de audio TX del lado del cliente, después de cualquier etapa DSP anterior. Cuando la etapa VERB está activa, los cinco controles giratorios — Size, Decay, Damp, Pre y Mix — dan forma al carácter y al nivel de la cola de reverberación añadida a su voz transmitida.

Los controles aparecen en dos lugares que permanecen sincronizados a aproximadamente 30 Hz:

- **El sub-contenedor "Aetherial FreeVerb"** — una fila compacta de cinco controles giratorios integrada dentro del contenedor principal Aetherial Audio (TXDSP) en el panel del applet.
- **El editor flotante titulado "Aetherial FreeVerb — TX"** — una versión ampliada de los mismos controles, que se abre haciendo doble clic en la etapa VERB del widget CHAIN. También puede hacer clic derecho en la barra de título del sub-contenedor "Aetherial FreeVerb" para hacerlo flotar, separarlo u ocultarlo.

Girar cualquier control en cualquiera de las dos vistas actualiza inmediatamente la otra. Los ajustes se guardan automáticamente al modificar un control.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento | Clave de ajuste |
|---------|----------------------|--------------|----------------|-----------------|
| Size | 50 % | 0–100 % | Establece el tamaño de sala modelado. Mapeo lineal. | `ClientReverbTxSize` |
| Decay | 1.20 s | 0.3–5.0 s | Establece la longitud de la cola de reverberación. Mapeo exponencial — el control recorre de 0.3 s a 5.0 s con mayor precisión en los valores más cortos. | `ClientReverbTxDecayS` |
| Damp | 50 % | 0–100 % | Los valores más altos atenúan las frecuencias agudas más rápidamente en la cola, produciendo una reverberación más cálida y menos brillante. Mapeo lineal. | `ClientReverbTxDamping` |
| Pre | 20 ms | 0–100 ms | Establece la pre-demora entre la señal seca y las primeras reflexiones. Mapeo lineal. | `ClientReverbTxPreDelayMs` |
| Mix | 15 % | 0–100 % | Establece el balance seco/húmedo. 0 % es completamente seco; 100 % es completamente húmedo. Mapeo lineal. | `ClientReverbTxMix` |

El estado habilitado/deshabilitado de la etapa se guarda como `ClientReverbTxEnabled`.

## Consejos

- Para voz, un valor de Mix entre 10–15 % es lo habitual. El valor predeterminado de 15 % es un buen punto de partida.
- Los valores altos de Decay (por encima de 3 s) pueden enlodar el habla. Comience con el valor predeterminado de 1.20 s y auméntelo solo si el efecto de sala suena demasiado corto.
- Aumentar Damp reduce el brillo de las frecuencias altas en la cola, lo que puede ayudar a que la reverberación quede detrás del habla en lugar de encima de ella.
- El editor flotante ("Aetherial FreeVerb — TX") ofrece controles giratorios más grandes para un ajuste preciso. Su posición y tamaño se guardan automáticamente entre sesiones.

## Temas relacionados

- [Omitir la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
- [Ajustar un Mix sutil — entre 10–15 % es lo habitual para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Afinar el Decay al gusto sin enlodar el habla](tune-decay-to-taste-without-muddying-speech.md)
- [Reducir el brillo de las frecuencias altas de la cola con Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Establecer el tamaño de sala para un ambiente de sala pequeña o grande](set-room-size-for-a-small-or-large-hall-feel.md)
- [Desfasar las reflexiones respecto a la señal seca con Pre](offset-reflections-from-the-dry-signal-with-pre.md)
