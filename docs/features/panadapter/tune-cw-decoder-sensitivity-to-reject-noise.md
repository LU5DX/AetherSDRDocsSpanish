# Ajuste de la sensibilidad del decodificador CW para rechazar ruido

El control deslizante **Sens** define con qué rigor el decodificador CW filtra las decodificaciones de caracteres inciertas. Al aumentarlo, se suprime la salida distorsionada causada por ruido o señales débiles; al disminuirlo, se muestran más caracteres a costa de la precisión.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto en el applet Panadapter. Si no está visible, ábralo primero.
- El audio de la PC debe estar enrutado a AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio.

## Pasos

1. Localice el panel de decodificación CW en la parte inferior del applet Panadapter.
2. Busque la etiqueta **Sens:** y el control deslizante horizontal corto inmediatamente a su derecha.
3. Arrastre el control deslizante **Sens** hacia la izquierda para aceptar más decodificaciones (umbral más bajo) o hacia la derecha para rechazar decodificaciones de baja confianza (umbral más alto).
4. Observe el área de "texto de decodificación CW". Los caracteres en rojo o naranja indican baja confianza; redúzcalos moviendo el control deslizante hacia la derecha.
5. Suelte el control deslizante. El valor se guarda automáticamente en `CwDecoderSensitivity`.

## Función de cada control

| Control                 | Valor predeterminado | Rango                |
|-------------------------|----------------------|----------------------|
| Control deslizante **Sens** | 30                   | 0–100                |
| Texto de decodificación CW | —                    | —                    |
| Etiqueta de estadísticas CW | —                    | `<hz> Hz  <wpm> WPM` |
| Control deslizante de rango **Pitch** | 500–700 Hz           | 300–1200 Hz          |
| Control deslizante de rango **WPM**  | 15–40 WPM            | 5–60 WPM             |

## Coloreado del texto de decodificación CW

El texto decodificado utiliza colores para indicar la confianza:

| Color  | Umbral de costo | Significado                |
|--------|-----------------|----------------------------|
| Verde  | < 0.15          | Confianza alta             |
| Amarillo | < 0.35        | Confianza moderada         |
| Naranja | < 0.60         | Confianza baja             |
| Rojo   | >= 0.60         | Confianza muy baja         |

El texto decodificado del lado de TX (su propia transmisión) aparece en cian (`#5fc8ff`) para que pueda distinguir su transmisión del CW entrante. Al cambiar de TX a RX, se inserta automáticamente un espacio separador para evitar que las dos secuencias de colores se fusionen.

## Consejos

- Comience con el valor predeterminado de 30 y aumente gradualmente el control deslizante hasta que los caracteres rojos y naranjas desaparezcan del texto decodificado.
- El color de los caracteres es un indicador rápido de confianza: si la mayor parte de la salida es verde, la sensibilidad actual está bien ajustada a las condiciones de la señal. Si la pantalla se queda completamente en blanco, el control deslizante está demasiado alto — muévalo hacia la izquierda hasta que los caracteres vuelvan a aparecer.
- El control deslizante de rango **Pitch** (predeterminado 500–700 Hz, rango 300–1200 Hz) limita las frecuencias tonales que el decodificador busca. Reducir ese rango para que coincida con el tono de la señal recibida puede reducir las activaciones falsas independientemente de **Sens**.
- El control deslizante de rango **WPM** (predeterminado 15–40 WPM, rango 5–60 WPM) limita las velocidades que el decodificador busca. Reducir ese rango para que coincida con la velocidad de transmisión de la señal recibida mejora la precisión de la decodificación.
- Al hacer clic derecho en el área de texto de decodificación CW también se accede a las acciones de texto estándar (Seleccionar todo, Copiar, etc.) junto con la opción **Clear**.

## Solución de problemas

- **El texto decodificado desaparece por completo después de aumentar Sens** — el umbral está por encima del nivel de confianza de la señal entrante. Baje el control deslizante hasta que la salida regrese, luego auméntelo más lentamente.
- **La salida sigue siendo ruidosa incluso con Sens en 100** — la señal podría estar fuera de la ventana de búsqueda de tono. Verifique la etiqueta de estadísticas CW para ver el tono informado y ajuste el control deslizante de rango **Pitch** para que lo incluya.
- **Sens se restablece a 30 después de reiniciar** — si falta `CwDecoderSensitivity` en la configuración guardada, AetherSDR usa el valor predeterminado de 30. Mueva el control deslizante una vez para escribir el valor; luego se guarda en cada cambio.

## Relacionado

- [Activar el decodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
