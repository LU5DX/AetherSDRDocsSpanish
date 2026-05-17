# Copiar el texto CW descodificado al portapapeles

El panel de descodificación CW proporciona dos botones de portapapeles que le permiten capturar el texto Morse descodificado — ya sea el búfer completo de la sesión o solo lo que está visible actualmente en pantalla.

## Antes de empezar

- El panel de descodificación CW debe estar abierto y descodificando activamente. Si no está visible, consulte [Activar el descodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio del PC debe estar enrutado a AetherSDR. El indicador "(requires PC Audio)" en el panel CW recuerda que la descodificación se detiene sin él.

## Pasos

### Copiar todo el texto descodificado

1. Localice el panel de descodificación CW debajo del espectro del panadapter.
2. Haga clic en `CPY ALL`.

Todo el texto del búfer de descodificación se copia al portapapeles, incluyendo cualquier texto que se haya desplazado fuera de la pantalla.

### Copiar solo el texto visible

1. Localice el panel de descodificación CW debajo del espectro del panadapter.
2. Desplace el área de descodificación hasta la porción de texto que desee.
3. Haga clic en `CPY VIS`.

Solo se copia el texto actualmente visible en el área de desplazamiento.

### Vaciar el búfer desde el menú contextual

A partir de la v0.9.2.1, el área de texto descodificado tiene un menú contextual. Haga clic derecho en cualquier lugar del área de texto de descodificación CW para abrirlo. El menú contiene las acciones estándar de edición de texto seguidas de un separador y un elemento **Clear**. Haga clic en **Clear** para borrar el búfer de descodificación. Esto equivale a hacer clic en `CLR`.

## Qué hace cada control

| Control                 | Qué hace                                                                                       | Por defecto |
|-------------------------|------------------------------------------------------------------------------------------------|-------------|
| `CPY ALL`               | Copia el búfer completo de texto descodificado al portapapeles.                                | —           |
| `CPY VIS`               | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles.          | —           |
| `CLR`                   | Vacía completamente el búfer de descodificación CW. El texto no se puede recuperar después.    | —           |
| Clic derecho > **Clear**| Vacía el búfer de descodificación CW desde el menú contextual del área de texto. Equivale a `CLR`. | —       |
| Sens                    | Filtra las descodificaciones de baja confianza antes de que aparezcan en el búfer. Valores más altos son más estrictos. | 30 |

## Visualización del texto descodificado

El panel de descodificación CW muestra el texto descodificado tanto de la manipulación recibida (RX) como de la transmitida (TX) en una única visualización continua. El texto está codificado por colores para que pueda distinguir el Morse entrante de su propia emisión:

| Color       | Significado                                                             |
|-------------|-------------------------------------------------------------------------|
| Verde       | Texto RX con alta confianza (coste < 0.15)                              |
| Amarillo    | Texto RX con confianza moderada (coste < 0.35)                          |
| Naranja     | Texto RX con menor confianza (coste < 0.60)                             |
| Rojo        | Texto RX con la confianza más baja (coste >= 0.60)                      |
| Cian        | Texto TX (su propia emisión) — cualquier nivel de confianza             |

Se inserta automáticamente un espacio separador cuando la visualización cambia entre bloques de texto TX y RX para que los dos bloques de color no se fusionen visualmente.

## Consejos

- Use `CPY VIS` cuando solo desee un intercambio o indicativo específico que esté visible en pantalla, sin el ruido de la sesión circundante.
- Use `CPY ALL` cuando registre un QSO completo o guarde una sesión de descodificación completa.
- Haga clic en `CLR` (o haga clic derecho en el área de texto y elija **Clear**) antes de un nuevo QSO para mantener el búfer relevante. Tenga en cuenta que vaciar el búfer también elimina el texto que `CPY ALL` habría capturado.
- El texto RX descodificado está codificado por colores según la confianza: verde es la confianza más alta, luego amarillo, naranja y rojo. El texto TX (su propia emisión) aparece en cian. Subir el control deslizante Sens suprime que los caracteres rojos y naranjas aparezcan en el búfer. Consulte [Ajustar la sensibilidad del descodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md).

## Relacionado

- [Activar el descodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del descodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del descodificador CW una vez que el seguimiento sea bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
