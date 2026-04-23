# Copiar el texto CW decodificado al portapapeles

Use el panel de decodificación CW para copiar texto Morse decodificado del aire — ya sea el buffer de decodificación completo o solo lo que esté visible en pantalla en ese momento.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto y decodificando activamente. Si no está visible, consulte [Activar el decodificador CW para leer Morse del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El decodificador CW requiere enrutamiento de audio del PC para recibir la señal. El panel muestra "(requires PC Audio)" como recordatorio.

## Pasos

1. Localice el panel de decodificación CW en la parte inferior del applet Panadapter.
2. Para copiar todo el contenido del buffer de decodificación, haga clic en `CPY ALL`. Todo el texto del buffer se coloca en el portapapeles.
3. Para copiar solo el texto visible actualmente en el área de desplazamiento, haga clic en `CPY VIS`. Solo la porción visible se coloca en el portapapeles.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| CPY ALL | Copia el buffer completo de texto decodificado al portapapeles. | — | — | — |
| CPY VIS | Copia al portapapeles solo el texto visible actualmente en el área de desplazamiento. | — | — | — |
| CLR | Borra completamente el buffer de decodificación CW. No afecta el portapapeles. | — | — | — |
| Sens | Filtra decodificaciones de baja confianza. Valores más altos son más estrictos. | 30 | 0–100 | `CwDecoderSensitivity` |
| Texto decodificado CW | Visualización continua de solo lectura del CW decodificado, coloreado según el nivel de confianza. Verde = mayor confianza; amarillo, naranja y rojo indican confianza progresivamente menor. | — | — | — |

## Consejos

- Si el buffer acumuló una sesión larga pero solo desea el intercambio más reciente, desplace el texto decodificado hasta la parte que le interesa y use `CPY VIS` en lugar de `CPY ALL`.
- Use `CLR` para resetear el buffer de decodificación antes de un nuevo contacto, de modo que `CPY ALL` capture únicamente el texto de ese contacto.
- Ajuste el control deslizante Sens para reducir caracteres de ruido en el buffer antes de copiar. Un valor de 30 (el predeterminado) deja pasar la mayor parte del texto legible mientras rechaza las decodificaciones de menor confianza.

## Solución de problemas

- **CPY ALL coloca una cadena vacía en el portapapeles** — El buffer de decodificación está vacío. Verifique que el decodificador CW esté recibiendo audio y que el control deslizante Sens no esté ajustado tan alto que todas las decodificaciones estén siendo filtradas.
- **CPY VIS copia menos texto del esperado** — Solo se copia el texto visible en el área de desplazamiento en el momento del clic. Desplace el panel de decodificación para mostrar el texto deseado antes de copiar.

## Relacionados

- [Activar el decodificador CW para leer Morse del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
