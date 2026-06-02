# Bloquear tono o velocidad del decodificador CW una vez que el seguimiento sea correcto

Una vez que el decodificador CW se ha enganchado a una señal, use los controles de bloqueo para evitar que el decodificador se desvíe a un tono o velocidad diferente cuando cambien las condiciones de la banda o aparezcan otras señales cercanas.

## Antes de comenzar

- El panel de decodificación CW debe estar visible. Si no lo está, consulte [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El decodificador debe estar produciendo salida. Observe la etiqueta de estadísticas CW hasta que muestre una lectura estable de tono y WPM antes de bloquear.

## Pasos

1. Sintonice la señal CW y observe la etiqueta de estadísticas CW hasta que se estabilice en una lectura consistente, por ejemplo `598 Hz  22 WPM`.
2. Para mantener el tono en esa frecuencia, haga clic en 🔒P (Lock Pitch). El botón se resalta cuando está activo.
3. Para mantener la velocidad en ese WPM, haga clic en 🔒S (Lock Speed). El botón se resalta cuando está activo.
4. Para liberar un bloqueo, vuelva a hacer clic en el botón activo. Este vuelve a su estado sin resaltar y el decodificador reanuda el seguimiento libremente.

## Qué hace cada control

| Control                       | Qué hace                                                                                                                                                          | Predeterminado |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| Etiqueta de estadísticas CW   | Muestra el tono y la velocidad detectados actualmente en el formato `<hz> Hz  <wpm> WPM`.                                                                          | —              |
| 🔒P (Lock Pitch)               | Bloquea el tono del decodificador a la frecuencia mostrada en la etiqueta de estadísticas CW en el momento en que hace clic.                                       | Desbloqueado   |
| 🔒S (Lock Speed)               | Bloquea la velocidad del decodificador al WPM mostrado en la etiqueta de estadísticas CW en el momento en que hace clic.                                           | Desbloqueado   |
| Lo (pitch min)                | Establece el límite inferior del rango de tono que busca el decodificador.                                                                                         | 500 Hz         |
| Hi (pitch max)                | Establece el límite superior del rango de tono que busca el decodificador.                                                                                         | 700 Hz         |
| Sens                          | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos.                                                                                | 30             |
| Texto decodificado CW (menú contextual) | Haga clic derecho en el área de texto decodificado para abrir un menú contextual. Además de las acciones de texto estándar, el menú incluye un elemento **Clear** que limpia el búfer de decodificación. | —              |

## Visualización CW decodificada del lado de TX

El decodificador CW también puede mostrar su propia transmisión de clave junto con las señales entrantes. Esto es útil para monitorear la calidad de su envío o para practicar fuera del aire.

- Su CW transmitido se muestra en cian para distinguirlo del texto recibido.
- Al cambiar de transmitir a recibir, se inserta un espacio para separar la ráfaga del texto recibido siguiente.
- Las decodificaciones del lado de TX utilizan el mismo filtro de confianza (Sens) que las decodificaciones recibidas.

## Consejos

- Bloquee el tono y la velocidad de forma independiente. Puede bloquear solo uno si el otro aún se está estabilizando.
- Ajuste los controles deslizantes de rango de tono Lo y Hi alrededor de la frecuencia de la señal antes de bloquear el tono. Una ventana de búsqueda más estrecha reduce la posibilidad de que el decodificador se enganche a la señal incorrecta en primer lugar.
- Si el texto decodificado se vuelve confuso después de bloquear, es posible que el tono o la velocidad de la señal se hayan desviado. Haga clic en el botón de bloqueo activo para liberarlo, espere a que la etiqueta de estadísticas se reestabilice y luego bloquee de nuevo.
- Para limpiar el búfer de decodificación sin mover el mouse al botón CLR, haga clic derecho en el área de texto decodificado y elija **Clear** en el menú contextual.

## Solución de problemas

- **La etiqueta de estadísticas CW está en blanco o no se actualiza** — El decodificador no ha adquirido una señal. Verifique que el audio de PC esté enrutado correctamente (la etiqueta de sugerencia dice `(requires PC Audio)`), que la señal caiga dentro del rango de tono Lo–Hi y que Sens no esté configurado tan alto que todas las decodificaciones sean rechazadas.
- **El tono bloqueado no produce salida después de sintonizar a otra frecuencia y volver** — Bloquear el tono mantiene el decodificador en la frecuencia en el momento del bloqueo. Si ha reajustado el VFO, es posible que el tono de la信号 vista por el decodificador se haya desplazado. Libere 🔒P, vuelva a sintonizar y bloquee de nuevo una vez que la etiqueta de estadísticas se estabilice.
- **El texto decodificado del lado de TX no aparece** — Asegúrese de que el audio de PC esté enrutado tanto para la ruta de recepción como para la de transmisión. El decodificador CW solo genera salida TX cuando hay audio disponible de su transmisión de clave.

## Relacionado

- [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Tune CW decoder sensitivity to reject noise](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Copy decoded CW text to the clipboard](copy-decoded-cw-text-to-the-clipboard.md)
