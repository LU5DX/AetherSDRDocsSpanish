# Copiar el texto CW decodificado al portapapeles

El panel de decodificación CW ofrece dos botones de copia que permiten transferir el texto Morse decodificado al portapapeles del sistema: ya sea el historial completo de decodificación o únicamente el texto visible en pantalla en ese momento.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto y decodificando activamente. Si no está visible, consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio del PC debe estar enrutado hacia AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio si el audio no está fluyendo.

## Pasos

1. Localice el panel de decodificación CW debajo del espectro panadapter y el waterfall.
2. Elija qué texto copiar:
   - Para copiar todo el contenido del búfer de decodificación, haga clic en `CPY ALL`.
   - Para copiar únicamente el texto visible en el área de desplazamiento, haga clic en `CPY VIS`.
3. Pegue en cualquier aplicación usando el comando de pegado estándar de su sistema.

Para eliminar todo el texto decodificado del búfer después de copiar, haga clic en `CLR`.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| `CPY ALL` | Copia el búfer completo de texto decodificado al portapapeles. | — | — | — |
| `CPY VIS` | Copia únicamente el texto visible en el área de desplazamiento al portapapeles. | — | — | — |
| `CLR` | Borra el búfer de decodificación CW. No afecta el portapapeles. | — | — | — |
| Sens | Filtra decodificaciones de baja confianza; valores más altos rechazan más caracteres inciertos. | 30 | 0–100 | `CwDecoderSensitivity` |

## Consejos

- El texto en el panel de decodificación está codificado por colores según el nivel de confianza. Los caracteres mostrados en rojo representan las decodificaciones de menor confianza y pueden contener errores. Si la precisión es importante, copie después de ajustar el control deslizante Sens hacia valores más altos para suprimir las decodificaciones deficientes — consulte [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md).
- `CPY VIS` resulta útil cuando ha desplazado la vista hacia una parte específica de un QSO y desea copiar únicamente ese fragmento al portapapeles.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Bloquear el tono o la velocidad del decodificador CW cuando el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
