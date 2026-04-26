# Ajuste un Mix sutil — el 10-15 % es típico para voz

El control Mix regula el balance seco/húmedo del reverb Aetherial FreeVerb en el audio que transmite. Mantener Mix en el rango del 10–15 % agrega una ligera sensación de espacio sin hacer que su voz suene procesada o distante.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. El subcontenedor "Aetherial FreeVerb" permanece oculto hasta que la etapa esté activa.
- Puede ajustar Mix desde la fila compacta del applet dentro del contenedor Aetherial Audio (TXDSP) o desde el editor flotante "Aetherial FreeVerb — TX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa VERB en el widget CHAIN. Aparece el editor titulado "Aetherial FreeVerb — TX".
2. Localice el control Mix — el más a la derecha de los cinco controles en la fila del editor.
3. Gire Mix hasta el valor deseado. La etiqueta del control se actualiza en tiempo real y se muestra como porcentaje (por ejemplo, `15 %`).
4. Para voz, configure Mix entre el 10 % y el 15 %. Los valores más bajos mezclan menos cola de reverb; los valores más altos hacen el efecto más prominente.
5. Cierre el editor o déjelo abierto. El valor se guarda de inmediato.

## Qué hace cada control

| Etiqueta | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|----------|----------------------|--------------|------------------|----------------|
| Mix | 15 % | 0–100 % (0.0 a 1.0) | `ClientReverbTxMix` | Balance lineal seco/húmedo. Los valores más altos aumentan la proporción de cola de reverb en la señal transmitida. |
| Size | 50 % | 0–100 % (0.0 a 1.0) | `ClientReverbTxSize` | Modela el tamaño de la sala. |
| Decay | 1.20 s | 0.3 a 5.0 s | `ClientReverbTxDecayS` | Define la longitud de la cola de reverb (mapeo exponencial). |
| Damp | 50 % | 0–100 % (0.0 a 1.0) | `ClientReverbTxDamping` | Los valores más altos atenúan las frecuencias altas más rápido en la cola. |
| Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Retardo previo entre la señal seca y las primeras reflexiones. |

## Consejos

- El valor predeterminado de Mix es el 15 %, que ya se encuentra dentro del rango típico para voz. Si restablece el control a su valor predeterminado, vuelve al 15 %.
- Tanto el control del applet compacto como el del editor flotante permanecen sincronizados. Los cambios realizados en uno se reflejan en el otro en aproximadamente 33 ms.
- Mix al 0 % deja pasar únicamente la señal seca; la etapa de reverb sigue activa pero es inaudible. Para eliminarla completamente de la cadena de procesamiento, consulte [Omitir el reverb desde la cadena](bypass-reverb-from-the-chain.md).

## Relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Omitir el reverb desde la cadena](bypass-reverb-from-the-chain.md)
- [Ajuste el decay a su gusto sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Reduzca el brillo en las frecuencias altas de la cola con Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Desplace las reflexiones respecto a la señal seca con Pre](offset-reflections-from-the-dry-signal-with-pre.md)
