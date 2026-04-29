# Copiar el texto CW decodificado al portapapeles

El panel de decodificación CW proporciona dos botones de portapapeles que permiten capturar el texto Morse decodificado: ya sea el búfer completo de la sesión o solo lo que se muestra en pantalla en ese momento.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto y decodificando activamente. Si no está visible, consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio del PC debe estar dirigido a AetherSDR. El indicador "(requires PC Audio)" en el panel CW es un recordatorio de que la decodificación se detiene sin él.

## Pasos

### Copiar todo el texto decodificado

1. Localice el panel de decodificación CW debajo del espectro del panadapter.
2. Haga clic en `CPY ALL`.

Todo el texto del búfer de decodificación se copia al portapapeles, incluido el texto que haya salido de la pantalla al desplazarse.

### Copiar solo el texto visible

1. Localice el panel de decodificación CW debajo del espectro del panadapter.
2. Desplácese por el área de decodificación hasta la parte del texto que desea.
3. Haga clic en `CPY VIS`.

Solo se copia el texto visible actualmente en el área de desplazamiento.

### Limpiar el búfer desde el menú contextual

A partir de la v0.9.2.1, el área de texto decodificado dispone de un menú contextual. Haga clic derecho en cualquier parte del área de texto CW decodificado para abrirlo. El menú contiene las acciones estándar de edición de texto, seguidas de un separador y un elemento **Clear**. Haga clic en **Clear** para borrar el búfer de decodificación. Esto equivale a hacer clic en `CLR`.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| `CPY ALL` | Copia el búfer completo de texto decodificado al portapapeles. | — | — | — |
| `CPY VIS` | Copia al portapapeles solo el texto visible actualmente en el área de desplazamiento. | — | — | — |
| `CLR` | Borra completamente el búfer de decodificación CW. El texto no puede recuperarse después de borrado. | — | — | — |
| Clic derecho > **Clear** | Borra el búfer de decodificación CW desde el menú contextual del área de texto. Equivalente a `CLR`. | — | — | — |
| Sens | Filtra las decodificaciones de baja confianza antes de que aparezcan en el búfer. Los valores más altos son más estrictos. | 30 | 0–100 | `CwDecoderSensitivity` |

## Consejos

- Use `CPY VIS` cuando desee únicamente un intercambio específico o un indicativo que esté visible en pantalla, sin el ruido de sesión circundante.
- Use `CPY ALL` al registrar un QSO completo o al guardar una sesión de decodificación completa.
- Haga clic en `CLR` (o haga clic derecho en el área de texto y elija **Clear**) antes de un nuevo QSO para mantener el búfer relevante. Tenga en cuenta que limpiar el búfer también elimina el texto que `CPY ALL` habría capturado.
- El texto decodificado tiene código de color según el nivel de confianza: verde es el mayor nivel de confianza, seguido de amarillo, naranja y rojo. Subir el control deslizante Sens suprime la aparición de caracteres rojos y naranjas en el búfer. Consulte [Ajustar la sensibilidad del decodificador CW para rechazar el ruido](tune-cw-decoder-sensitivity-to-reject-noise.md).

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar el ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
