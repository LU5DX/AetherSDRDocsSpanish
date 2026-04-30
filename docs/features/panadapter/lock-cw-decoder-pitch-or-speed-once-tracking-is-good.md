# Bloquear la afinación o velocidad del decodificador CW una vez que el seguimiento sea bueno

Una vez que el decodificador CW se ha enganchado a una señal, use los controles de bloqueo para evitar que el decodificador se desplace a una afinación o velocidad diferente cuando cambien las condiciones de la banda u otras señales aparezcan cerca.

## Antes de comenzar

- El panel de decodificación CW debe estar visible. Si no es así, consulte [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El decodificador debe estar produciendo salida. Observe la etiqueta de estadísticas CW hasta que muestre una lectura estable de afinación y WPM antes de bloquear.

## Pasos

1. Sintonice la señal CW y observe la etiqueta de estadísticas CW hasta que se estabilice en una lectura consistente, por ejemplo `598 Hz  22 WPM`.
2. Para mantener la afinación en esa frecuencia, haga clic en 🔒P (Lock Pitch). El botón se resalta cuando está activo.
3. Para mantener la velocidad en ese WPM, haga clic en 🔒S (Lock Speed). El botón se resalta cuando está activo.
4. Para liberar un bloqueo, haga clic nuevamente en el botón activo. Vuelve a su estado sin resaltar y el decodificador reanuda el seguimiento libre.

## Qué hace cada control

| Control                       | Qué hace                                                                                                                                                          | Predeterminado  |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| Etiqueta de estadísticas CW                | Muestra la afinación y velocidad detectadas actualmente en el formato `<hz> Hz  <wpm> WPM`.                                                                                   | —        |
| 🔒P (Lock Pitch)               | Bloquea la afinación del decodificador a la frecuencia mostrada en la etiqueta de estadísticas CW en el momento en que haga clic.                                                                         | Desbloqueado |
| 🔒S (Lock Speed)               | Bloquea la velocidad del decodificador al WPM mostrado en la etiqueta de estadísticas CW en el momento en que hace clic.                                                                               | Desbloqueado |
| Lo (pitch min)                | Establece el límite inferior del rango de afinación que busca el decodificador.                                                                                                         | 500 Hz   |
| Hi (pitch max)                | Establece el límite superior del rango de afinación que busca el decodificador.                                                                                                         | 700 Hz   |
| Sens                          | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos.                                                                                                           | 30       |
| Texto de decodificación CW (menú contextual) | Haga clic derecho en el área de texto decodificado para abrir un menú contextual. Además de las acciones de texto estándar, el menú incluye un elemento **Clear** que borra el búfer de decodificación. | —        |

## Consejos

- Bloquee la afinación y la velocidad de forma independiente. Puede bloquear solo una si la otra aún se está estabilizando.
- Reduzca los controles deslizantes del rango de afinación Lo e Hi alrededor de la frecuencia de la señal antes de bloquear la afinación. Una ventana de búsqueda más estrecha reduce la probabilidad de que el decodificador se enganche a la señal incorrecta en primer lugar.
- Si el texto decodificado se vuelve confuso después de bloquear, la afinación o velocidad de la señal puede haber cambiado. Haga clic en el botón de bloqueo activo para liberarlo, espere a que la etiqueta de estadísticas se estabilice nuevamente, luego bloquee nuevamente.
- Para borrar el búfer de decodificación sin mover el ratón al botón CLR, haga clic derecho en el área de texto decodificado y elija **Clear** en el menú contextual.

## Solución de problemas

- **Etiqueta de estadísticas CW en blanco o no se actualiza** — El decodificador no ha adquirido una señal. Verifique que el audio de la PC esté enrutado correctamente (la etiqueta de sugerencia lee `(requires PC Audio)`), que la señal caiga dentro del rango de afinación Lo–Hi, y que Sens no esté configurado tan alto que se rechacen todas las decodificaciones.
- **Pitch bloqueado no produce salida después de sintonizar lejos y volver** — Bloquear la afinación mantiene el decodificador a la frecuencia en el momento del bloqueo. Si resintonizó el VFO, la afinación de la señal vista por el decodificador puede haber cambiado. Libere 🔒P, resintonice y bloquee nuevamente una vez que la etiqueta de estadísticas se estabilice.

## Relacionado

- [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Tune CW decoder sensitivity to reject noise](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Copy decoded CW text to the clipboard](copy-decoded-cw-text-to-the-clipboard.md)
