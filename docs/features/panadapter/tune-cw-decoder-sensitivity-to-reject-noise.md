# Ajustar la sensibilidad del decodificador CW para rechazar ruido

El control deslizante **Sens** determina con qué rigor el decodificador CW filtra los caracteres decodificados con baja certeza. Aumentarlo suprime la salida ilegible causada por ruido o señales débiles; reducirlo muestra más caracteres a costa de la precisión.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto en el applet Panadapter. Si no es visible, ábralo primero.
- El audio del PC debe estar enrutado hacia AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio.

## Pasos

1. Ubique el panel de decodificación CW en la parte inferior del applet Panadapter.
2. Localice la etiqueta **Sens:** y el control deslizante horizontal corto situado inmediatamente a su derecha.
3. Arrastre el control **Sens** hacia la izquierda para aceptar más decodificaciones (umbral más bajo) o hacia la derecha para rechazar decodificaciones de baja confianza (umbral más alto).
4. Observe el área de texto "CW decode text". Los caracteres en rojo o naranja indican baja confianza; redúzcalos moviendo el control hacia la derecha.
5. Suelte el control. El valor se guarda automáticamente en `CwDecoderSensitivity`.

## Qué hace cada control

| Control | Valor predeterminado | Rango | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Control deslizante **Sens** | 30 | 0–100 | `CwDecoderSensitivity` | Asigna el rango 0–100 a un umbral de costo interno de 1.0–0.1. Los valores más altos implican un filtrado más estricto: solo se muestran los caracteres de alta confianza. |
| Texto de decodificación CW | — | — | — | Pantalla continua de solo lectura con color según la confianza: verde (más alta), amarillo, naranja, rojo (más baja). |
| Etiqueta de estadísticas CW | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad que el decodificador está siguiendo en ese momento. |

## Consejos

- Comience con el valor predeterminado de 30 y aumente el control gradualmente hasta que los caracteres en rojo y naranja desaparezcan del texto decodificado.
- El color de los caracteres es un indicador rápido de confianza: si la mayor parte de la salida es verde, la sensibilidad actual está bien ajustada a las condiciones de la señal. Si la pantalla queda completamente en blanco, el control está demasiado alto — muévalo hacia la izquierda hasta que los caracteres vuelvan a aparecer.
- Los controles deslizantes de tono **Lo** y **Hi** (valores predeterminados de 500 Hz y 700 Hz, rango de 300–1200 Hz) limitan los tonos en los que el decodificador realiza la búsqueda. Reducir ese rango para que coincida con el tono lateral de la señal recibida puede disminuir las falsas detecciones de forma independiente a **Sens**.

## Resolución de problemas

- **El texto decodificado desaparece por completo al aumentar Sens** — el umbral supera el nivel de confianza de la señal entrante. Baje el control hasta que vuelva a aparecer la salida y luego auméntelo más despacio.
- **La salida sigue siendo ruidosa incluso con Sens en 100** — la señal puede estar fuera de la ventana de búsqueda de tono. Verifique la etiqueta de estadísticas CW para conocer el tono reportado y ajuste **Lo** y **Hi** para enmarcarlo.
- **Sens vuelve a 30 tras reiniciar** — si `CwDecoderSensitivity` no está presente en la configuración guardada, AetherSDR utiliza el valor predeterminado de 30. Mueva el control una vez para escribir el valor; a partir de entonces se guarda en cada cambio.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
