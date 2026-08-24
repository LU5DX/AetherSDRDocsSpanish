# Ecualizador (Gráfico)

El applet del Ecualizador es un ecualizador gráfico de 8 bandas aplicado **dentro del propio radio** mediante la API TCP/IP. Es independiente del EQ paramétrico del lado del cliente. Las bandas fijas están en 63, 125, 250, 500 Hz y 1, 2, 4, 8 kHz; cada control deslizante ajusta ±10 dB.

## Cambiar entre dar forma al audio de RX y al audio de TX

El applet del Ecualizador mantiene ajustes de banda separados para las rutas de recepción y transmisión. Use los botones de selector RX y TX para elegir sobre qué ruta actúan los controles deslizantes y el botón ON. El applet recuerda la vista (RX o TX) que usó por última vez y se reabre en esa vista cuando reinicie AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet del EQ requiere una conexión activa al radio.
- Abra el mosaico del Ecualizador haciendo clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha.

## Pasos

1. Haga clic en el botón EQ de la bandeja en la barra lateral derecha para abrir el mosaico del Ecualizador si aún no está visible.
2. Para editar la ruta de recepción, haga clic en RX. Los controles deslizantes y el botón ON ahora reflejan y controlan las bandas del ecualizador de RX.
3. Para editar la ruta de transmisión, haga clic en TX. Los controles deslizantes y el botón ON ahora reflejan y controlan las bandas del ecualizador de TX.
4. La próxima vez que abra el mosaico del Ecualizador, se mostrará la misma vista (RX o TX) que seleccionó por última vez.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| RX | Botón de alternancia | Sin marcar en el primer inicio; luego recuerda la última selección | — | Selecciona la ruta del ecualizador de recepción para visualización y edición. Resaltado azul cuando está activo. |
| TX | Botón de alternancia | Marcado en el primer inicio; luego recuerda la última selección | — | Selecciona la ruta del ecualizador de transmisión para visualización y edición. Resaltado azul cuando está activo. El applet se abre en la vista TX en el primer inicio. |
| ON | Botón de alternancia | Sin marcar | — | Activa o desactiva el ecualizador para la ruta (RX o TX) actualmente seleccionada. Resaltado verde cuando está habilitado. |
| 63 | Control deslizante | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada; la etiqueta de valor debajo del control se actualiza en vivo. Mientras arrastra, una ventana emergente muestra el valor dB con signo. |
| 125 | Control deslizante | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo. |
| 250 | Control deslizante | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo. |
| 500 | Control deslizante | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo. |
| 1k | Control deslizante | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo. |
| 2k | Control deslizante | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo. |
| 4k | Control deslizante | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo. |
| 8k | Control deslizante | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo. |
| Arco de restablecimiento (icono de revertir) | Botón pulsador | — | — | Restablece las 8 bandas de la ruta actualmente seleccionada a 0 dB. Información sobre herramientas: "Restablecer todas las bandas a 0 dB". Se dibuja como una flecha de 3/4 de círculo. |
| Escala +10 / 0 / −10 dB | Indicador | — | — | Etiquetas de referencia izquierda y derecha que muestran el rango de ±10 dB de los controles deslizantes. |

## Indicadores

| Etiqueta | Estados | Significado |
|---|---|---|
| Etiqueta de valor por banda | −10 a +10 | Valor dB en vivo de cada control deslizante mostrado debajo de su manija. |

## Consejos

- RX y TX son mutuamente excluyentes. Al hacer clic en uno se deselecciona automáticamente el otro. No puede editar ambas rutas al mismo tiempo.
- El botón ON, todos los controles deslizantes y el botón de restablecimiento operan siempre sobre la ruta actualmente seleccionada. Cambie a RX antes de restablecer o ajustar si tiene la intención de modificar la ruta de recepción.
- Cuando cambie de TX a RX (o viceversa), los controles deslizantes se actualizan inmediatamente para mostrar los valores almacenados de la ruta recién seleccionada. Sus cambios en la ruta anterior no se pierden.
- La vista seleccionada por última vez (RX o TX) se guarda en la configuración de su aplicación (`EqApplet.showTx`). Esto persiste entre reinicios de AetherSDR. En el primer inicio, el applet se abre por defecto en la vista TX.
- Mientras arrastra cualquier control deslizante de banda, aparece una pequeña ventana emergente cerca de la manija del control que muestra el valor dB con signo actual (por ejemplo, "+3 dB" o "-5 dB"). La ventana emergente permanece brevemente después de soltar el botón del mouse.
- También puede ajustar los controles deslizantes mediante atajos de teclado. Cuando mueve un control deslizante con el teclado (por ejemplo, presionando la tecla de flecha Arriba o Abajo mientras el control tiene el foco), la insignia de valor emergente aparece cerca del centro de la manija del control y permanece con el mismo tiempo de espera que al soltar el mouse. Esto proporciona retroalimentación visual para los ajustes con teclado sin necesidad de arrastrar el mouse.
- El applet del Ecualizador admite cambio de tema en vivo. Las manijas de los controles deslizantes y las etiquetas actualizan automáticamente sus colores cuando cambia el tema activo. La ranura del control deslizante no cambia de color, lo que garantiza que la manija siga siendo el único elemento con color de acento en la columna de banda.

## Relacionado

- [Descripción general del Ecualizador (Gráfico)](overview.md)
- [Habilitar EQ gráfico del lado del radio para RX](enable-radio-side-graphic-eq-for-rx.md)
- [Habilitar EQ gráfico del lado del radio para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Aumentar o reducir bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Restablecer todas las bandas a planas con un clic](reset-all-bands-to-flat-with-one-click.md)
