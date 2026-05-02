# Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es estable

Una vez que el decodificador CW ha capturado una señal, use los controles de bloqueo para evitar que el decodificador derive hacia un tono o velocidad diferentes cuando las condiciones de banda cambien o aparezcan otras señales cercanas.

## Antes de comenzar

- El panel de decodificación CW debe estar visible. Si no lo está, consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El decodificador debe estar produciendo salida. Observe la etiqueta de estadísticas CW hasta que muestre una lectura estable de tono y WPM antes de bloquear.

## Pasos

1. Sintonice la señal CW y observe la etiqueta de estadísticas CW hasta que se estabilice en una lectura consistente, por ejemplo `598 Hz  22 WPM`.
2. Para fijar el tono en esa frecuencia, haga clic en 🔒P (Lock Pitch). El botón se resalta cuando está activo.
3. Para fijar la velocidad en ese WPM, haga clic en 🔒S (Lock Speed). El botón se resalta cuando está activo.
4. Para liberar un bloqueo, haga clic nuevamente en el botón activo. Regresa a su estado sin resaltar y el decodificador reanuda el seguimiento libremente.

## Qué hace cada control

| Control                       | Descripción                                                                                                                                                                                         | Valor predeterminado |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| Etiqueta de estadísticas CW   | Muestra el tono y la velocidad detectados actualmente en el formato `<hz> Hz  <wpm> WPM`.                                                                                                           | —                    |
| 🔒P (Lock Pitch)               | Bloquea el tono del decodificador a la frecuencia mostrada en la etiqueta de estadísticas CW en el momento en que hace clic.                                                                        | Desbloqueado         |
| 🔒S (Lock Speed)               | Bloquea la velocidad del decodificador al WPM mostrado en la etiqueta de estadísticas CW en el momento en que hace clic.                                                                            | Desbloqueado         |
| Lo (tono mínimo)              | Establece el límite inferior del rango de tono en el que busca el decodificador.                                                                                                                    | 500 Hz               |
| Hi (tono máximo)              | Establece el límite superior del rango de tono en el que busca el decodificador.                                                                                                                    | 700 Hz               |
| Sens                          | Filtra las decodificaciones de baja confianza. Los valores más altos son más estrictos.                                                                                                             | 30                   |
| Texto decodificado CW (menú contextual) | Haga clic derecho en el área de texto decodificado para abrir un menú contextual. Además de las acciones de texto estándar, el menú incluye un elemento **Clear** que borra el búfer de decodificación. | —             |

## Consejos

- Bloquee el tono y la velocidad de forma independiente. Puede bloquear solo uno si el otro aún se está estabilizando.
- Ajuste los controles deslizantes de rango de tono Lo y Hi alrededor de la frecuencia de la señal antes de bloquear el tono. Una ventana de búsqueda más estrecha reduce la posibilidad de que el decodificador capture una señal incorrecta desde el principio.
- Si el texto decodificado se vuelve ilegible después de bloquear, es posible que el tono o la velocidad de la señal hayan derivado. Haga clic en el botón de bloqueo activo para liberarlo, espere a que la etiqueta de estadísticas se vuelva a estabilizar y luego bloquee de nuevo.
- Para borrar el búfer de decodificación sin mover el mouse al botón CLR, haga clic derecho en el área de texto decodificado y elija **Clear** en el menú contextual.

## Solución de problemas

- **La etiqueta de estadísticas CW está en blanco o no se actualiza** — El decodificador no ha adquirido una señal. Verifique que el audio de la PC esté enrutado correctamente (la etiqueta de sugerencia muestra `(requires PC Audio)`), que la señal esté dentro del rango de tono Lo–Hi, y que Sens no esté configurado tan alto que se rechacen todas las decodificaciones.
- **El tono bloqueado no produce salida después de sintonizar y volver** — Bloquear el tono fija el decodificador a la frecuencia en el momento del bloqueo. Si resintonizó el VFO, el tono de la señal visto por el decodificador puede haber cambiado. Libere 🔒P, resintonice y vuelva a bloquear una vez que la etiqueta de estadísticas se estabilice.

## Relacionados

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
