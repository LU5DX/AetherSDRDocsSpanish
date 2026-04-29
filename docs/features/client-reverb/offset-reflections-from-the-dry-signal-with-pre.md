# Compensar reflexiones de la señal seca con Pre

El control Pre añade un intervalo entre la señal seca y el inicio de la cola de reverberación. Úselo para mantener su voz definida y en primer plano mientras permite que la reverberación se expanda detrás de ella.

## Antes de empezar

- La etapa Reverb debe estar habilitada en el widget CHAIN. El applet permanece oculto hasta que la etapa esté activa.
- Abra el applet Aetherial FreeVerb o el editor flotante. Para abrir el editor, haga doble clic en la etapa VERB del widget CHAIN; la ventana se titula "Aetherial FreeVerb — TX".

## Pasos

1. Localice el control Pre en la fila de cinco controles (Size, Decay, Damp, **Pre**, Mix).
2. Gire Pre hacia la derecha para aumentar el retardo entre la señal seca y las primeras reflexiones, o hacia la izquierda para reducirlo.
3. Observe la etiqueta debajo del control; muestra el valor en milisegundos (por ejemplo, `20 ms`).
4. Detenga el ajuste cuando la cola de reverberación se perciba separada de su voz sin sonar desconectada.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---------|---------------------|--------------|------------------|----------------|
| Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Mapeo lineal. Establece el tiempo entre la señal seca y las primeras reflexiones de reverberación. |

## Consejos

- Un valor de Pre de 0 ms hace que las reflexiones comiencen de inmediato, lo que puede difuminar los transitorios. Los valores en el rango de 15–30 ms son habituales para voz con el fin de preservar la inteligibilidad.
- Pre interactúa con Decay: un Pre corto con un Decay largo puede hacer que la cola parezca comenzar antes de lo esperado. Aumente Pre si la reverberación parece envolver el borde inicial de las palabras.
- Tanto el control del applet compacto (etiquetado Pre) como el del editor flotante (etiquetado PreDly) controlan el mismo ajuste `ClientReverbTxPreDelayMs` y permanecen sincronizados.

## Temas relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajustar el Decay al gusto sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Configurar un Mix sutil — 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Desactivar la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
