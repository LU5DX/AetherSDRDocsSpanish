# Ajuste la sensibilidad del decodificador CW para rechazar ruido

El control deslizante **Sens** determina con qué rigor el decodificador CW filtra las decodificaciones de caracteres inciertas. Subirlo suprime la salida confusa causada por ruido o señales débiles; bajarlo muestra más caracteres a costa de precisión.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto en el applet Panadapter. Si no está visible, ábralo primero.
- El audio del PC debe estar enrutado a AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio.

## Pasos

1. Localice el panel de decodificación CW en la parte inferior del applet Panadapter.
2. Busque la etiqueta **Sens:** y el control deslizante horizontal corto inmediatamente a su derecha.
3. Arrastre el control deslizante **Sens** hacia la izquierda para aceptar más decodificaciones (umbral más bajo) o hacia la derecha para rechazar decodificaciones de baja confianza (umbral más alto).
4. Observe el área de "CW decode text". Los caracteres en rojo o naranja indican baja confianza; redúzcalos moviendo el control deslizante hacia la derecha.
5. Suelte el control deslizante. El valor se guarda automáticamente en `CwDecoderSensitivity`.

## Función de cada control

| Control              | Valor predeterminado | Rango                |
|----------------------|----------------------|----------------------|
| Control deslizante **Sens** | 30                   | 0–100                |
| CW decode text       | —                    | —                    |
| Etiqueta de estadísticas CW | —              | `<hz> Hz  <wpm> WPM` |

## Codificación por colores del texto decodificado CW

El texto decodificado usa colores para indicar la confianza:

| Color  | Umbral de costo | Significado            |
|--------|-----------------|------------------------|
| Verde  | < 0.15          | Alta confianza         |
| Amarillo | < 0.35        | Confianza moderada     |
| Naranja | < 0.60         | Baja confianza         |
| Rojo   | >= 0.60         | Confianza muy baja     |

El texto decodificado del lado TX (su propia transmisión) aparece en cian (`#5fc8ff`) para que pueda distinguir su transmisión del CW entrante. Al cambiar de TX a RX, se inserta automáticamente un espacio separador para evitar que las dos secuencias de colores se fusionen.

## Consejos

- Comience en el valor predeterminado de 30 y suba el control deslizante gradualmente hasta que los caracteres rojos y naranjas desaparezcan del texto decodificado.
- El color del carácter es un indicador rápido de confianza: si la mayor parte de la salida es verde, la sensibilidad actual está bien ajustada a las condiciones de la señal. Si la pantalla se queda completamente en blanco, el control deslizante está demasiado alto — muévalo hacia la izquierda hasta que los caracteres vuelvan.
- Los controles deslizantes de tono **Lo** y **Hi** (valores predeterminados 500 Hz y 700 Hz, rango 300–1200 Hz) limitan los tonos que el decodificador busca. Reducir ese rango para que coincida con el tono de la señal recibida puede reducir las activaciones falsas independientemente de **Sens**.
- Al hacer clic derecho en el área de texto decodificado CW también se accede a las acciones de texto estándar (Seleccionar todo, Copiar, etc.) junto con la opción **Clear**.

## Solución de problemas

- **El texto decodificado desaparece por completo después de subir Sens** — el umbral está por encima del nivel de confianza de la señal entrante. Baje el control deslizante hasta que la salida regrese, luego súbalo más lentamente.
- **La salida sigue siendo ruidosa incluso con Sens al 100** — la señal podría estar fuera de la ventana de búsqueda de tono. Verifique la etiqueta de estadísticas CW para conocer el tono informado y ajuste **Lo** y **Hi** para enmarcarlo.
- **Sens se restablece a 30 después de reiniciar** — si `CwDecoderSensitivity` falta en la configuración guardada, AetherSDR usa el valor predeterminado de 30. Mueva el control deslizante una vez para escribir el valor; luego se guarda en cada cambio.

## Relacionados

- [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Lock CW decoder pitch or speed once tracking is good](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copy decoded CW text to the clipboard](copy-decoded-cw-text-to-the-clipboard.md)
