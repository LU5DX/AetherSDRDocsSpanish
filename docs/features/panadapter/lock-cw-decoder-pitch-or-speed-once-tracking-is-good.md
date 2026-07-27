# Bloquear la frecuencia o velocidad del decodificador CW una vez que el rastreo sea estable

Una vez que el decodificador CW se ha enganchado a una señal, use los controles de bloqueo para evitar que el decodificador se desvíe hacia una frecuencia o velocidad diferente cuando las condiciones de la banda cambien o aparezcan otras señales cercanas.

## Antes de comenzar

- El panel de decodificación CW debe estar visible. Si no lo está, consulte [Activar el decodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El decodificador debe estar produciendo salida. Observe la etiqueta de estadísticas CW hasta que muestre una frecuencia y velocidad de lectura estables antes de bloquear.

## Pasos

1. Sintonice la señal CW y observe la etiqueta de estadísticas CW hasta que se estabilice en una lectura consistente, por ejemplo `598 Hz  22 WPM`.
2. Para mantener la frecuencia en ese valor, haga clic en 🔒P (Lock Pitch). El botón se resalta cuando está activo.
3. Para mantener la velocidad en ese WPM, haga clic en 🔒S (Lock Speed). El botón se resalta cuando está activo.
4. Para liberar un bloqueo, vuelva a hacer clic en el botón activo. Este vuelve a su estado sin resaltar y el decodificador reanuda el rastreo libremente.

## Qué hace cada control

| Control                       | Qué hace                                                                                                                                                          | Valor predeterminado |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| Etiqueta de estadísticas CW   | Muestra la frecuencia y velocidad detectadas actualmente en el formato `<hz> Hz  <wpm> WPM`.                                                                       | —                    |
| 🔒P (Lock Pitch)                | Bloquea la frecuencia del decodificador al valor mostrado en la etiqueta de estadísticas CW en el momento de hacer clic.                                            | Desbloqueado         |
| 🔒S (Lock Speed)                | Bloquea la velocidad del decodificador al WPM mostrado en la etiqueta de estadísticas CW en el momento de hacer clic.                                              | Desbloqueado         |
| Control deslizante de rango de frecuencia | Establece tanto el límite inferior como el superior del rango de frecuencias que el decodificador busca, usando un control deslizante de dos manijas. Arrastre la manija izquierda para el mínimo (Lo) y la manija derecha para el máximo (Hi). La etiqueta muestra los valores actuales (p. ej., 500 Hz / 700 Hz). | 500–700 Hz |
| Control deslizante de rango de WPM | Establece tanto el límite inferior como el superior del rango de velocidad que el decodificador busca, usando un control deslizante de dos manijas. Arrastre la manija izquierda para el mínimo y la manija derecha para el máximo. La etiqueta muestra los valores actuales (p. ej., 15 WPM / 40 WPM). | 15–40 WPM |
| Sens                          | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos.                                                                                  | 30                   |
| Texto de decodificación CW (menú contextual) | Haga clic derecho en el área de texto decodificado para abrir un menú contextual. Además de las acciones de texto estándar, el menú incluye un elemento **Clear** que borra el búfer de decodificación. | —                    |
| A- (disminuir tamaño de fuente) | Disminuye el tamaño de fuente del texto decodificado en el panel CW. Se mantiene entre sesiones.                                                                   | 13 px                |
| A+ (aumentar tamaño de fuente) | Aumenta el tamaño de fuente del texto decodificado en el panel CW. Se mantiene entre sesiones.                                                                     | 13 px                |

## Visualización de CW decodificado del lado de TX

El decodificador CW también puede mostrar su propia clave transmitida junto con las señales entrantes. Esto es útil para monitorear la calidad de su envío o para practicar fuera del aire.

- Su CW transmitido se muestra en cian para distinguirlo del texto recibido.
- Al cambiar de transmitir a recibir, se inserta un espacio para separar la ráfaga del siguiente texto recibido.
- Las decodificaciones del lado de TX utilizan el mismo filtro de confianza (Sens) que las decodificaciones recibidas.

## Redimensionar el panel de decodificación CW

La altura del panel de decodificación CW es ajustable para revelar más o menos historial de texto decodificado.

- Haga clic y arrastre la delgada barra de agarre horizontal en la parte superior del panel (justo debajo de la barra de estadísticas) hacia arriba o hacia abajo.
- La altura del panel se mantiene entre sesiones (rango: 60–600 px).
- El agarre de redimensionamiento tiene la etiqueta "Redimensionar el panel de decodificación CW" en su información sobre herramientas.

## Consejos

- Bloquee frecuencia y velocidad de forma independiente. Puede bloquear solo una si la otra aún se está estabilizando.
- Apriete las manijas del control deslizante de rango de frecuencia alrededor de la frecuencia de la señal antes de bloquear la frecuencia. Una ventana de búsqueda más estrecha reduce la posibilidad de que el decodificador se enganche a la señal incorrecta en primer lugar.
- Si el texto decodificado se vuelve confuso después del bloqueo, la frecuencia o velocidad de la señal puede haber cambiado. Haga clic en el botón de bloqueo activo para liberarlo, espere a que la etiqueta de estadísticas se reestabilice, luego bloquee de nuevo.
- Para borrar el búfer de decodificación sin mover el mouse al botón CLR, haga clic derecho en el área de texto decodificado y elija **Clear** en el menú contextual.
- Use los botones A- y A+ para ajustar el tamaño de fuente del texto decodificado para una mejor legibilidad (se mantiene entre sesiones).
- Arrastre el agarre de redimensionamiento en la parte superior del panel CW para aumentar o disminuir la cantidad de historial decodificado visible.

## Solución de problemas

- **La etiqueta de estadísticas CW está en blanco o no se actualiza** — El decodificador no ha adquirido una señal. Verifique que el audio de la PC esté enrutado correctamente (la etiqueta de sugerencia dice `(requires PC Audio)`), que la señal esté dentro de los límites del control deslizante de rango de frecuencia y que Sens no esté configurado tan alto que todas las decodificaciones sean rechazadas.
- **La frecuencia bloqueada no produce salida después de sintonizar otro lugar y volver** — Bloquear la frecuencia mantiene el decodificador en el valor en el momento del bloqueo. Si volvió a sintonizar el VFO, la frecuencia de la señal vista por el decodificador puede haberse desplazado. Libere 🔒P, vuelva a sintonizar y vuelva a bloquear una vez que la etiqueta de estadísticas se estabilice.
- **El texto decodificado del lado de TX no aparece** — Asegúrese de que el audio de la PC esté enrutado tanto para las rutas de recepción como de transmisión. El decodificador CW solo genera salida de TX cuando hay audio disponible desde su clave transmitida.

## Relacionado

- [Activar el decodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Copiar texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
