# Ajuste la sensibilidad del decodificador CW para rechazar ruido

El control deslizante **Sens** regula qué tan estrictamente el decodificador CW filtra decodificaciones de caracteres inciertas. Aumentarlo suprime la salida distorsionada causada por ruido o señales débiles; reducirlo muestra más caracteres a costa de la precisión.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto en el applet Panadapter. Si no es visible, ábralo primero.
- El audio de la PC debe enrutarse a AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio.

## Pasos

1. Ubique el panel de decodificación CW en la parte inferior del applet Panadapter.
2. Busque la etiqueta **Sens:** y el pequeño control deslizante horizontal inmediatamente a su derecha.
3. Arrastre el control deslizante **Sens** hacia la izquierda para aceptar más decodificaciones (umbral más bajo) o hacia la derecha para rechazar decodificaciones de baja confianza (umbral más alto).
4. Observe el área de "texto decodificado CW". Los caracteres en rojo o naranja indican baja confianza; redúzcalos moviendo el control deslizante hacia la derecha.
5. Suelte el control deslizante. El valor se guarda automáticamente en `CwDecoderSensitivity`.

## Qué hace cada control

| Control              | Por defecto | Rango                |
|----------------------|-------------|----------------------|
| Control desl. **Sens**| 30          | 0–100                |
| Texto decodif. CW    | —           | —                    |
| Etiqueta estad. CW   | —           | `<hz> Hz  <wpm> WPM` |

## Consejos

- Comience en el valor predeterminado de 30 y aumente el control deslizante gradualmente hasta que los caracteres rojos y naranjas desaparezcan del texto decodificado.
- El color de los caracteres es un indicador rápido de confianza: si la mayor parte de la salida es verde, la sensibilidad actual está bien ajustada a las condiciones de la señal. Si la pantalla se queda completamente en blanco, el control deslizante está demasiado alto — muévalo hacia la izquierda hasta que los caracteres regresen.
- Los controles deslizantes de tono **Lo** y **Hi** (por defecto 500 Hz y 700 Hz, rango 300–1200 Hz) limitan qué tonos busca el decodificador. Reducir ese rango para que coincida con el tono de la señal recibida puede reducir falsas detecciones independientemente de **Sens**.
- Hacer clic derecho en el área de texto decodificado CW también proporciona acceso a las acciones de texto estándar (Seleccionar todo, Copiar, etc.) junto con la opción **Clear**.

## Solución de problemas

- **El texto decodificado desaparece por completo al aumentar Sens** — el umbral está por encima del nivel de confianza de la señal entrante. Baje el control deslizante hasta que la salida regrese, luego auméntelo más lentamente.
- **La salida sigue siendo ruidosa incluso con Sens en 100** — la señal puede estar fuera de la ventana de búsqueda de tono. Verifique la etiqueta de estadísticas CW para conocer el tono reportado y ajuste **Lo** y **Hi** para que lo incluyan.
- **Sens se reinicia a 30 después de reiniciar** — si falta `CwDecoderSensitivity` en la configuración guardada, AetherSDR usa el valor predeterminado de 30. Mueva el control deslizante una vez para escribir el valor; luego se guarda en cada cambio.

## Relacionados

- [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Lock CW decoder pitch or speed once tracking is good](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copy decoded CW text to the clipboard](copy-decoded-cw-text-to-the-clipboard.md)
