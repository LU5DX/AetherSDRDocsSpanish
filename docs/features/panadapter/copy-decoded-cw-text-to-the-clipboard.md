# Copiar el texto CW decodificado al portapapeles

El panel de decodificación CW dispone de dos botones de portapapeles que permiten capturar el texto Morse decodificado, ya sea todo el búfer de la sesión o solo lo que está visible en pantalla.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto y decodificando activamente. Si no está visible, consulte [Activar el decodificador CW para leer Morse de la recepción](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio del PC debe estar enrutado a AetherSDR. El indicador "(requires PC Audio)" en el panel CW recuerda que la decodificación se detiene sin él.

## Pasos

### Copiar todo el texto decodificado

1. Localice el panel de decodificación CW debajo del espectro del panadapter.
2. Haga clic en `CPY ALL`.

Todo el texto del búfer de decodificación se copia al portapapeles, incluyendo cualquier texto que haya salido de la pantalla.

### Copiar solo el texto visible

1. Localice el panel de decodificación CW debajo del espectro del panadapter.
2. Desplace el área de decodificación hasta la porción de texto que desee.
3. Haga clic en `CPY VIS`.

Solo el texto actualmente visible en el área de desplazamiento se copia.

### Limpiar el búfer mediante el menú contextual

A partir de v0.9.2.1, el área de texto decodificado tiene un menú contextual. Haga clic derecho en cualquier lugar del área de texto decodificado CW para abrirlo. El menú contiene las acciones estándar de edición de texto seguidas de un separador y un elemento **Clear**. Haga clic en **Clear** para borrar el búfer de decodificación. Esto equivale a hacer clic en `CLR`.

## Función de cada control

| Control                 | Función                                                                                                | Valor predeterminado |
|-------------------------|--------------------------------------------------------------------------------------------------------|----------------------|
| `CPY ALL`               | Copia todo el búfer de texto decodificado al portapapeles.                                             | —                    |
| `CPY VIS`               | Copia solo el texto actualmente visible en el área de desplazamiento al portapapeles.                  | —                    |
| `CLR`                   | Limpia por completo el búfer de decodificación CW. El texto no se puede recuperar después de limpiarlo.| —                    |
| Clic derecho > **Clear**| Limpia el búfer de decodificación CW desde el menú contextual del área de texto. Equivalente a `CLR`. | —                    |
| Sens                    | Filtra las decodificaciones de baja confianza antes de que aparezcan en el búfer. Valores más altos son más estrictos. | 30 |

## Visualización del texto decodificado

El panel de decodificación CW muestra el texto decodificado tanto de la recepción (RX) como de la transmisión (TX) en una sola visualización continua. El texto está codificado por colores para que pueda distinguir el Morse entrante de su propia emisión:

| Color      | Significado                                                        |
|------------|-------------------------------------------------------------------|
| Verde      | Texto RX con alta confianza (costo < 0.15)                        |
| Amarillo   | Texto RX con confianza moderada (costo < 0.35)                    |
| Naranja    | Texto RX con confianza baja (costo < 0.60)                        |
| Rojo       | Texto RX con confianza muy baja (costo >= 0.60)                   |
| Cian       | Texto TX (su propia emisión) — cualquier nivel de confianza       |

Se inserta automáticamente un espacio separador cuando la visualización cambia entre tramos de texto TX y RX para que los dos bloques de colores no se fusionen visualmente.

## Consejos

- Use `CPY VIS` cuando desee solo un intercambio o indicativo específico que esté visible en pantalla, sin el ruido circundante de la sesión.
- Use `CPY ALL` cuando registre un QSO completo o guarde una sesión de decodificación completa.
- Haga clic en `CLR` (o haga clic derecho en el área de texto y elija **Clear**) antes de un nuevo QSO para mantener el búfer actualizado. Tenga en cuenta que limpiar el búfer también elimina el texto que `CPY ALL` habría capturado.
- El texto RX decodificado está codificado por colores según la confianza: verde es la confianza más alta, luego amarillo, naranja y rojo. El texto TX (su propia emisión) aparece en cian. Aumentar el control deslizante Sens suprime la aparición de caracteres rojos y naranjas en el búfer. Consulte [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md).

## Relacionados

- [Activar el decodificador CW para leer Morse de la recepción](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
