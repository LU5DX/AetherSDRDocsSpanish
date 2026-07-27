# Copiar el texto CW descodificado al portapapeles

El panel de descodificación CW dispone de dos botones de portapapeles que permiten capturar el texto Morse descodificado, ya sea todo el búfer de la sesión o solo lo que está visible actualmente en pantalla.

## Antes de empezar

- El panel de descodificación CW debe estar abierto y descodificando activamente. Si no está visible, consulte [Activar el descodificador CW para leer Morse en antena](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio del PC debe enrutarse a AetherSDR. El indicador "(requires PC Audio)" en el panel CW recuerda que la descodificación se detiene sin él.

## Pasos

### Copiar todo el texto descodificado

1. Localice el panel de descodificación CW debajo del espectro del panadapter.
2. Haga clic en `CPY ALL`.

Todo el texto del búfer de descodificación se copia al portapapeles, incluido cualquier texto que se haya desplazado fuera de la pantalla.

### Copiar solo el texto visible

1. Localice el panel de descodificación CW debajo del espectro del panadapter.
2. Desplace el área de descodificación hasta la parte del texto que desee.
3. Haga clic en `CPY VIS`.

Solo se copia el texto actualmente visible en el área de desplazamiento.

### Vaciar el búfer desde el menú contextual

A partir de la versión v0.9.2.1, el área de texto descodificado dispone de un menú contextual. Haga clic con el botón derecho en cualquier lugar del área de texto de descodificación CW para abrirlo. El menú contiene las acciones estándar de edición de texto seguidas de un separador y un elemento **Clear**. Haga clic en **Clear** para borrar el búfer de descodificación. Esto equivale a hacer clic en `CLR`.

### Ajustar el tamaño de fuente del texto descodificado

A partir de la versión v26.7.4, puede aumentar o disminuir el tamaño de fuente del texto CW descodificado para mejorar la legibilidad.

1. Localice los botones `A-` y `A+` en la barra de botones del panel de descodificación CW.
2. Haga clic en `A+` para aumentar el tamaño de fuente.
3. Haga clic en `A-` para disminuir el tamaño de fuente.

El tamaño de fuente se conserva entre sesiones. El rango válido es de 8 a 32 píxeles.

### Cambiar el tamaño del panel de descodificación CW

A partir de la versión v26.7.4, puede arrastrar el borde superior del panel CW para cambiar su altura, revelando más historial de texto descodificado.

1. Pase el cursor sobre el fino control de cambio de tamaño en la parte superior del panel de descodificación CW. El cursor cambia a un cursor de cambio de tamaño vertical.
2. Haga clic y arrastre hacia arriba o hacia abajo para cambiar el tamaño del panel.

La altura del panel se conserva entre sesiones. El rango válido es de 60 a 600 píxeles.

## Qué hace cada control

| Control                         | Qué hace                                                                                             | Por defecto |
|---------------------------------|------------------------------------------------------------------------------------------------------|-------------|
| `CPY ALL`                       | Copia todo el búfer de texto descodificado al portapapeles.                                          | —           |
| `CPY VIS`                       | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles.                | —           |
| `CLR`                           | Borra completamente el búfer de descodificación CW. El texto no se puede recuperar tras borrarlo.   | —           |
| Clic derecho > **Clear**        | Borra el búfer de descodificación CW desde el menú contextual del área de texto. Equivalente a `CLR`. | —           |
| `A-` / `A+` (v26.7.4)          | Disminuye/aumenta el tamaño de fuente del texto descodificado. Conservado por `CwDecodeSettings::fontPx()`. | 13 px       |
| Control de cambio de tamaño (v26.7.4) | Arrastre hacia arriba o abajo para cambiar la altura del panel. Conservado por `CwDecodeSettings::panelHeight()`. | 80 px       |
| Sens                            | Filtra descodificaciones de baja confianza antes de que aparezcan en el búfer. Valores más altos son más estrictos. | 30          |
| 🔒P (Lock Pitch)                | Bloquea la frecuencia del descodificador CW en la frecuencia sintonizada actual.                     | —           |
| 🔒S (Lock Speed)                | Bloquea la velocidad del descodificador CW en las PPM actuales.                                      | —           |
| Deslizador de rango de frecuencia | Deslizador de doble mango que establece el rango de búsqueda de frecuencia del descodificador (Bajo a Alto) en Hz. | 500–700     |
| Deslizador de rango de PPM       | Deslizador de doble mango que establece el rango de búsqueda de velocidad del descodificador (Bajo a Alto) en PPM. | 15–40       |

## Visualización de estadísticas CW

La etiqueta de estadísticas CW muestra la frecuencia y velocidad detectadas en el formato `<hz> Hz  <wpm> WPM`. Estos valores se actualizan en tiempo real a medida que el descodificador procesa las señales.

## Visualización del texto descodificado

El panel de descodificación CW muestra el texto descodificado tanto de la clave recibida (RX) como de la transmitida (TX) en una única visualización continua. El texto está codificado por colores para que pueda distinguir el Morse entrante de su propio envío:

| Color   | Significado                                                        |
|---------|--------------------------------------------------------------------|
| Verde   | Texto RX con alta confianza (coste < 0,15)                        |
| Amarillo| Texto RX con confianza moderada (coste < 0,35)                    |
| Naranja | Texto RX con confianza más baja (coste < 0,60)                    |
| Rojo    | Texto RX con la confianza más baja (coste >= 0,60)                |
| Cian    | Texto TX (su propio envío): cualquier nivel de confianza           |

Se inserta automáticamente un espacio separador cuando la visualización cambia entre tramos de texto TX y RX para que los dos bloques de color no se fusionen visualmente.

## Consejos

- Use `CPY VIS` cuando desee solo un intercambio o indicativo específico que esté visible en pantalla, sin el ruido de la sesión circundante.
- Use `CPY ALL` al registrar un QSO completo o guardar una sesión de descodificación completa.
- Haga clic en `CLR` (o haga clic derecho en el área de texto y elija **Clear**) antes de un nuevo QSO para mantener el búfer relevante. Tenga en cuenta que borrar el búfer también elimina el texto que `CPY ALL` habría capturado.
- El texto RX descodificado está codificado por colores según la confianza: el verde es la confianza más alta, seguido de amarillo, naranja y rojo. El texto TX (su propio envío) aparece en cian. Subir el deslizador Sens suprime los caracteres rojos y naranjas del búfer. Consulte [Ajustar la sensibilidad del descodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md).
- Use el deslizador de rango de frecuencia (deslizador de doble mango integrado etiquetado como "Pitch") para limitar la búsqueda de frecuencia del descodificador. Coloque el mango izquierdo para la frecuencia mínima y el mango derecho para la frecuencia máxima. El rango predeterminado es 500–700 Hz.
- Use el deslizador de rango de PPM (deslizador de doble mango integrado etiquetado como "WPM") para restringir la búsqueda de velocidad del descodificador. El rango predeterminado es 15–40 PPM.
- Los botones Lock Pitch (`🔒P`) y Lock Speed (`🔒S`) le permiten congelar los valores detectados actuales para que el descodificador ya no ajuste la frecuencia o la velocidad aunque la señal varíe.
- Use `A+` y `A-` para ajustar la fuente del texto descodificado para una mejor legibilidad, especialmente en ventanas de panadapter pequeñas.
- Arrastre el control de cambio de tamaño en la parte superior del panel CW para mostrar más historial de texto descodificado sin necesidad de desplazarse.

## Relacionados

- [Activar el descodificador CW para leer Morse en antena](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del descodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear la frecuencia o velocidad del descodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
