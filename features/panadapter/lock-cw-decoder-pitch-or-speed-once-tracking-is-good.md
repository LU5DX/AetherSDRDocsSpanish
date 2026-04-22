# Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es estable

Una vez que el decodificador CW ha encontrado una señal y la sigue con estabilidad, puede bloquear su tono, su velocidad o ambos para evitar que el decodificador se desplace hacia otra señal o responda al ruido.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto. Consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- La etiqueta de estadísticas CW debe mostrar una lectura estable de tono y WPM antes de bloquear. La etiqueta muestra los valores en el formato `<hz> Hz  <wpm> WPM`.

## Pasos

1. Observe la etiqueta de estadísticas CW hasta que los valores de tono (Hz) y velocidad (WPM) sean estables y estén siguiendo la señal deseada.
2. Para bloquear el tono, haga clic en 🔒P. El botón se resalta cuando está activo, lo que indica que el decodificador ya no buscará un nuevo tono.
3. Para bloquear la velocidad, haga clic en 🔒S. El botón se resalta cuando está activo, lo que indica que el decodificador mantendrá la estimación de WPM actual.
4. Para desbloquear cualquiera de los parámetros, haga clic en el mismo botón nuevamente. El resaltado desaparece y el decodificador reanuda el seguimiento.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| 🔒P (Lock Pitch) | Bloquea el tono del decodificador CW en la frecuencia sintonizada actualmente. Desactívelo para reanudar el seguimiento. | Off (desbloqueado) | On / Off | — |
| 🔒S (Lock Speed) | Bloquea la velocidad del decodificador CW en el WPM actual. Desactívelo para reanudar el seguimiento. | Off (desbloqueado) | On / Off | — |
| Etiqueta de estadísticas CW | Indicador de solo lectura del tono y la velocidad detectados: `<hz> Hz  <wpm> WPM`. | — | — | — |
| Lo (tono mínimo) | Tono mínimo en el que busca el decodificador. Limitado a ≤ Hi. | 500 Hz | 300–1200 Hz | — |
| Hi (tono máximo) | Tono máximo en el que busca el decodificador. Limitado a ≥ Lo. | 700 Hz | 300–1200 Hz | — |
| Sens | Filtra las decodificaciones de baja confianza. Los valores más altos son más estrictos. Asigna 0–100 a un umbral de costo de 1.0–0.1. | 30 | 0–100 | `CwDecoderSensitivity` |

## Consejos

- Ajuste los controles deslizantes de rango de tono Lo y Hi alrededor del tono de la señal antes de bloquear. Esto reduce la posibilidad de que el decodificador se enganche en la señal incorrecta desde el principio.
- Si la confianza del texto decodificado disminuye (los caracteres se vuelven de color naranja o rojo en la pantalla de decodificación) después de bloquear, es posible que la estación transmisora se haya desplazado. Desbloquee 🔒P temporalmente para que el decodificador readquiera la señal y luego vuelva a bloquear.
- Puede bloquear el tono y la velocidad de forma independiente. Bloquear solo la velocidad es útil en una banda donde el QSB desplaza el tono de audio, pero la velocidad de transmisión del operador es constante.

## Solución de problemas

- **La etiqueta de estadísticas CW no muestra tono ni WPM después de bloquear** — Los botones de bloqueo solo retienen los últimos valores seguidos; si no se estaba siguiendo ninguna señal antes de bloquear, no hay valores que retener. Haga clic en 🔒P o 🔒S nuevamente para desbloquear y permitir que el decodificador busque.
- **El decodificador ignora una nueva estación después de bloquear** — Este es el comportamiento esperado. Desbloquee el botón correspondiente para permitir que el decodificador se sintonice en la nueva señal.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar el ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
