# Copiar texto CW decodificado al portapapeles

El panel de decodificación CW proporciona dos botones de portapapeles que le permiten capturar texto Morse decodificado — ya sea todo el búfer de sesión o solo lo que está actualmente visible en pantalla.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto y decodificando activamente. Si no es visible, consulte [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio de PC debe enrutarse a AetherSDR. El indicador "(requires PC Audio)" en el panel CW es un recordatorio de que la decodificación se detiene sin él.

## Pasos

### Copiar todo el texto decodificado

1. Localice el panel de decodificación CW debajo del espectro panadapter.
2. Haga clic en `CPY ALL`.

Todo el texto en el búfer de decodificación se copia al portapapeles, incluido cualquier texto que se haya desplazado fuera de pantalla.

### Copiar solo el texto visible

1. Localice el panel de decodificación CW debajo del espectro panadapter.
2. Desplace el área de decodificación a la porción de texto que desea.
3. Haga clic en `CPY VIS`.

Solo el texto actualmente visible en el área de desplazamiento se copia.

### Limpiar el búfer desde el menú contextual

A partir de la v0.9.2.1, el área de texto decodificado tiene un menú contextual. Haga clic derecho en cualquier lugar del área de texto de decodificación CW para abrirlo. El menú contiene las acciones estándar de edición de texto seguidas de un separador y un elemento **Clear**. Haga clic en **Clear** para borrar el búfer de decodificación. Esto es equivalente a hacer clic en `CLR`.

## Qué hace cada control

| Control                 | Qué hace                                                                                     | Predeterminado |
|-------------------------|----------------------------------------------------------------------------------------------|----------------|
| `CPY ALL`               | Copia el búfer de texto decodificado completo al portapapeles.                              | —              |
| `CPY VIS`               | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles.       | —              |
| `CLR`                   | Borra completamente el búfer de decodificación CW. El texto no se puede recuperar después. | —              |
| Clic derecho > **Clear** | Borra el búfer de decodificación CW desde el menú contextual del área de texto. Equivalente a `CLR`. | —              |
| Sens                    | Filtra las decodificaciones de baja confianza antes de que aparezcan en el búfer. Los valores más altos son más estrictos. | 30             |

## Consejos

- Use `CPY VIS` cuando desee solo un intercambio específico o indicativo visible en pantalla, sin el ruido de sesión circundante.
- Use `CPY ALL` cuando registre un QSO completo o guarde una sesión de decodificación completa.
- Haga clic en `CLR` (o haga clic derecho en el área de texto y elija **Clear**) antes de un QSO nuevo para mantener el búfer relevante. Tenga en cuenta que limpiar el búfer también elimina el texto que `CPY ALL` habría capturado.
- El texto decodificado está codificado por colores según la confianza: verde es la confianza más alta, seguido de amarillo, naranja y rojo. Aumentar el regulador Sens suprime los caracteres rojo y naranja de aparición en el búfer. Consulte [Tune CW decoder sensitivity to reject noise](tune-cw-decoder-sensitivity-to-reject-noise.md).

## Relacionado

- [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Tune CW decoder sensitivity to reject noise](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Lock CW decoder pitch or speed once tracking is good](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
