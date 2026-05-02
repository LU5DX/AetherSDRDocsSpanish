# Ajustar la sensibilidad del decodificador CW para rechazar el ruido

El control deslizante **Sens** determina con qué rigor el decodificador CW filtra los caracteres decodificados con baja confianza. Aumentarlo suprime la salida distorsionada causada por el ruido o las señales débiles; reducirlo muestra más caracteres a costa de la precisión.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto en el applet Panadapter. Si no está visible, ábralo primero.
- El audio del PC debe estar enrutado hacia AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio.

## Pasos

1. Ubique el panel de decodificación CW en la parte inferior del applet Panadapter.
2. Localice la etiqueta **Sens:** y el control deslizante horizontal corto que se encuentra inmediatamente a su derecha.
3. Arrastre el control **Sens** hacia la izquierda para aceptar más decodificaciones (umbral menor) o hacia la derecha para rechazar las de baja confianza (umbral mayor).
4. Observe el área de texto "CW decode text". Los caracteres en rojo o naranja indican baja confianza; redúzcalos desplazando el control hacia la derecha.
5. Suelte el control. El valor se guarda automáticamente en `CwDecoderSensitivity`.

## Qué hace cada control

| Control                  | Valor predeterminado | Rango                |
|--------------------------|----------------------|----------------------|
| Control deslizante **Sens** | 30                | 0–100                |
| Texto de decodificación CW  | —                 | —                    |
| Etiqueta de estadísticas CW | —                 | `<hz> Hz  <wpm> WPM` |

## Consejos

- Comience con el valor predeterminado de 30 y aumente el control gradualmente hasta que los caracteres rojos y naranjas desaparezcan del texto decodificado.
- El color de los caracteres es un indicador rápido de confianza: si la mayor parte de la salida es verde, la sensibilidad actual está bien adaptada a las condiciones de la señal. Si la pantalla queda completamente en blanco, el control está ajustado demasiado alto — muévalo hacia la izquierda hasta que los caracteres vuelvan a aparecer.
- Los controles deslizantes de tono **Lo** y **Hi** (500 Hz y 700 Hz de forma predeterminada, rango de 300–1200 Hz) limitan los tonos en los que el decodificador realiza la búsqueda. Reducir ese rango para que coincida con el tono lateral de la señal recibida puede disminuir las activaciones falsas de manera independiente a **Sens**.
- Al hacer clic derecho en el área de texto de decodificación CW también se accede a las acciones de texto estándar (Select All, Copy, entre otras), junto con la opción **Clear**.

## Solución de problemas

- **El texto decodificado desaparece por completo al aumentar Sens** — el umbral está por encima del nivel de confianza de la señal entrante. Reduzca el control hasta que la salida vuelva y luego auméntelo más lentamente.
- **La salida sigue siendo ruidosa incluso con Sens en 100** — es posible que la señal esté fuera del rango de búsqueda de tono. Revise la etiqueta de estadísticas CW para conocer el tono reportado y ajuste **Lo** y **Hi** para encuadrarlo.
- **Sens se restablece a 30 después de reiniciar** — si `CwDecoderSensitivity` no está en la configuración guardada, AetherSDR usa el valor predeterminado de 30. Mueva el control una vez para escribir el valor; a partir de entonces se guarda con cada cambio.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
