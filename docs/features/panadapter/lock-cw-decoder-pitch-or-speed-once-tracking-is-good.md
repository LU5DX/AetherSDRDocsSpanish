# Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es estable

Una vez que el decodificador CW se ha ajustado al tono y la velocidad de una señal, bloquear esos valores impide que el decodificador derive hacia interferencias o ruido entre transmisiones.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto y decodificando. Consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El audio del PC debe estar enrutado hacia AetherSDR. El panel CW muestra "(requires PC Audio)" como recordatorio si no lo está.
- Observe la etiqueta de estadísticas CW (formato: `<hz> Hz  <wpm> WPM`) y espere a obtener lecturas estables y consistentes antes de bloquear.

## Pasos

1. Sintonice la señal CW y observe la etiqueta de estadísticas CW hasta que las lecturas de tono y velocidad se estabilicen.
2. Para bloquear el tono: haga clic en 🔒P en el panel CW. El botón se resalta cuando está activo.
3. Para bloquear la velocidad: haga clic en 🔒S en el panel CW. El botón se resalta cuando está activo.
4. Para desbloquear, haga clic nuevamente en el botón activo.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Etiqueta de estadísticas CW | Muestra el tono y la velocidad detectados como `<hz> Hz  <wpm> WPM`. | — | — | — |
| 🔒P | Bloquea el tono del decodificador CW a la frecuencia sintonizada actualmente. Alternancia; se resalta cuando está bloqueado. | Off | — | — |
| 🔒S | Bloquea la velocidad del decodificador CW al WPM actual. Alternancia; se resalta cuando está bloqueado. | Off | — | — |
| Lo | Tono mínimo que busca el decodificador. Limitado a ≤ Hi. | 500 Hz | 300–1200 Hz | — |
| Hi | Tono máximo que busca el decodificador. Limitado a ≥ Lo. | 700 Hz | 300–1200 Hz | — |
| Sens | Filtra las decodificaciones de baja confianza. Valores más altos son más estrictos. | 30 | 0–100 | `CwDecoderSensitivity` |

## Consejos

- Bloquee el tono y la velocidad juntos al copiar una sola estación durante un pileup. El decodificador dejará de seguir otras señales en la banda de paso.
- Si la señal deriva ligeramente, desbloquee 🔒P, permita que el decodificador vuelva a adquirirla y luego bloquéela de nuevo.
- Reduzca el rango de tono entre Lo y Hi antes de bloquear para disminuir la posibilidad de que el decodificador se enganche en la señal incorrecta.
- El texto decodificado tiene código de color según la confianza: verde indica la mayor confianza, seguido de amarillo, naranja y rojo. Bloquee cuando observe principalmente caracteres verdes o amarillos.

## Solución de problemas

- **🔒P o 🔒S no aparece** — El panel de decodificación CW no está abierto. Ábralo primero; consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- **La etiqueta de estadísticas no muestra ninguna lectura después de bloquear** — El audio del PC no está enrutado hacia AetherSDR. El panel mostrará "(requires PC Audio)". Verifique el enrutamiento de audio y desbloquee para permitir que el decodificador vuelva a adquirir la señal.
- **El texto decodificado se vuelve mayoritariamente naranja o rojo después de bloquear** — El tono o la velocidad bloqueados ya no coinciden con la señal. Haga clic en 🔒P o 🔒S para desbloquear, espere a que la etiqueta de estadísticas se estabilice en la señal objetivo y vuelva a bloquear.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar el ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
