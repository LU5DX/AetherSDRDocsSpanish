# Ajustar la sensibilidad del decodificador CW para rechazar ruido

El control deslizante **Sens** determina con qué rigurosidad el decodificador CW filtra decodificaciones de caracteres inciertas. Subirlo suprime la salida distorsionada causada por ruido o señales débiles; bajarlo muestra más caracteres a costa de precisión.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto en el applet Panadapter. Si no es visible, ábralo primero.
- El audio del PC debe estar enrutado a AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio.

## Pasos

1. Localice el panel de decodificación CW en la parte inferior del applet Panadapter.
2. Encuentre la etiqueta **Sens:** y el control deslizante horizontal corto inmediatamente a su derecha.
3. Arrastre el control deslizante **Sens** hacia la izquierda para aceptar más decodificaciones (umbral más bajo) o hacia la derecha para rechazar decodificaciones de baja confianza (umbral más alto).
4. Observe el área de "texto de decodificación CW". Los caracteres en color rojo o naranja indican baja confianza; redúzcalos moviendo el control deslizante hacia la derecha.
5. Suelte el control deslizante. El valor se guarda automáticamente en `CwDecoderSensitivity`.

## Función de cada control

| Control                     | Valor predeterminado | Rango                |
|-----------------------------|----------------------|----------------------|
| Control deslizante **Sens** | 30                   | 0–100                |
| Texto de decodificación CW  | —                    | —                    |
| Etiqueta de estadísticas CW | —                    | `<hz> Hz  <wpm> WPM` |
| Control deslizante de rango de **Pitch** | 500–700 Hz | 300–1200 Hz        |
| Control deslizante de rango de **WPM**   | 15–40 WPM  | 5–60 WPM            |
| Botón **A-**                | —                    | —                    |
| Botón **A+**                | —                    | —                    |
| Asa de redimensión del panel CW | —                | —                    |

## Codificación de colores del texto de decodificación CW

El texto decodificado usa colores para indicar confianza:

| Color  | Umbral de costo | Significado             |
|--------|-----------------|-------------------------|
| Verde  | < 0,15          | Alta confianza          |
| Amarillo | < 0,35        | Confianza moderada      |
| Naranja | < 0,60         | Baja confianza          |
| Rojo   | >= 0,60         | Muy baja confianza      |

El texto decodificado del lado TX (su propia transmisión) aparece en cian (`#5fc8ff`) para que pueda distinguir su transmisión del CW entrante. Al cambiar de TX a RX, se inserta automáticamente un espacio separador para evitar que las dos secuencias de color se fusionen.

## Ajustar el tamaño de fuente del texto de decodificación CW

Los botones **A+** y **A-** en la parte superior del panel de decodificación CW le permiten aumentar o disminuir el tamaño de fuente del texto decodificado.

1. Haga clic en **A+** para agrandar el texto; haga clic en **A-** para reducirlo.
2. El tamaño de fuente se conserva entre sesiones. El rango válido es 8–32 px.
3. Use un texto más grande para una mejor legibilidad a distancia; use un texto más pequeño para ver más historial en el panel.

## Redimensionar el panel de decodificación CW

Arrastre la delgada asa horizontal en la parte superior del panel de decodificación CW (justo debajo de la barra de título) hacia arriba o hacia abajo para cambiar la altura del panel. Esto revela más o menos historial de texto decodificado.

1. Mueva el cursor sobre la barra de redimensión de 4 píxeles de alto hasta que se convierta en un cursor de redimensión vertical.
2. Haga clic y arrastre hacia arriba para reducir el panel, o hacia abajo para agrandarlo. El rango válido es 60–600 px.
3. La altura del panel se conserva entre sesiones.

## Consejos

- Comience con el valor predeterminado de 30 y eleve gradualmente el control deslizante hasta que los caracteres rojos y naranjas desaparezcan del texto de decodificación.
- El color de los caracteres es un indicador rápido de confianza: si la mayor parte de la salida es verde, la sensibilidad actual está bien ajustada a las condiciones de la señal. Si la pantalla se queda completamente en blanco, el control deslizante está demasiado alto: muévalo hacia la izquierda hasta que los caracteres regresen.
- El control deslizante de rango de **Pitch** (predeterminado 500–700 Hz, rango 300–1200 Hz) limita los tonos que busca el decodificador. Reducir ese rango para que coincida con el tono de la señal recibida puede reducir las activaciones falsas independientemente de **Sens**.
- El control deslizante de rango de **WPM** (predeterminado 15–40 WPM, rango 5–60 WPM) limita las velocidades que busca el decodificador. Reducir ese rango para que coincida con la velocidad de transmisión de la señal recibida mejora la precisión de la decodificación.
- Al hacer clic derecho en el área de texto de decodificación CW también se accede a las acciones de texto estándar (Seleccionar todo, Copiar, etc.) junto con la opción **Clear**.
- Use **A+** y **A-** para encontrar un tamaño de lectura cómodo. El cambio tiene efecto inmediato y se guarda para la próxima vez.

## Solución de problemas

- **El texto decodificado desaparece por completo después de subir Sens** — el umbral está por encima del nivel de confianza de la señal entrante. Baje el control deslizante hasta que la salida regrese, luego súbalo más lentamente.
- **La salida sigue siendo ruidosa incluso con Sens al 100** — la señal puede estar fuera de la ventana de búsqueda de tono. Verifique la etiqueta de estadísticas CW para el tono informado y ajuste el control deslizante de rango de **Pitch** para abarcarlo.
- **Sens se restablece a 30 después de reiniciar** — si falta `CwDecoderSensitivity` en la configuración guardada, AetherSDR usa el valor predeterminado de 30. Mueva el control deslizante una vez para escribir el valor; luego se guarda en cada cambio.
- **El tamaño de fuente se restablece después de reiniciar** — el tamaño de fuente se guarda automáticamente. Si se restablece, asegúrese de tener permisos de escritura en el archivo de configuración.

## Relacionado

- [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Lock CW decoder pitch or speed once tracking is good](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copy decoded CW text to the clipboard](copy-decoded-cw-text-to-the-clipboard.md)
