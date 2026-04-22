# Copiar el texto CW decodificado al portapapeles

Use los botones de copia del panel de decodificación CW para transferir el texto Morse decodificado al portapapeles del sistema — ya sea el historial completo de decodificación o solo lo que está visible en pantalla en ese momento.

## Antes de comenzar

- El panel de decodificación CW debe estar visible. Si no lo está, active primero el decodificador CW.
- El radio debe estar conectado y recibiendo audio. La etiqueta de estadísticas CW muestra el tono y la velocidad detectados cuando el decodificador está activo.

## Pasos

1. Observe el área de texto CW decodificado en la parte inferior del panadapter.
2. Elija qué copiar:
   - Para copiar todo el contenido del búfer de decodificación, haga clic en **CPY ALL**.
   - Para copiar solo el texto visible actualmente en el área de desplazamiento, haga clic en **CPY VIS**.
3. Pegue desde el portapapeles en cualquier otra aplicación de la manera habitual.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **CPY ALL** | Copia el búfer completo de texto decodificado al portapapeles. | — | — | — |
| **CPY VIS** | Copia solo el texto visible actualmente en el área de desplazamiento al portapapeles. | — | — | — |
| **CLR** | Borra el búfer de decodificación CW. No afecta el portapapeles. | — | — | — |
| **Sens** | Filtra decodificaciones de baja confianza; valores más altos son más estrictos. | 30 | 0–100 | `CwDecoderSensitivity` |

## Consejos

- El texto en el área de decodificación está coloreado según el nivel de confianza. Si gran parte del texto aparece en naranja o rojo, suba el control deslizante **Sens** para suprimir los caracteres de baja confianza antes de copiar.
- **CPY VIS** es útil cuando desea capturar solo un intercambio específico al que ha desplazado la vista, sin incluir el historial completo de la sesión.
- **CLR** borra el búfer en pantalla. Si desea una captura limpia a partir de un punto conocido, haga clic en **CLR** primero, espere al texto que necesita y luego haga clic en **CPY ALL**.

## Temas relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Fijar el tono o la velocidad del decodificador CW una vez que el seguimiento es correcto](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
