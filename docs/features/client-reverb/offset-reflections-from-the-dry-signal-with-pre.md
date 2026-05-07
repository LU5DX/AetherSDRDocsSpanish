# Desfase de las reflexiones de la señal limpia con Pre

El control Pre añade un espacio entre la señal limpia y el inicio de la cola de reverberación. Úselo para mantener su voz nítida y al frente mientras permite que la reverberación se desarrolle detrás.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. El applet permanece oculto hasta que la etapa esté activa.
- Abra el applet Aetherial FreeVerb o el editor flotante. Para abrir el editor, haga doble clic en la etapa VERB en el widget CHAIN; la ventana se titula "Aetherial FreeVerb — TX".

## Pasos

1. Localice el control Pre en la fila de cinco controles (Size, Decay, Damp, **Pre**, Mix).
2. Gire Pre en sentido horario para aumentar el retardo entre la señal limpia y las primeras reflexiones, o en sentido antihorario para reducirlo.
3. Supervise la etiqueta debajo del control; muestra el valor en milisegundos (por ejemplo, `20 ms`).
4. Deténgase cuando la cola de reverberación se sienta separada de su voz sin sonar desconectada.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---------|---------------------|--------------|------------------|----------------|
| Pre | 20 ms | 0 a 100 ms | `ClientReverbTxPreDelayMs` | Mapeo lineal. Establece el tiempo entre la señal limpia y las primeras reflexiones de reverberación. |

## Visualización en vivo

A partir de v0.9.7, el applet Aetherial FreeVerb incluye un diagrama de reverberación en tiempo real mostrado sobre la fila de controles. La visualización es un panel compacto de 90 píxeles de alto con fondo oscuro y líneas de cuadrícula. Se actualiza inmediatamente al mover cualquiera de los cinco controles.

El diagrama muestra tres capas de forma de onda superpuestas:

- **Cian — señal limpia.** Un paquete sinusoidal que representa el audio sin procesar. Su amplitud disminuye a medida que se aumenta Mix, reflejando el cambio hacia la señal procesada.
- **Amarillo — reflexiones de primer orden.** Una serie de breves ráfagas sinusoidales que comienzan después del espacio de pre-retardo. Su separación se amplía al aumentar Size, y su amplitud decae más rápido al aumentar Damp.
- **Magenta — cola reverberante.** Una oscilación con decaimiento exponencial que comienza en el mismo desfase que las reflexiones. Su extensión horizontal crece con Decay, y valores más altos de Damp hacen que la amplitud de la cola colapse más rápidamente.

La posición donde comienzan las capas amarilla y magenta se desplaza hacia la derecha al aumentar Pre, mostrando directamente el espacio entre la señal limpia y las primeras reflexiones.

No se requiere configuración. La visualización siempre está visible cuando el applet está abierto y la etapa Reverb está activa.

## Consejos

- Un valor de Pre de 0 ms hace que las reflexiones comiencen inmediatamente, lo que puede difuminar los transitorios. Los valores en el rango de 15–30 ms son comunes para voz a fin de preservar la inteligibilidad.
- Pre interactúa con Decay: un Pre corto con un Decay largo puede hacer que la cola parezca comenzar antes de lo esperado. Aumente Pre si la reverberación parece tragar el borde inicial de las palabras.
- Tanto el control del applet compacto (etiquetado Pre) como el control del editor flotante ajustan la misma configuración `ClientReverbTxPreDelayMs` y se mantienen sincronizados.
- Use la visualización en vivo para confirmar que las ráfagas de reflexión amarillas comiencen claramente a la derecha del paquete de señal limpia cian. Si las dos capas parecen superponerse, aumente Pre.

## Relacionado

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste el decaimiento al gusto sin enturbiar el habla](tune-decay-to-taste-without-muddying-speech.md)
- [Ajuste una mezcla sutil — 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omita la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
