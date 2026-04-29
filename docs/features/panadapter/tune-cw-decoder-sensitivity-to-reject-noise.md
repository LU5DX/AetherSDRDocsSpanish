# Ajustar la sensibilidad del decodificador CW para rechazar ruido

El control deslizante **Sens** controla con qué rigor el decodificador CW filtra los caracteres decodificados con incertidumbre. Aumentarlo suprime la salida confusa causada por ruido o señales débiles; reducirlo muestra más caracteres a costa de la precisión.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto en el applet Panadapter. Si no es visible, ábralo primero.
- El audio de la PC debe estar enrutado hacia AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio.

## Pasos

1. Ubique el panel de decodificación CW en la parte inferior del applet Panadapter.
2. Localice la etiqueta **Sens:** y el control deslizante horizontal corto inmediatamente a su derecha.
3. Arrastre el control deslizante **Sens** hacia la izquierda para aceptar más decodificaciones (umbral inferior) o hacia la derecha para rechazar decodificaciones de baja confianza (umbral superior).
4. Observe el área de texto "CW decode text". Los caracteres de color rojo o naranja indican baja confianza; redúzcalos moviendo el control deslizante hacia la derecha.
5. Suelte el control deslizante. El valor se guarda automáticamente en `CwDecoderSensitivity`.

## Qué hace cada control

| Control | Valor predeterminado | Rango | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Control deslizante **Sens** | 30 | 0–100 | `CwDecoderSensitivity` | Asigna el rango 0–100 a un umbral de costo interno de 1.0–0.1. Los valores más altos implican un filtrado más estricto: solo se muestran los caracteres de alta confianza. |
| Texto de decodificación CW | — | — | — | Pantalla continua de solo lectura con color según la confianza: verde (más alta), amarillo, naranja, rojo (más baja). Haga clic derecho en cualquier parte del área de texto para abrir un menú contextual; seleccione **Clear** en ese menú para limpiar el búfer de decodificación sin abandonar el teclado. |
| Etiqueta de estadísticas CW | — | `<hz> Hz  <wpm> WPM` | — | Muestra el tono y la velocidad que el decodificador está rastreando actualmente. |

## Consejos

- Comience con el valor predeterminado de 30 y aumente el control deslizante gradualmente hasta que los caracteres rojos y naranjas desaparezcan del texto decodificado.
- El color del carácter es un indicador rápido de confianza: si la mayor parte de la salida es verde, la sensibilidad actual se ajusta bien a las condiciones de la señal. Si la pantalla queda completamente en blanco, el control deslizante está configurado demasiado alto — muévalo hacia la izquierda hasta que vuelvan a aparecer caracteres.
- Los controles deslizantes de tono **Lo** y **Hi** (500 Hz y 700 Hz por defecto, rango 300–1200 Hz) limitan los tonos en los que el decodificador realiza la búsqueda. Reducir ese rango para que coincida con el tono lateral de la señal recibida puede disminuir las falsas activaciones de forma independiente de **Sens**.
- Hacer clic derecho en el área de texto CW también da acceso a las acciones de texto estándar (Select All, Copy, entre otras) junto con la opción **Clear**.

## Solución de problemas

- **El texto decodificado desaparece por completo al aumentar Sens** — el umbral está por encima del nivel de confianza de la señal entrante. Reduzca el control deslizante hasta que vuelva a aparecer la salida y, luego, auméntelo más lentamente.
- **La salida sigue siendo ruidosa incluso con Sens en 100** — es posible que la señal esté fuera de la ventana de búsqueda de tono. Verifique la etiqueta de estadísticas CW para conocer el tono reportado y ajuste **Lo** y **Hi** para encuadrarlo.
- **Sens se reinicia a 30 después de reiniciar** — si `CwDecoderSensitivity` no está presente en la configuración guardada, AetherSDR utiliza el valor predeterminado de 30. Mueva el control deslizante una vez para escribir el valor; a partir de ese momento se guarda en cada cambio.

## Relacionados

- [Activar el decodificador CW para leer código Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el rastreo es estable](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
