# Bloquear la afinación o velocidad del decodificador CW una vez que el seguimiento es bueno

Una vez que el decodificador CW se ha fijado en una señal, use los controles de bloqueo para evitar que el decodificador se desvíe a una afinación o velocidad diferente cuando cambien las condiciones de la banda o aparezcan otras señales cercanas.

## Antes de comenzar

- El panel de decodificación CW debe estar visible. Si no lo está, consulte [Activar el decodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md).
- El decodificador debe estar produciendo salida. Observe la etiqueta de estadísticas CW hasta que muestre una lectura estable de afinación y WPM antes de bloquear.

## Pasos

1. Sintonice la señal CW y observe la etiqueta de estadísticas CW hasta que se estabilice en una lectura consistente, por ejemplo `598 Hz 22 WPM`.
2. Para mantener la afinación en esa frecuencia, haga clic en 🔒P (Lock Pitch). El botón se resalta cuando está activo.
3. Para mantener la velocidad en ese WPM, haga clic en 🔒S (Lock Speed). El botón se resalta cuando está activo.
4. Para liberar un bloqueo, haga clic nuevamente en el botón activo. Este vuelve a su estado sin resaltar y el decodificador reanuda el seguimiento libremente.

## Qué hace cada control

| Control                        | Qué hace                                                                                                                                                                                                                             | Predeterminado |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| Etiqueta de estadísticas CW    | Muestra la afinación y velocidad detectadas actualmente en el formato `<hz> Hz <wpm> WPM`.                                                                                                                                             | —              |
| 🔒P (Lock Pitch)                | Bloquea la afinación del decodificador en la frecuencia mostrada en la etiqueta de estadísticas CW en el momento en que hace clic.                                                                                                    | Desbloqueado   |
| 🔒S (Lock Speed)                | Bloquea la velocidad del decodificador en el WPM mostrado en la etiqueta de estadísticas CW en el momento en que hace clic.                                                                                                            | Desbloqueado   |
| Control deslizante de rango de afinación | Establece tanto el límite inferior como el superior del rango de afinación que el decodificador busca, usando un control deslizante de doble asa. Arrastre el asa izquierda para el mínimo (Lo) y el asa derecha para el máximo (Hi). La etiqueta muestra los valores actuales (p. ej. 500 Hz / 700 Hz). | 500–700 Hz |
| Control deslizante de rango de WPM | Establece tanto el límite inferior como el superior del rango de velocidad que el decodificador busca, usando un control deslizante de doble asa. Arrastre el asa izquierda para el mínimo y el asa derecha para el máximo. La etiqueta muestra los valores actuales (p. ej. 15 WPM / 40 WPM). | 15–40 WPM |
| Sens                          | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos.                                                                                                                                                   | 30            |
| Texto de decodificación CW (menú contextual) | Haga clic derecho en el área de texto decodificado para abrir un menú contextual. Además de las acciones de texto estándar, el menú incluye un elemento **Clear** que borra el búfer de decodificación.                                  | —              |
| A- (reducir tamaño de fuente)  | Reduce el tamaño de fuente del texto decodificado en el panel CW. Se conserva entre sesiones.                                                                                                                                         | 13 px         |
| A+ (aumentar tamaño de fuente) | Aumenta el tamaño de fuente del texto decodificado en el panel CW. Se conserva entre sesiones.                                                                                                                                        | 13 px         |

## Visualización de CW decodificado del lado de TX

El decodificador CW también puede mostrar su propia clave transmitida junto con las señales entrantes. Esto es útil para monitorear la calidad de su envío o para practicar fuera del aire.

- Su CW transmitido se muestra en cian para distinguirlo del texto recibido.
- Al cambiar de transmitir a recibir, se inserta un espacio para separar la ráfaga del texto recibido siguiente.
- Las decodificaciones del lado TX usan el mismo filtro de confianza (Sens) que las decodificaciones recibidas.

## Cambiar el tamaño del panel de decodificación CW

La altura del panel de decodificación CW es ajustable para mostrar más o menos historial de texto decodificado.

- Haga clic y arrastre la delgada barra de agarre horizontal en la parte superior del panel (justo debajo de la barra de estadísticas) hacia arriba o hacia abajo.
- La altura del panel se conserva entre sesiones (rango: 60–600 px).
- El agarre de redimensionamiento está etiquetado como "Drag to resize the CW decode panel" en su información sobre herramientas.

## Consejos

- Bloquee la afinación y la velocidad de forma independiente. Puede bloquear solo una si la otra aún se está estabilizando.
- Reduzca las asas del control deslizante de rango de afinación alrededor de la frecuencia de la señal antes de bloquear la afinación. Una ventana de búsqueda más estrecha reduce la posibilidad de que el decodificador se fije en la señal incorrecta desde el principio.
- Si el texto decodificado se vuelve ilegible después de bloquear, la afinación o velocidad de la señal puede haberse desviado. Haga clic en el botón de bloqueo activo para liberarlo, espere a que la etiqueta de estadísticas se reestabilice y luego vuelva a bloquear.
- Para borrar el búfer de decodificación sin mover el mouse al botón CLR, haga clic derecho en el área de texto decodificado y elija **Clear** en el menú contextual.
- Use los botones A- y A+ para ajustar el tamaño de fuente del texto decodificado para una mejor legibilidad (se conserva entre sesiones).
- Arrastre el agarre de redimensionamiento en la parte superior del panel CW para aumentar o disminuir la cantidad de historial decodificado visible.

## Solución de problemas

- **La etiqueta de estadísticas CW está en blanco o no se actualiza** — El decodificador no ha adquirido una señal. Verifique que el audio de la PC esté enrutado correctamente (la etiqueta de sugerencia dice `(requires PC Audio)`), que la señal esté dentro de los límites del control deslizante de rango de afinación y que Sens no esté configurado tan alto que todas las decodificaciones sean rechazadas.
- **La afinación bloqueada no produce salida después de sintonizar fuera y volver** — Bloquear la afinación mantiene el decodificador en la frecuencia en el momento del bloqueo. Si reajustó el VFO, la afinación de la señal vista por el decodificador puede haberse desplazado. Libere 🔒P, reajuste y vuelva a bloquear una vez que la etiqueta de estadísticas se estabilice.
- **El texto decodificado del lado TX no aparece** — Asegúrese de que el audio de la PC esté enrutado tanto para las rutas de recepción como de transmisión. El decodificador CW solo genera salida TX cuando hay audio disponible de su clave transmitida.

## Relacionados

- [Activar el decodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Ajustar la sensibilidad del decodificador CW para rechazar ruido](tune-cw-decoder-sensitivity-to-reject-noise.md)
- [Copiar texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)
