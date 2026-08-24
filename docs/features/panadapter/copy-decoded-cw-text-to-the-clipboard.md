# Copiar texto CW decodificado al portapapeles

El panel de decodificación CW proporciona dos botones de portapapeles que le permiten capturar texto Morse decodificado — ya sea todo el búfer de la sesión o solo lo que está actualmente visible en pantalla.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto y decodificando activamente. Si no está visible, consulte [Activar el decodificador CW para leer Morse al aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio de la PC debe estar enrutado a AetherSDR. El indicador "(requires PC Audio)" en el panel CW es un recordatorio de que la decodificación se detiene sin él.

## Pasos

### Copiar todo el texto decodificado

1. Localice el panel de decodificación CW debajo del espectro del panadapter.
2. Haga clic en `CPY ALL`.

Todo el texto en el búfer de decodificación se copia al portapapeles, incluido cualquier texto que se haya desplazado fuera de la pantalla.

### Copiar solo el texto visible

1. Localice el panel de decodificación CW debajo del espectro del panadapter.
2. Desplace el área de decodificación hasta la porción de texto que desee.
3. Haga clic en `CPY VIS`.

Solo se copia el texto actualmente visible en el área de desplazamiento.

### Borrar el búfer desde el menú contextual

A partir de la v0.9.2.1, el área de texto decodificado tiene un menú contextual. Haga clic derecho en cualquier parte del área de texto de decodificación CW para abrirlo. El menú contiene las acciones estándar de edición de texto seguidas de un separador y un elemento **Clear**. Haga clic en **Clear** para borrar el búfer de decodificación. Esto equivale a hacer clic en `CLR`.

### Ajustar el tamaño de fuente del texto decodificado

A partir de la v26.7.4, puede aumentar o disminuir el tamaño de fuente del texto CW decodificado para una mejor legibilidad.

1. Localice los botones `A-` y `A+` en la barra de botones del panel de decodificación CW.
2. Haga clic en `A+` para aumentar el tamaño de fuente.
3. Haga clic en `A-` para disminuir el tamaño de fuente.

El tamaño de fuente se conserva entre sesiones. El rango válido es de 8 a 32 píxeles.

### Redimensionar el panel de decodificación CW

A partir de la v26.7.4, puede arrastrar el borde superior del panel CW para cambiar su altura, revelando más historial de texto decodificado.

1. Pase el cursor sobre la delgada empuñadura de redimensionamiento en la parte superior del panel de decodificación CW. El cursor cambia a un cursor de redimensionamiento vertical.
2. Haga clic y arrastre hacia arriba o hacia abajo para redimensionar el panel.

La altura del panel se conserva entre sesiones. El rango válido es de 60 a 600 píxeles.

## Qué hace cada control

| Control                  | Qué hace                                                                                      | Predeterminado |
|--------------------------|-----------------------------------------------------------------------------------------------|----------------|
| `CPY ALL`                | Copia el búfer completo de texto decodificado al portapapeles.                                | —              |
| `CPY VIS`                | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles.          | —              |
| `CLR`                    | Borra por completo el búfer de decodificación CW. El texto no se puede recuperar después de borrarlo. | —          |
| Clic derecho > **Clear** | Borra el búfer de decodificación CW desde el menú contextual del área de texto. Equivale a `CLR`. | —            |
| `A-` / `A+` (v26.7.4)    | Disminuye/aumenta el tamaño de fuente del texto decodificado. Se conserva mediante `CwDecodeSettings::fontPx()`. | 13 px |
| Empuñadura de redimensionamiento (v26.7.4) | Arrastre hacia arriba o hacia abajo para cambiar la altura del panel. Se conserva mediante `CwDecodeSettings::panelHeight()`. | 80 px |
| Sens                    | Filtra decodificaciones de baja confianza antes de que aparezcan en el búfer. Valores más altos son más estrictos. | 30   |
| 🔒P (Lock Pitch)         | Bloquea el tono del decodificador CW a la frecuencia sintonizada actual.                      | —              |
| 🔒S (Lock Speed)         | Bloquea la velocidad del decodificador CW a las PPM actuales.                                 | —              |
| Control deslizante de rango de tono | Control deslizante de doble manija que establece el rango de búsqueda de tono del decodificador (Lo a Hi) en Hz. | 500–700 |
| Control deslizante de rango de PPM | Control deslizante de doble manija que establece el rango de búsqueda de velocidad del decodificador (Lo a Hi) en PPM. | 15–40 |

## Visualización de estadísticas CW

La etiqueta de estadísticas CW muestra el tono y la velocidad detectados en el formato `<hz> Hz  <wpm> WPM`. Estos valores se actualizan en tiempo real a medida que el decodificador procesa las señales.

## Visualización de texto decodificado

El panel de decodificación CW muestra el texto decodificado tanto de la telegrafía recibida (RX) como de la transmitida (TX) en una sola visualización dinámica. El texto está codificado por colores para que pueda distinguir el Morse entrante de su propio envío:

| Color   | Significado                                                              |
|---------|--------------------------------------------------------------------------|
| Verde   | Texto RX con alta confianza (costo < 0.15)                               |
| Amarillo| Texto RX con confianza moderada (costo < 0.35)                           |
| Naranja | Texto RX con confianza más baja (costo < 0.60)                           |
| Rojo    | Texto RX con la confianza más baja (costo >= 0.60)                       |
| Cian    | Texto TX (su propio envío) — cualquier nivel de confianza                |

Se inserta automáticamente un espacio separador cuando la visualización cambia entre secuencias de texto TX y RX para que los dos bloques de colores no se fusionen visualmente.

## Barra de título del panadapter y arrastre en el lienzo

Cuando el panadapter está alojado en el lienzo del espacio de trabajo (nuevo en v26.8.4), la barra de título (nombre accesible "panTitleBar") admite arrastrar para mover como un gesto en vivo. Un clic (movimiento inferior a 6 px antes de soltar) activa el panadapter; una presión seguida de movimiento más allá de 6 px comienza un arrastre que mueve el panadapter en el lienzo. El botón de ventana emergente permanece visible para los elementos del lienzo incluso en modo de un solo panadapter. Fuera del lienzo, la visibilidad del botón vuelve al comportamiento estándar de un solo panadapter.

## Consejos

- Use `CPY VIS` cuando desee solo un intercambio específico o indicativo que esté visible en pantalla, sin el ruido circundante de la sesión.
- Use `CPY ALL` al registrar un QSO completo o guardar una sesión de decodificación completa.
- Haga clic en `CLR` (o haga clic derecho en el área de texto y elija **Clear**) antes de un nuevo QSO para mantener el búfer relevante. Tenga en cuenta que borrar el búfer también elimina el texto que `CPY ALL` habría capturado.
- El texto RX decodificado está codificado por colores según la confianza: el verde es la confianza más alta, luego amarillo, naranja y rojo. El texto TX (su propio envío) aparece en cian. Aumentar el control deslizante Sens suprime que los caracteres rojos y naranjas aparezcan en el búfer. Consulte [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md).
- Use el control deslizante de rango de tono (control deslizante de doble manija integrado etiquetado "Pitch") para reducir la búsqueda de frecuencia del decodificador. Establezca la manija izquierda para el tono mínimo y la manija derecha para el tono máximo. El rango predeterminado es 500–700 Hz.
- Use el control deslizante de rango de PPM (control deslizante de doble manija integrado etiquetado "WPM") para limitar la búsqueda de velocidad del decodificador. El rango predeterminado es 15–40 PPM.
- Los botones Lock Pitch (`🔒P`) y Lock Speed (`🔒S`) le permiten congelar los valores detectados actuales para que el decodificador ya no ajuste el tono o la velocidad incluso si la señal varía.
- Use `A+` y `A-` para ajustar la fuente del texto decodificado para una mejor legibilidad, especialmente en ventanas pequeñas del panadapter.
- Arrastre la empuñadura de redimensionamiento en la parte superior del panel CW para mostrar más historial de texto decodificado sin desplazarse.

## Relacionados

- [Activar el decodificador CW para leer Morse al aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento sea bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
