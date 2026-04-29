# Ajuste un Mix sutil — el valor típico para voz es del 10–15 %

El control Mix regula el balance seco/húmedo del reverb Aetherial FreeVerb en el audio transmitido. Mantener Mix en el rango del 10–15 % añade una leve sensación de espacio sin que la voz suene procesada o distante.

## Antes de comenzar

- La etapa de reverb debe estar habilitada en el widget CHAIN. El subcontenedor "Aetherial FreeVerb" permanece oculto hasta que la etapa esté activa.
- Puede ajustar Mix desde la fila compacta del applet dentro del contenedor Aetherial Audio (TXDSP) o desde el editor flotante "Aetherial FreeVerb — TX".

## Pasos

1. Abra el editor flotante haciendo doble clic en la etapa VERB del widget CHAIN. Aparece el editor titulado "Aetherial FreeVerb — TX".
2. Localice el control Mix — el más a la derecha de los cinco controles de la fila del editor.
3. Gire Mix hasta el valor deseado. La etiqueta del control se actualiza en tiempo real y se muestra como porcentaje (por ejemplo, `15 %`).
4. Para voz, establezca Mix entre el 10 % y el 15 %. Los valores más bajos mezclan menos cola de reverb; los valores más altos hacen el efecto más prominente.
5. Cierre el editor o déjelo abierto. El valor se guarda de inmediato.

## Qué hace cada control

| Etiqueta | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|----------|---------------|--------------|------------------|----------------|
| Mix | 15 % | 0–100 % (0.0 a 1.0) | `ClientReverbTxMix` | Balance lineal seco/húmedo. Los valores más altos aumentan la proporción de cola de reverb en la señal transmitida. |
| Size | 50 % | 0–100 % (0.0 a 1.0) | `ClientReverbTxSize` | Modela el tamaño del recinto. |
| Decay | 1.20 s | 0.3 a 5.0 s | `ClientReverbTxDecayS` | Establece la longitud de la cola de reverb (mapeo exponencial). |
| Damp | 50 % | 0–100 % (0.0 a 1.0) | `ClientReverbTxDamping` | Los valores más altos atenúan las frecuencias altas más rápidamente en la cola. |
| Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Predelay entre la señal seca y las primeras reflexiones. |

## Consejos

- El valor predeterminado de Mix es el 15 %, que ya se encuentra dentro del rango típico para voz. Si restablece el control a su valor predeterminado, vuelve al 15 %.
- Tanto el control del applet compacto como el del editor flotante permanecen sincronizados. Los cambios realizados en uno se reflejan en el otro en aproximadamente 33 ms.
- Mix al 0 % deja pasar únicamente la señal seca; la etapa de reverb sigue activa pero no se escucha. Para eliminarla completamente de la cadena de procesamiento, consulte [Desactivar el reverb desde la cadena](bypass-reverb-from-the-chain.md).

## Temas relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Desactivar el reverb desde la cadena](bypass-reverb-from-the-chain.md)
- [Ajustar el decay al gusto sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Reducir el brillo de los agudos en la cola con Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Separar las reflexiones de la señal seca con Pre](offset-reflections-from-the-dry-signal-with-pre.md)
