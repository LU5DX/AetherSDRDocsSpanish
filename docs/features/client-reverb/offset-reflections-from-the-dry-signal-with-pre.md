# Desplace las reflexiones del sonido seco con Pre

El mando Pre agrega un intervalo entre la señal seca y el inicio de la cola de reverberación. Úselo para mantener su voz nítida y en primer plano mientras la reverberación florece detrás de ella.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. El applet permanece oculto hasta que la etapa esté activa.
- Abra el applet Aetherial FreeVerb o el editor flotante. Para abrir el editor, haga doble clic en la etapa VERB del widget CHAIN; la ventana lleva el título "Aetherial FreeVerb — TX".

## Pasos

1. Localice el mando Pre en la fila de cinco mandos (Size, Decay, Damp, **Pre**, Mix).
2. Gire Pre en sentido horario para aumentar el retardo entre la señal seca y las primeras reflexiones, o en sentido antihorario para reducirlo.
3. Observe la etiqueta debajo del mando; muestra el valor en milisegundos (por ejemplo, `20 ms`).
4. Deténgase cuando la cola de reverberación se sienta separada de su voz sin sonar desconectada.

## Qué hace cada control

| Control | Valor por defecto | Rango válido | Clave persistida | Comportamiento |
|---------|-------------------|--------------|------------------|----------------|
| Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Mapeo lineal. Establece el tiempo entre la señal seca y las primeras reflexiones de reverberación. |

## Consejos

- Un valor de Pre de 0 ms hace que las reflexiones comiencen de inmediato, lo que puede difuminar los transitorios. Los valores entre 15 y 30 ms son habituales para voz a fin de preservar la inteligibilidad.
- Pre interactúa con Decay: un Pre corto combinado con un Decay largo puede hacer que la cola parezca comenzar antes de lo esperado. Aumente Pre si la reverberación parece engullir el borde inicial de las palabras.
- Tanto el mando del applet compacto (etiquetado Pre) como el del editor flotante (etiquetado PreDly) controlan el mismo parámetro `ClientReverbTxPreDelayMs` y permanecen sincronizados.

## Relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste el decay a su gusto sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Establezca un Mix sutil — entre 10 y 15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omitir la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
