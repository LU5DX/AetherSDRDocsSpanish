# Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es estable

Una vez que el decodificador CW ha adquirido una señal, bloquear su tono o velocidad evita que derive hacia otra señal o que vuelva a estimar la velocidad entre turnos de transmisión.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto. Consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- La etiqueta de estadísticas CW debe mostrar una lectura estable, por ejemplo `600 Hz  20 WPM`, antes de bloquear.

## Pasos

1. Observe la etiqueta de estadísticas CW hasta que los valores de tono (Hz) y velocidad (WPM) se estabilicen en la señal deseada.
2. Para bloquear el tono, haga clic en 🔒P. El botón se resalta cuando está activo.
3. Para bloquear la velocidad, haga clic en 🔒S. El botón se resalta cuando está activo.
4. Para desbloquear, haga clic nuevamente en el botón activo.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| Etiqueta de estadísticas CW | Muestra el tono y la velocidad detectados actualmente como `<hz> Hz  <wpm> WPM`. | — | — | — |
| 🔒P (Lock Pitch) | Bloquea el tono del decodificador en la frecuencia sintonizada actual. Desactívelo para reanudar el seguimiento. | Off | On / Off | — |
| 🔒S (Lock Speed) | Bloquea la velocidad del decodificador en el WPM actual. Desactívelo para reanudar el seguimiento. | Off | On / Off | — |
| Lo (tono mínimo) | Tono mínimo en el que busca el decodificador. Limitado a ≤ Hi. | 500 Hz | 300–1200 Hz | — |
| Hi (tono máximo) | Tono máximo en el que busca el decodificador. Limitado a ≥ Lo. | 700 Hz | 300–1200 Hz | — |
| Sens | Filtra las decodificaciones de baja confianza. Los valores más altos son más estrictos. Asigna el rango 0–100 a un umbral de costo de 1.0–0.1. | 30 | 0–100 | `CwDecoderSensitivity` |

## Consejos

- Si el decodificador salta entre señales, reduzca el rango de tono Lo/Hi alrededor de la señal antes de bloquear el tono. Esto limita la ventana de búsqueda antes de que el bloqueo entre en efecto.
- Bloquee la velocidad al copiar a un solo operador a un WPM conocido; desbloquéela al pasar a un nuevo QSO donde la velocidad de envío puede ser diferente.
- Bloquear tanto el tono como la velocidad al mismo tiempo proporciona la decodificación más estable en un segmento de banda con mucho tráfico.

## Solución de problemas

- **La etiqueta de estadísticas CW no muestra ninguna lectura antes de bloquear** — El decodificador aún no ha adquirido la señal. Verifique que el audio del PC esté enrutado correctamente (el panel CW muestra un aviso `(requires PC Audio)` si falta el audio). Ajuste Lo y Hi para encuadrar el tono de la señal, y reduzca Sens hacia 0 para permitir el paso de decodificaciones de menor confianza hasta que se adquiera la señal.
- **La calidad del texto decodificado disminuye después de bloquear el tono** — Es posible que la señal haya derivado. Desbloquee 🔒P, permita que el decodificador vuelva a adquirir la señal y luego vuelva a bloquear.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
