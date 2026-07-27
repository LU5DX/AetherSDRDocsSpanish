# Resumen del Ecualizador (Gráfico)

El applet Ecualizador (Gráfico) proporciona un ecualizador gráfico de 8 bandas que se ejecuta dentro del propio radio Flex, aplicado a través de la API TCP/IP del radio. Úselo para dar forma a la respuesta de frecuencia de su audio recibido o su señal transmitida en ocho bandas fijas de octava de 63 Hz a 8 kHz.

Este ecualizador es independiente de cualquier ecualizador paramétrico del lado del cliente en AetherSDR. Los cambios surten efecto en el DSP del radio, no en el software de su computadora.

## Antes de comenzar

- Conecte AetherSDR a un radio Flex. El applet requiere una conexión activa al radio.
- Haga visible el panel de applets. Si está oculto, vaya a `View > Applet Panel` para mostrarlo.

## Cómo funciona

Haga clic en el botón de la bandeja EQ en la barra lateral derecha para abrir o cerrar el mosaico del Ecualizador. El mosaico aparece en la fila superior del panel de applets.

El applet siempre muestra una ruta a la vez — ya sea RX o TX. Use los botones RX y TX para cambiar qué ruta está viendo y editando. El applet se abre en la vista TX de forma predeterminada. AetherSDR recuerda la última vista seleccionada (RX o TX) entre sesiones; si cierra el applet mientras ve el ecualizador RX, se abrirá en RX la próxima vez que inicie el programa.

Cada una de las ocho bandas tiene un control deslizante vertical. Mover un control deslizante envía el nuevo valor al radio inmediatamente; el valor en dB debajo de cada control deslizante se actualiza en vivo. Mientras arrastra un control deslizante, aparece una ventana emergente cerca del control deslizante que muestra el valor actual en dB (formateado con un signo, por ejemplo, "+3 dB" o "-5 dB"). Activar o desactivar el ecualizador con ON también surte efecto inmediatamente en la ruta seleccionada actualmente.

Cuando ajusta un control deslizante usando el teclado (por ejemplo, mediante teclas de flecha), aparece una ventana emergente con el valor de arrastre que muestra el nuevo valor, luego permanece y se desvanece con el mismo tiempo de espera que una liberación del mouse. Esto le permite leer el valor final después de un paso del teclado.

Las rutas RX y TX son independientes. Puede tener curvas diferentes en cada una y activarlas o desactivarlas por separado.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Apagado (desmarcado) | Encendido / Apagado | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (RX o TX). Se resalta en verde cuando está activado. |
| Arco de reinicio (icono de revertir) | Botón de pulsación | — | — | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Sugerencia: "Restablecer todas las bandas a 0 dB". |
| RX | Botón de alternancia | Apagado (desmarcado) | Encendido / Apagado | Selecciona la ruta del ecualizador de recepción para mostrar y editar. Se resalta en azul cuando está activo. Mutuamente excluyente con TX. |
| TX | Botón de alternancia | Encendido (marcado) | Encendido / Apagado | Selecciona la ruta del ecualizador de transmisión para mostrar y editar. Se resalta en azul cuando está activo. Mutuamente excluyente con RX. |
| 63 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante o se ajusta mediante el teclado. Las subclases pueden anular los controladores del mouse para un comportamiento de arrastre personalizado, como el posicionamiento con un clic para saltar, mientras se preserva la visualización emergente. |
| 125 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante o se ajusta mediante el teclado. |
| 250 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante o se ajusta mediante el teclado. |
| 500 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante o se ajusta mediante el teclado. |
| 1k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante o se ajusta mediante el teclado. |
| 2k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante o se ajusta mediante el teclado. |
| 4k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante o se ajusta mediante el teclado. |
| 8k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante o se ajusta mediante el teclado. |
| Etiqueta de valor por banda | Indicador | 0 | −10 a +10 | Muestra el valor actual en dB de cada banda debajo de su control deslizante. Se actualiza en vivo mientras mueve el control deslizante. |
| Escala +10 / 0 / −10 dB | Indicador | — | — | Etiquetas de referencia en los bordes izquierdo y derecho del área del control deslizante que muestran el rango del control deslizante. |

Ningún valor de control deslizante de banda de este applet se conserva en la configuración local de AetherSDR; todos los valores de los controles deslizantes se almacenan y recuperan del radio. La selección de vista RX/TX se almacena localmente para que el applet se vuelva a abrir en la ruta utilizada por última vez.

## Soporte de temas

El applet Ecualizador es totalmente compatible con el cambio de tema en vivo. Cuando cambia de tema, los siguientes elementos visuales se actualizan automáticamente:

- Fondo de la ranura del control deslizante, color del control deslizante y relleno de subpágina/página adicional
- Colores de las etiquetas de banda
- Colores de las etiquetas de escala (+10, 0, −10)
- Colores de fondo del botón de reinicio y color de acento al presionar
- Fondo general del contenedor del applet

Los controles deslizantes usan el color de acento de primer plano (relleno) del tema en lugar del token de control deslizante estándar para que coincida con la expresión visual prevista. Las áreas de subpágina y página adicional de la ranura permanecen con el color de fondo de la ranura para evitar rellenos de acento no deseados del estilo de control deslizante global.

## Consejos

- Debido a que RX y TX son rutas independientes, puede dejar la ecualización de TX plana mientras da forma solo al audio de RX, o viceversa.
- Use ON para comparar rápidamente el audio ecualizado frente al audio plano sin mover ningún control deslizante. Actívelo y desactívelo mientras escucha para evaluar su curva.
- El botón de arco de reinicio restablece las ocho bandas a la vez. Si solo desea ajustar una banda, mueva ese control deslizante de vuelta a 0 manualmente.
- La ventana emergente con el valor de arrastre aparece cerca del control deslizante mientras lo arrastra. La ventana emergente permanece brevemente después de soltar el botón del mouse para que pueda leer el valor final. Al ajustar los controles deslizantes mediante el teclado, aparece un destello de la ventana emergente que muestra el nuevo valor y luego se desvanece con la misma duración de permanencia que una liberación del mouse.
- El applet recuerda si estaba en RX o TX la última vez que lo usó, incluso después de reiniciar el programa.

## Relacionados

- [Activar EQ gráfico del lado del radio para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Activar EQ gráfico del lado del radio para RX](enable-radio-side-graphic-eq-for-rx.md)
- [Aumentar o cortar bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Restablecer todas las bandas a plano con un clic](reset-all-bands-to-flat-with-one-click.md)
- [Cambiar entre dar forma al audio de RX y al audio de TX](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Comparar EQ activado vs EQ desactivado rápidamente con el botón ON](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
