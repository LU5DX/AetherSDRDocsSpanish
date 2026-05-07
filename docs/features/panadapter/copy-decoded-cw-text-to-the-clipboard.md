# Copiar el texto de CW descodificado al portapapeles

El panel de descodificación de CW proporciona dos botones de portapapeles que le permiten capturar el texto Morse descodificado — ya sea todo el búfer de la sesión o solo lo que está visible actualmente en pantalla.

## Antes de empezar

- El panel de descodificación de CW debe estar abierto y descodificando activamente. Si no está visible, consulte [Activar el descodificador de CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio del PC debe estar enrutado a AetherSDR. El indicador "(requires PC Audio)" en el panel de CW recuerda que la descodificación se detiene sin él.

## Pasos

### Copiar todo el texto descodificado

1. Localice el panel de descodificación de CW debajo del espectro del panadapter.
2. Haga clic en `CPY ALL`.

Todo el texto del búfer de descodificación se copia al portapapeles, incluyendo cualquier texto que se haya desplazado fuera de la pantalla.

### Copiar solo el texto visible

1. Localice el panel de descodificación de CW debajo del espectro del panadapter.
2. Desplace el área de descodificación hasta la porción de texto que desea.
3. Haga clic en `CPY VIS`.

Solo el texto actualmente visible en el área de desplazamiento se copia.

### Limpiar el búfer desde el menú contextual

A partir de la v0.9.2.1, el área de texto descodificado tiene un menú contextual. Haga clic con el botón derecho en cualquier lugar del área de texto de descodificación de CW para abrirlo. El menú contiene las acciones de edición de texto estándar seguidas de un separador y un elemento **Clear**. Haga clic en **Clear** para borrar el búfer de descodificación. Esto equivale a hacer clic en `CLR`.

## Qué hace cada control

| Control                 | Qué hace                                                                                     | Predeterminado |
|-------------------------|----------------------------------------------------------------------------------------------|----------------|
| `CPY ALL`               | Copia el búfer completo de texto descodificado al portapapeles.                              | —              |
| `CPY VIS`               | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles.        | —              |
| `CLR`                   | Limpia completamente el búfer de descodificación de CW. El texto no se puede recuperar después de limpiarlo. | —              |
| Clic derecho > **Clear**| Limpia el búfer de descodificación de CW desde el menú contextual del área de texto. Equivale a `CLR`. | —              |
| Sens                    | Filtra las descodificaciones de baja confianza antes de que aparezcan en el búfer. Valores más altos son más estrictos. | 30             |

## Consejos

- Use `CPY VIS` cuando desee solo un intercambio específico o un indicativo visible en pantalla, sin el ruido de la sesión circundante.
- Use `CPY ALL` al registrar un QSO completo o guardar una sesión de descodificación completa.
- Haga clic en `CLR` (o haga clic con el botón derecho en el área de texto y elija **Clear**) antes de un nuevo QSO para mantener el búfer relevante. Tenga en cuenta que limpiar el búfer también elimina el texto que `CPY ALL` habría capturado.
- El texto descodificado está codificado por colores según la confianza: verde es la confianza más alta, luego amarillo, naranja y rojo. Aumentar el control deslizante Sens suprime los caracteres rojos y naranjas para que no aparezcan en el búfer. Consulte [Ajustar la sensibilidad del descodificador de CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md).

## Relacionados

- [Activar el descodificador de CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del descodificador de CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del descodificador de CW una vez que el seguimiento sea bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
