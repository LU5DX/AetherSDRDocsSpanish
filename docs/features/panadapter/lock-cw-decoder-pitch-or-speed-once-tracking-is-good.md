# Fijar la frecuencia o velocidad del decodificador CW una vez que el seguimiento sea estable

Una vez que el decodificador CW se haya enganchado a una señal, use los controles de fijación para evitar que el decodificador se desvíe a una frecuencia o velocidad diferente cuando cambien las condiciones de la banda o aparezcan otras señales cercanas.

## Antes de comenzar

- El panel de decodificación CW debe estar visible. Si no lo está, consulte [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El decodificador debe estar generando salida. Observe la etiqueta de estadísticas CW hasta que muestre una frecuencia y velocidad de lectura estables antes de fijar.

## Pasos

1. Sintonice la señal CW y observe la etiqueta de estadísticas CW hasta que se estabilice en una lectura consistente, por ejemplo `598 Hz  22 WPM`.
2. Para mantener la frecuencia en ese valor, haga clic en 🔒P (Lock Pitch). El botón se resalta cuando está activo.
3. Para mantener la velocidad en ese WPM, haga clic en 🔒S (Lock Speed). El botón se resalta cuando está activo.
4. Para liberar una fijación, haga clic nuevamente en el botón activo. Este vuelve a su estado sin resaltar y el decodificador reanuda el seguimiento libremente.

## Qué hace cada control

| Control                       | Qué hace                                                                                                                                                          | Valor predeterminado |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| Etiqueta de estadísticas CW   | Muestra la frecuencia y velocidad detectadas actualmente en el formato `<hz> Hz  <wpm> WPM`.                                                                        | —        |
| 🔒P (Lock Pitch)               | Fija la frecuencia del decodificador al valor mostrado en la etiqueta de estadísticas CW en el momento de hacer clic.                                                 | Desbloqueado |
| 🔒S (Lock Speed)               | Fija la velocidad del decodificador al WPM mostrado en la etiqueta de estadísticas CW en el momento de hacer clic.                                                   | Desbloqueado |
| Control deslizante de rango de frecuencia (Pitch range slider) | Establece los límites inferior y superior del rango de frecuencia que el decodificador busca, usando un control deslizante de dos manijas. Arrastre la manija izquierda para el mínimo (Lo) y la manija derecha para el máximo (Hi). La etiqueta muestra los valores actuales (ej. 500 Hz / 700 Hz). | 500–700 Hz |
| Control deslizante de rango de WPM (WPM range slider) | Establece los límites inferior y superior del rango de velocidad que el decodificador busca, usando un control deslizante de dos manijas. Arrastre la manija izquierda para el mínimo y la manija derecha para el máximo. La etiqueta muestra los valores actuales (ej. 15 WPM / 40 WPM). | 15–40 WPM |
| Sens                          | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos.                                                                                  | 30       |
| Área de texto de decodificación CW (menú contextual) | Haga clic derecho en el área de texto decodificado para abrir un menú contextual. Además de las acciones de texto estándar, el menú incluye un elemento **Clear** que limpia el búfer de decodificación. | —        |

## Visualización de CW decodificado del lado de transmisión (TX)

El decodificador CW también puede mostrar su propia señalización transmitida junto con las señales entrantes. Esto es útil para monitorear la calidad de su envío o para práctica fuera del aire.

- Su CW transmitido se muestra en cian para distinguirlo del texto recibido.
- Al cambiar de transmisión a recepción, se inserta un espacio para separar la ráfaga del texto recibido siguiente.
- Las decodificaciones del lado TX usan el mismo filtro de confianza (Sens) que las decodificaciones recibidas.

## Consejos

- Fije la frecuencia y la velocidad de forma independiente. Puede fijar solo una si la otra aún se está estabilizando.
- Reduzca las manijas del control deslizante de rango de frecuencia alrededor de la frecuencia de la señal antes de fijar la frecuencia. Una ventana de búsqueda más estrecha reduce la probabilidad de que el decodificador se enganche a la señal incorrecta en primer lugar.
- Si el texto decodificado se vuelve confuso después de fijar, es posible que la frecuencia o velocidad de la señal haya cambiado. Haga clic en el botón de fijación activo para liberarlo, espere a que la etiqueta de estadísticas se reestabilice y luego fije nuevamente.
- Para limpiar el búfer de decodificación sin mover el mouse al botón CLR, haga clic derecho en el área de texto decodificado y elija **Clear** en el menú contextual.

## Solución de problemas

- **La etiqueta de estadísticas CW está en blanco o no se actualiza** — El decodificador no ha adquirido una señal. Verifique que el audio de PC esté enrutado correctamente (la etiqueta de sugerencia muestra `(requires PC Audio)`), que la señal esté dentro de los límites del control deslizante de rango de frecuencia y que Sens no esté configurado tan alto que todas las decodificaciones sean rechazadas.
- **La frecuencia fijada no produce salida después de sintonizar a otra frecuencia y regresar** — Fijar la frecuencia mantiene el decodificador en la frecuencia en el momento de la fijación. Si reajustó el VFO, la frecuencia de la señal vista por el decodificador puede haber cambiado. Libere 🔒P, reajuste y vuelva a fijar una vez que la etiqueta de estadísticas se estabilice.
- **El texto decodificado del lado TX no aparece** — Asegúrese de que el audio de PC esté enrutado para ambas rutas de recepción y transmisión. El decodificador CW solo genera salida TX cuando hay audio disponible de su señalización transmitida.

## Relacionados

- [Turn on the CW decoder to read Morse off-air](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Tune CW decoder sensitivity to reject noise](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Copy decoded CW text to the clipboard](copy-decoded-cw-text-to-the-clipboard.md)
