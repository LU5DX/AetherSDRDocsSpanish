# Copiar el texto CW decodificado al portapapeles

El panel de decodificación CW ofrece dos botones de portapapeles que permiten capturar el texto Morse decodificado — ya sea el búfer completo de la sesión o únicamente lo que está visible en pantalla en ese momento.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto y decodificando activamente. Si no está visible, consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio del PC debe estar enrutado a AetherSDR. El indicador "(requires PC Audio)" en el panel CW es un recordatorio de que la decodificación se detiene sin él.

## Pasos

### Copiar todo el texto decodificado

1. Localice el panel de decodificación CW debajo del espectro del panadapter.
2. Haga clic en `CPY ALL`.

Todo el texto del búfer de decodificación se copia al portapapeles, incluido el texto que haya quedado fuera de la pantalla al desplazarse.

### Copiar solo el texto visible

1. Localice el panel de decodificación CW debajo del espectro del panadapter.
2. Desplace el área de decodificación hasta la parte del texto que desee.
3. Haga clic en `CPY VIS`.

Solo se copia el texto visible en ese momento en el área de desplazamiento.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| `CPY ALL` | Copia el búfer completo de texto decodificado al portapapeles. | — | — | — |
| `CPY VIS` | Copia al portapapeles solo el texto visible en el área de desplazamiento. | — | — | — |
| `CLR` | Borra completamente el búfer de decodificación CW. El texto no puede recuperarse tras borrado. | — | — | — |
| Sens | Filtra las decodificaciones de baja confianza antes de que aparezcan en el búfer. Valores más altos son más estrictos. | 30 | 0–100 | `CwDecoderSensitivity` |

## Consejos

- Use `CPY VIS` cuando quiera capturar únicamente un intercambio o indicativo específico visible en pantalla, sin el ruido del resto de la sesión.
- Use `CPY ALL` para registrar un QSO completo o guardar una sesión de decodificación íntegra.
- Haga clic en `CLR` antes de un nuevo QSO para mantener el búfer relevante. Tenga en cuenta que borrar el búfer también elimina el texto que `CPY ALL` habría capturado.
- El texto decodificado tiene código de color según la confianza: verde indica la mayor confianza, seguido de amarillo, naranja y rojo. Subir el control deslizante Sens suprime los caracteres rojos y naranjas para que no aparezcan en el búfer. Consulte [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md).

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
