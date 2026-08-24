# Aumente o recorte bandas de octava específicas (63 Hz a 8 kHz)

Use el applet Equalizer para subir o bajar bandas de frecuencia individuales en la ruta de audio de recepción o transmisión de la radio. Cada una de las ocho bandas se puede ajustar en cualquier punto entre −10 dB y +10 dB.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Equalizer requiere una conexión activa con la radio.
- Decida si va a dar forma a la ruta RX o TX antes de mover los controles deslizantes.

## Pasos

1. Haga clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha para abrir el mosaico Equalizer.
2. Haga clic en TX para editar la ruta de transmisión, o haga clic en RX para editar la ruta de recepción. TX está seleccionado por defecto cuando se abre el applet. La vista seleccionada por última vez se recuerda y se restaura la próxima vez que abra el applet.
3. Haga clic en ON para habilitar el ecualizador en la ruta seleccionada. ON se resalta en verde cuando está activo.
4. Arrastre el control deslizante de la banda que desea ajustar. Las bandas están etiquetadas como **63**, **125**, **250**, **500**, **1k**, **2k**, **4k** y **8k** (Hz y kHz respectivamente). Arrastre hacia arriba para aumentar, arrastre hacia abajo para recortar.
5. Mientras arrastra, aparece una etiqueta emergente cerca del control deslizante que muestra el valor actual en dB (p. ej., "+3 dB" o "−5 dB"). Lea la etiqueta de valor directamente debajo de cada control deslizante para confirmar la cantidad en dB. La etiqueta se actualiza en vivo mientras arrastra.
6. También puede ajustar un control deslizante con las teclas de flecha del teclado (Arriba/Abajo o Izquierda/Derecha) cuando el control deslizante tiene el foco. La etiqueta emergente aparece y permanece brevemente después de soltar la tecla, igual que después de arrastrar con el mouse.
7. Repita los pasos 4–6 para cualquier otra banda que desee ajustar.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Apagado (desmarcado) | On / Off | Habilita o deshabilita el ecualizador para la ruta seleccionada actualmente. Se resalta en verde cuando está habilitado. |
| RX | Botón de alternancia | Desmarcado | — | Cambia el applet para mostrar y editar las bandas del ecualizador de recepción. Se resalta en azul cuando está activo. |
| TX | Botón de alternancia | Marcado | — | Cambia el applet para mostrar y editar las bandas del ecualizador de transmisión. Se resalta en azul cuando está activo. Comienza marcado: el applet se abre en la vista TX. |
| Botón de arco Reset | Botón pulsador | — | — | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Información sobre herramientas: "Reset all bands to 0 dB". Se dibuja como una flecha de arco de 3/4 de círculo. |
| 63 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada. Arrastre hacia arriba para aumentar, hacia abajo para recortar. Una ventana emergente muestra el valor exacto mientras arrastra y permanece brevemente después de soltar. El ajuste con teclas de flecha también muestra la ventana emergente. |
| 125 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. Arrastre hacia arriba para aumentar, hacia abajo para recortar. Una ventana emergente muestra el valor exacto mientras arrastra y permanece brevemente después de soltar. El ajuste con teclas de flecha también muestra la ventana emergente. |
| 250 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. Arrastre hacia arriba para aumentar, hacia abajo para recortar. Una ventana emergente muestra el valor exacto mientras arrastra y permanece brevemente después de soltar. El ajuste con teclas de flecha también muestra la ventana emergente. |
| 500 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. Arrastre hacia arriba para aumentar, hacia abajo para recortar. Una ventana emergente muestra el valor exacto mientras arrastra y permanece brevemente después de soltar. El ajuste con teclas de flecha también muestra la ventana emergente. |
| 1k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. Arrastre hacia arriba para aumentar, hacia abajo para recortar. Una ventana emergente muestra el valor exacto mientras arrastra y permanece brevemente después de soltar. El ajuste con teclas de flecha también muestra la ventana emergente. |
| 2k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. Arrastre hacia arriba para aumentar, hacia abajo para recortar. Una ventana emergente muestra el valor exacto mientras arrastra y permanece brevemente después de soltar. El ajuste con teclas de flecha también muestra la ventana emergente. |
| 4k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. Arrastre hacia arriba para aumentar, hacia abajo para recortar. Una ventana emergente muestra el valor exacto mientras arrastra y permanece brevemente después de soltar. El ajuste con teclas de flecha también muestra la ventana emergente. |
| 8k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. Arrastre hacia arriba para aumentar, hacia abajo para recortar. Una ventana emergente muestra el valor exacto mientras arrastra y permanece brevemente después de soltar. El ajuste con teclas de flecha también muestra la ventana emergente. |
| Escala +10 / 0 / −10 dB | Etiquetas de referencia | — | — | Etiquetas de referencia izquierda y derecha que muestran el rango de +/-10 dB de los controles deslizantes. |
| Etiqueta de valor por banda | Indicador | 0 | −10 a +10 | Muestra el valor en dB en vivo del control deslizante directamente debajo de su manija. |
| Ventana emergente de arrastre | Indicador | Ninguno | −10 a +10 | Etiqueta flotante que aparece cerca de la manija del control deslizante durante operaciones de arrastre o después de un ajuste con teclas de flecha. Muestra el valor actual en dB con signo (p. ej., "+3 dB" o "−5 dB"). Permanece por un momento después de soltar el botón del mouse o la tecla del teclado. |

## Consejos

- Los ajustes de RX y TX son independientes. Ajustar las bandas mientras TX está seleccionado no tiene efecto en la curva RX, y viceversa.
- Las etiquetas de escala +10 / 0 / −10 dB en los bordes izquierdo y derecho de la columna de controles deslizantes ofrecen una referencia visual del punto medio (0 dB) y los límites.
- Para devolver rápidamente todas las bandas a planas sin mover cada control deslizante individualmente, haga clic en el botón de arco Reset.
- El applet recuerda si usó la vista RX o TX por última vez. Cuando vuelva a abrir el mosaico Equalizer, mostrará la misma vista que estaba usando antes, ahorrándole un clic.
- La ventana emergente de arrastre muestra un valor en dB con signo (p. ej., "+3 dB" para valores positivos, "−3 dB" para valores negativos, "0 dB" para cero) para coincidir con el formato utilizado en el resto de la aplicación.
- Los colores de la manija del control deslizante y la ranura se adaptan al tema activo. El color de la manija usa el color de acento, mientras que el fondo de la ranura usa el color de la pista del control deslizante del tema actual.
- Mover el control deslizante anterior o siguiente con la tecla Tab del teclado no activa la ventana emergente. Solo las teclas de flecha en un control deslizante con foco muestran la ventana emergente.

## Solución de problemas

- **Los controles deslizantes se mueven pero el audio no se ve afectado** — Verifique que ON esté resaltado en verde para la ruta activa. El ecualizador no tiene efecto cuando ON está desmarcado, incluso si los controles deslizantes están configurados en valores distintos de cero.
- **Ajustar los controles deslizantes en la ruta TX cambia lo que escucha en RX** — Es posible que esté en la ruta equivocada. Haga clic en RX para confirmar que está editando las bandas de recepción, o haga clic en TX para transmisión. Las dos rutas son independientes; solo se está editando la ruta mostrada actualmente.

## Relacionado

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for TX](enable-radio-side-graphic-eq-for-tx.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
