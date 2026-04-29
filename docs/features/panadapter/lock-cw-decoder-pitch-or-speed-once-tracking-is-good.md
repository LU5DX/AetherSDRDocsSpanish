# Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento es estable

Una vez que el decodificador CW ha captado una señal, utilice los controles de bloqueo para evitar que derive hacia un tono o velocidad diferentes cuando las condiciones de banda cambien o aparezcan otras señales cercanas.

## Antes de comenzar

- El panel de decodificación CW debe estar visible. Si no lo está, consulte [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El decodificador debe estar produciendo salida. Observe la etiqueta de estadísticas CW hasta que muestre un tono y una lectura de PPM estables antes de bloquear.

## Pasos

1. Sintonice la señal CW y observe la etiqueta de estadísticas CW hasta que se estabilice en una lectura consistente, por ejemplo `598 Hz  22 WPM`.
2. Para fijar el tono en esa frecuencia, haga clic en 🔒P (Lock Pitch). El botón se resalta cuando está activo.
3. Para fijar la velocidad en ese valor de PPM, haga clic en 🔒S (Lock Speed). El botón se resalta cuando está activo.
4. Para liberar un bloqueo, haga clic de nuevo en el botón activo. Vuelve a su estado sin resaltar y el decodificador retoma el seguimiento libremente.

## Qué hace cada control

| Control | Función | Valor predeterminado | Notas |
|---|---|---|---|
| Etiqueta de estadísticas CW | Muestra el tono y la velocidad detectados actualmente en el formato `<hz> Hz  <wpm> WPM`. | — | Indicador de solo lectura. |
| 🔒P (Lock Pitch) | Bloquea el tono del decodificador en la frecuencia mostrada en la etiqueta de estadísticas CW en el momento de hacer clic. | Desbloqueado | Botón de alternancia; resaltado cuando está activo. |
| 🔒S (Lock Speed) | Bloquea la velocidad del decodificador en el valor de PPM mostrado en la etiqueta de estadísticas CW en el momento de hacer clic. | Desbloqueado | Botón de alternancia; resaltado cuando está activo. |
| Lo (tono mínimo) | Establece el límite inferior del rango de tono que busca el decodificador. | 500 Hz | Rango válido: 300–1200 Hz. Limitado ≤ Hi. |
| Hi (tono máximo) | Establece el límite superior del rango de tono que busca el decodificador. | 700 Hz | Rango válido: 300–1200 Hz. Limitado ≥ Lo. |
| Sens | Filtra las decodificaciones de baja confianza. Los valores más altos son más estrictos. | 30 | Rango: 0–100. Se guarda como `CwDecoderSensitivity`. |
| Texto decodificado CW (menú contextual) | Haga clic derecho en el área de texto decodificado para abrir un menú contextual. Además de las acciones de texto estándar, el menú incluye el elemento **Clear** que borra el búfer de decodificación. | — | Añadido en v0.9.2.1. Equivalente a hacer clic en CLR. |

## Consejos

- Bloquee el tono y la velocidad de forma independiente. Puede bloquear solo uno si el otro aún se está estabilizando.
- Ajuste los controles deslizantes Lo y Hi del rango de tono alrededor de la frecuencia de la señal antes de bloquear el tono. Una ventana de búsqueda más estrecha reduce la posibilidad de que el decodificador capture la señal incorrecta desde el principio.
- Si el texto decodificado se corrompe después de bloquear, es posible que el tono o la velocidad de la señal hayan derivado. Haga clic en el botón de bloqueo activo para liberarlo, espere a que la etiqueta de estadísticas se estabilice nuevamente y vuelva a bloquear.
- Para borrar el búfer de decodificación sin mover el mouse al botón CLR, haga clic derecho en el área de texto decodificado y elija **Clear** en el menú contextual.

## Solución de problemas

- **La etiqueta de estadísticas CW está en blanco o no se actualiza** — El decodificador no ha captado ninguna señal. Compruebe que el audio del PC esté enrutado correctamente (la etiqueta de ayuda muestra `(requires PC Audio)`), que la señal se encuentre dentro del rango de tono Lo–Hi, y que Sens no esté configurado tan alto que se rechacen todas las decodificaciones.
- **El tono bloqueado no produce salida después de sintonizar y volver** — Bloquear el tono fija el decodificador en la frecuencia en el momento del bloqueo. Si resintonizó el VFO, el tono de la señal que percibe el decodificador puede haber cambiado. Libere 🔒P, resintonice y vuelva a bloquear una vez que la etiqueta de estadísticas se estabilice.

## Relacionado

- [Activar el decodificador CW para leer Morse en el aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Copiar el texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
