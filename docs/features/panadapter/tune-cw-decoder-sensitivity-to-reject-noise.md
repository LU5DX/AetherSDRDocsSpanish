# Ajustar la sensibilidad del decodificador CW para rechazar el ruido

El control deslizante **Sens** controla con qué rigor el decodificador CW filtra las decodificaciones de baja confianza. Al aumentarlo se reducen los caracteres incorrectos causados por el ruido; al disminuirlo se permiten señales más débiles o rápidas sobre las que el decodificador tiene menos certeza.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto. Si no está visible debajo del panadapter, consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio de la PC debe estar enrutado hacia AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio si el audio no está llegando al decodificador.

## Pasos

1. Localice el panel de decodificación CW en la parte inferior del panadapter.
2. Encuentre el control deslizante **Sens** en la barra de controles del panel.
3. Arrastre el control hacia la derecha para aumentar la sensibilidad (filtrado más estricto, menos caracteres de baja confianza en la salida) o hacia la izquierda para disminuirla (más permisivo, más caracteres en la salida, incluidos los inciertos).
4. Observe el texto decodificado en el área **CW decode text**. Los caracteres se colorean según el nivel de confianza: verde es la mayor confianza, luego amarillo, naranja y rojo. Aumente **Sens** hasta que los caracteres rojos y naranjas disminuyan a un nivel aceptable.

La configuración se guarda automáticamente. La próxima vez que AetherSDR se inicie, el control deslizante se restaurará a este valor.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de persistencia | Comportamiento |
|---|---|---|---|---|
| Sens | 30 | 0–100 | `CwDecoderSensitivity` | Filtra las decodificaciones de baja confianza. Los valores más altos aplican un umbral de costo más estricto, rechazando los caracteres más inciertos. Mapea 0–100 a un umbral de costo interno de 1.0–0.1. |

## Consejos

- Un valor de **Sens** de 30 (el predeterminado) es un buen punto de partida en una banda tranquila. En una banda ruidosa o con una señal débil, pruebe valores en el rango de 50–70 y observe si el color del texto decodificado se desplaza hacia el verde.
- Si una señal fuerte y limpia produce pocos caracteres decodificados, disminuya **Sens** hacia 10–20 para suavizar el umbral.
- Los controles deslizantes de tono **Lo** y **Hi** (300–1200 Hz, valores predeterminados 500 Hz y 700 Hz) reducen el rango de frecuencias que el decodificador examina. Restringir este rango puede ayudar por sí solo antes de que sea necesario aumentar **Sens**. Consulte [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md) para mantener el decodificador en un tono conocido una vez que esté siguiendo correctamente.
- Use **CLR** para limpiar el búfer de decodificación después de ajustar **Sens**, de modo que solo lea la salida nueva con la nueva configuración.

## Solución de problemas

- **El decodificador sigue mostrando muchos caracteres incorrectos con un valor alto de Sens** — Confirme que el audio de la PC está siendo recibido (la etiqueta de estadísticas CW debe mostrar un tono en Hz y una velocidad en WPM). Si la etiqueta de estadísticas está en blanco, el decodificador no está recibiendo audio y la sensibilidad no tiene efecto.
- **No aparece ningún carácter** — Es posible que **Sens** esté configurado demasiado alto (cerca de 100), o que el tono de la señal quede fuera del rango Lo–Hi. Disminuya **Sens** hacia 20–30 y amplíe el rango de tono de **Lo** y **Hi** para cubrir la señal.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
