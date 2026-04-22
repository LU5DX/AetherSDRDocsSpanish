# Copiar texto CW decodificado al portapapeles

Use los botones de copia del panel de decodificación CW para capturar texto Morse decodificado en el portapapeles del sistema — ya sea el historial completo de decodificación o solo el texto visible actualmente en pantalla.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto y activo. Si no es visible debajo del panadapter, consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El decodificador requiere enrutamiento de audio por PC para producir texto. El panel muestra "(requires PC Audio)" como recordatorio si el audio no está configurado.

## Pasos

1. Observe el área de texto CW decodificado en la parte inferior del panadapter para confirmar que hay texto decodificado presente.
2. Para copiar todo lo que el decodificador ha capturado desde la última limpieza, haga clic en `CPY ALL`.
3. Para copiar solo el texto visible actualmente en el área de desplazamiento, desplácese hasta la parte que desea y luego haga clic en `CPY VIS`.
4. Pegue en cualquier aplicación usando el comando de pegado estándar de su sistema.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| `CPY ALL` | Copia el buffer completo de texto decodificado al portapapeles. | — | — | — |
| `CPY VIS` | Copia solo el texto visible actualmente en el área de desplazamiento al portapapeles. | — | — | — |
| `CLR` | Borra el buffer de decodificación CW. El texto ya copiado al portapapeles no se ve afectado. | — | — | — |
| Sens | Filtra decodificaciones de baja confianza; valores más altos son más estrictos. | 30 | 0–100 | `CwDecoderSensitivity` |

## Consejos

- El texto en la pantalla de decodificación está codificado por colores según el nivel de confianza. El verde indica la mayor confianza; el amarillo, naranja y rojo indican niveles de confianza progresivamente más bajos. Si la mayor parte del texto copiado aparece en naranja o rojo, considere subir el control deslizante Sens para filtrar los caracteres de baja confianza antes de copiar.
- Si el buffer ha crecido mucho, use `CPY VIS` para copiar solo un pasaje específico desplazándose hasta él primero y luego haciendo clic en `CPY VIS`.
- Haga clic en `CLR` antes de un nuevo contacto para mantener el buffer relevante, de modo que `CPY ALL` capture solo la sesión actual.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
