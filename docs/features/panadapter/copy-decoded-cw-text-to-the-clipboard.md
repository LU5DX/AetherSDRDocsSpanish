# Copiar el texto de CW descodificado al portapapeles

El panel de descodificación de CW dispone de dos botones de portapapeles que permiten capturar el texto Morse descodificado — ya sea todo el búfer de la sesión o solo lo que está visible en pantalla.

## Antes de comenzar

- El panel de descodificación de CW debe estar abierto y descodificando activamente. Si no está visible, consulte [Activar el descodificador de CW para leer Morse de antena](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio del PC debe estar enrutado a AetherSDR. El indicador "(requires PC Audio)" en el panel de CW recuerda que la descodificación se detiene sin él.

## Pasos

### Copiar todo el texto descodificado

1. Localice el panel de descodificación de CW debajo del espectro del panadapter.
2. Haga clic en `CPY ALL`.

Todo el texto del búfer de descodificación se copia al portapapeles, incluido cualquier texto que se haya desplazado fuera de la pantalla.

### Copiar solo el texto visible

1. Localice el panel de descodificación de CW debajo del espectro del panadapter.
2. Desplace el área de descodificación hasta la porción de texto que desee.
3. Haga clic en `CPY VIS`.

Solo se copia el texto actualmente visible en el área de desplazamiento.

### Vaciar el búfer desde el menú contextual

A partir de la v0.9.2.1, el área de texto descodificado tiene un menú contextual. Haga clic derecho en cualquier lugar del área de texto de descodificación de CW para abrirlo. El menú contiene las acciones estándar de edición de texto seguidas de un separador y un elemento **Clear**. Haga clic en **Clear** para borrar el búfer de descodificación. Esto equivale a hacer clic en `CLR`.

## Qué hace cada control

| Control                 | Qué hace                                                                                     | Por defecto |
|-------------------------|----------------------------------------------------------------------------------------------|-------------|
| `CPY ALL`               | Copia todo el búfer de texto descodificado al portapapeles.                                  | —           |
| `CPY VIS`               | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles.        | —           |
| `CLR`                   | Vacía completamente el búfer de descodificación de CW. El texto no se puede recuperar tras el borrado. | —           |
| Clic derecho > **Clear**| Vacía el búfer de descodificación de CW desde el menú contextual del área de texto. Equivale a `CLR`. | —           |
| Sens                    | Filtra las descodificaciones de baja confianza antes de que aparezcan en el búfer. Valores más altos son más estrictos. | 30      |
| 🔒P (Lock Pitch)        | Bloquea el tono del descodificador de CW en la frecuencia sintonizada actual.                 | —           |
| 🔒S (Lock Speed)        | Bloquea la velocidad del descodificador de CW en las PPM actuales.                           | —           |
| Deslizador de rango de tono | Deslizador de doble control que establece el rango de búsqueda de tono del descodificador (Mín a Máx) en Hz. | 500–700 |
| Deslizador de rango de PPM  | Deslizador de doble control que establece el rango de búsqueda de velocidad del descodificador (Mín a Máx) en PPM. | 15–40   |

## Visualización de estadísticas de CW

La etiqueta de estadísticas de CW muestra el tono y la velocidad detectados en el formato `<hz> Hz  <wpm> PPM`. Estos valores se actualizan en tiempo real a medida que el descodificador procesa las señales.

## Visualización del texto descodificado

El panel de descodificación de CW muestra el texto descodificado tanto de la recepción (RX) como de la transmisión (TX) en una única visualización continua. El texto está codificado por colores para que pueda distinguir el Morse entrante de su propio envío:

| Color       | Significado                                                              |
|--------------|--------------------------------------------------------------------------|
| Verde        | Texto RX con alta confianza (coste < 0,15)                               |
| Amarillo     | Texto RX con confianza moderada (coste < 0,35)                           |
| Naranja      | Texto RX con confianza baja (coste < 0,60)                               |
| Rojo         | Texto RX con confianza muy baja (coste >= 0,60)                          |
| Cian         | Texto TX (su propio envío) — cualquier nivel de confianza                |

Se inserta automáticamente un espacio separador cuando la visualización cambia entre tramos de texto TX y RX para que los dos bloques de color no se fusionen visualmente.

## Consejos

- Use `CPY VIS` cuando desee solo un intercambio o indicativo específico que esté visible en pantalla, sin el ruido de la sesión circundante.
- Use `CPY ALL` al registrar un QSO completo o guardar una sesión de descodificación completa.
- Haga clic en `CLR` (o haga clic derecho en el área de texto y elija **Clear**) antes de un nuevo QSO para mantener el búfer relevante. Tenga en cuenta que vaciar el búfer también elimina el texto que `CPY ALL` habría capturado.
- El texto RX descodificado está codificado por colores según la confianza: verde es la confianza más alta, luego amarillo, naranja y rojo. El texto TX (su propio envío) aparece en cian. Aumentar el deslizador Sens suprime la aparición de caracteres rojos y naranjas en el búfer. Consulte [Ajustar la sensibilidad del descodificador de CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md).
- Use el deslizador de rango de tono (deslizador de doble control integrado etiquetado "Pitch") para reducir la búsqueda de frecuencia del descodificador. Ajuste el control izquierdo para el tono mínimo y el control derecho para el tono máximo. El rango predeterminado es 500–700 Hz.
- Use el deslizador de rango de PPM (deslizador de doble control integrado etiquetado "WPM") para limitar la búsqueda de velocidad del descodificador. El rango predeterminado es 15–40 PPM.
- Los botones Lock Pitch (`🔒P`) y Lock Speed (`🔒S`) permiten congelar los valores detectados actualmente para que el descodificador ya no ajuste el tono o la velocidad aunque la señal varíe.

## Relacionados

- [Activar el descodificador de CW para leer Morse de antena](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del descodificador de CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del descodificador de CW una vez que el seguimiento es bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
