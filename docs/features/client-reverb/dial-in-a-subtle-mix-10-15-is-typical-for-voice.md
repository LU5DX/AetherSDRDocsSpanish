# Ajuste sutil de la Mezcla — 10–15 % es típico para voz

El control Mix regula el balance seco/húmedo de la reverberación Aetherial FreeVerb en su audio transmitido. Mantener Mix en el rango del 10–15 % añade una ligera sensación de espacio sin que su voz suene procesada o distante.

## Antes de empezar

- La etapa Reverb debe estar habilitada en el widget CHAIN. El subcontenedor "Aetherial FreeVerb" permanece oculto hasta que la etapa esté activa.
- Puede ajustar Mix desde la fila compacta de applets dentro del contenedor Aetherial Audio (TXDSP) o desde el editor flotante "Aetherial FreeVerb — TX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa VERB del widget CHAIN. Aparece el editor titulado "Aetherial FreeVerb — TX".
2. Localice el control Mix — es el quinto control de derecha a izquierda en la fila del editor.
3. Gire Mix hasta alcanzar el valor deseado. La etiqueta del control se actualiza en tiempo real, mostrada como porcentaje (por ejemplo, `15 %`).
4. Para voz, ajuste Mix entre 10 % y 15 %. Valores más bajos mezclan menos cola de reverberación; valores más altos hacen el efecto más prominente.
5. Cierre el editor o déjelo abierto. El valor se guarda inmediatamente.

## Función de cada control

| Etiqueta | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|----------|----------------------|--------------|------------------|----------------|
| Mix | 15 % | 0–100 % (0.0 a 1.0) | `ClientReverbTxMix` | Balance seco/húmedo lineal. Valores más altos aumentan la proporción de la cola de reverberación en la señal transmitida. |
| Size | 50 % | 0–100 % (0.0 a 1.0) | `ClientReverbTxSize` | Modela el tamaño de la sala. |
| Decay | 1.20 s | 0.3 a 5.0 s | `ClientReverbTxDecayS` | Ajusta la longitud de la cola de reverberación (mapeo exponencial). |
| Damp | 50 % | 0–100 % (0.0 a 1.0) | `ClientReverbTxDamping` | Valores más altos amortiguan más rápido las frecuencias altas en la cola. |
| Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Predelai entre la señal seca y las primeras reflexiones. |

## Visualización en vivo

La v0.9.7 añade una pequeña visualización de la reverberación dentro del editor "Aetherial FreeVerb — TX". Aparece como una pantalla de forma de onda de 90 píxeles de alto sobre la fila de controles y se actualiza en tiempo real conforme gira cualquier control.

La pantalla usa tres capas codificadas por color:

| Color | Qué representa |
|-------|----------------|
| Cian | Señal seca — un paquete sinusoidal que se desvanece hacia la derecha a medida que Mix aumenta. |
| Amarillo | Reflexiones de primer orden — ráfagas cortas cuyo espaciado se amplía con Size y cuya amplitud disminuye con Damp. |
| Magenta | Cola reverberante — una oscilación exponencialmente decreciente cuya longitud sigue a Decay y cuya posición de inicio sigue a Pre. |

La visualización es de solo lectura. No añade ni elimina ningún procesamiento; solo refleja los valores actuales de los controles. El algoritmo de diseño coincide con el panel de reverberación del lado de la tira, por lo que ambas vistas se leen de forma coherente cuando ambas están abiertas al mismo tiempo.

## Consejos

- El valor predeterminado de Mix es 15 %, que ya está dentro del rango típico para voz. Si restablece el control a su valor predeterminado, vuelve al 15 %.
- Tanto el control compacto del applet como el control del editor flotante se mantienen sincronizados. Los cambios realizados en uno se reflejan en el otro en aproximadamente 33 ms.
- Con Mix en 0 % solo pasa señal seca; la etapa de reverberación sigue activa pero es inaudible. Para eliminarla completamente de la cadena de procesamiento, consulte [Bypass reverb from the chain](bypass-reverb-from-the-chain.md).
- Use la visualización en vivo para obtener una lectura rápida de cómo interactúan Decay y Damp: una cola larga y brillante en la pantalla corresponde a una reverberación larga y rica en altas frecuencias en el audio transmitido.

## Relacionados

- [Aetherial FreeVerb overview](overview.md)
- [Bypass reverb from the chain](bypass-reverb-from-the-chain.md)
- [Tune decay to taste without muddying speech](tune-decay-to-taste-without-muddying-speech.md)
- [Reduce the high-end sparkle of the tail with Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Offset reflections from the dry signal with Pre](offset-reflections-from-the-dry-signal-with-pre.md)
