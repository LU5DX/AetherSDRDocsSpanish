# Resumen del ecualizador gráfico

El applet Ecualizador (Gráfico) proporciona un ecualizador gráfico de 8 bandas que funciona dentro del propio radio Flex, aplicado a través de la API TCP/IP del radio. Úselo para dar forma a la respuesta en frecuencia del audio recibido o de la señal transmitida en ocho bandas de octava fijas de 63 Hz a 8 kHz.

Este ecualizador es independiente de cualquier ecualización paramétrica del lado del cliente en AetherSDR. Los cambios se aplican en el DSP del radio, no en el software de su computadora.

## Antes de comenzar

- Conecte AetherSDR a un radio Flex. El applet requiere una conexión activa al radio.
- Haga visible el panel de applets. Si está oculto, vaya a `View > Applet Panel` para mostrarlo.

## Cómo funciona

Haga clic en el botón EQ de la barra lateral derecha para abrir o cerrar el panel del ecualizador. El panel aparece en la fila superior del panel de applets.

El applet siempre muestra una ruta a la vez — ya sea RX o TX. Use los botones RX y TX para cambiar la ruta que está viendo y editando. El applet se abre en la vista TX de forma predeterminada. AetherSDR recuerda la última vista seleccionada (RX o TX) entre sesiones; si cierra el applet mientras ve el ecualizador RX, se abrirá en RX la próxima vez que inicie el programa.

Cada una de las ocho bandas tiene un control deslizante vertical. Mover un control deslizante envía el nuevo valor al radio de inmediato; el valor en dB debajo de cada control deslizante se actualiza en vivo. Mientras arrastra un control deslizante, aparece una ventana emergente cerca del control que muestra el valor actual en dB (formateado con signo, p. ej., "+3 dB" o "-5 dB"). Activar o desactivar el ecualizador con el botón ON también tiene efecto inmediato en la ruta seleccionada actualmente.

Cuando ajusta un control deslizante usando el teclado (por ejemplo, con las teclas de flecha), aparece brevemente una ventana emergente con el nuevo valor, que luego permanece y se desvanece con el mismo tiempo de espera que al soltar el mouse. Esto le permite leer el valor final después de un paso con el teclado.

Las rutas RX y TX son independientes. Puede tener curvas diferentes en cada una, y activarlas o desactivarlas por separado.

## Función de cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Apagado (desmarcado) | Encendido / Apagado | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (RX o TX). Se resalta en verde cuando está activado. |
| Reset arc (icono de revertir) | Botón pulsador | — | — | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Información sobre herramientas: "Restablecer todas las bandas a 0 dB". |
| RX | Botón de alternancia | Apagado (desmarcado) | Encendido / Apagado | Selecciona la ruta del ecualizador de recepción para visualización y edición. Se resalta en azul cuando está activo. Mutuamente excluyente con TX. |
| TX | Botón de alternancia | Encendido (marcado) | Encendido / Apagado | Selecciona la ruta del ecualizador de transmisión para visualización y edición. Se resalta en azul cuando está activo. Mutuamente excluyente con RX. |
| 63 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada. Muestra una ventana emergente de valor de arrastre mientras se mueve el control deslizante o se ajusta con el teclado. |
| 125 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. Muestra una ventana emergente de valor de arrastre mientras se mueve el control deslizante o se ajusta con el teclado. |
| 250 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. Muestra una ventana emergente de valor de arrastre mientras se mueve el control deslizante o se ajusta con el teclado. |
| 500 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. Muestra una ventana emergente de valor de arrastre mientras se mueve el control deslizante o se ajusta con el teclado. |
| 1k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. Muestra una ventana emergente de valor de arrastre mientras se mueve el control deslizante o se ajusta con el teclado. |
| 2k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. Muestra una ventana emergente de valor de arrastre mientras se mueve el control deslizante o se ajusta con el teclado. |
| 4k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. Muestra una ventana emergente de valor de arrastre mientras se mueve el control deslizante o se ajusta con el teclado. |
| 8k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. Muestra una ventana emergente de valor de arrastre mientras se mueve el control deslizante o se ajusta con el teclado. |
| Etiqueta de valor por banda | Indicador | 0 | −10 a +10 | Muestra el valor actual en dB de cada banda debajo de su control deslizante. Se actualiza en vivo al mover el control deslizante. |
| Escala +10 / 0 / −10 dB | Indicador | — | — | Etiquetas de referencia en los bordes izquierdo y derecho del área de los controles deslizantes que muestran el rango de los mismos. |

Ningún valor de banda de este applet se guarda en la configuración local de AetherSDR; todos los valores se almacenan y recuperan del radio. La selección de vista RX/TX se almacena localmente para que el applet se vuelva a abrir en la ruta que usó por última vez.

## Compatibilidad con temas

El applet Ecualizador es totalmente compatible con el cambio de temas en vivo. Al cambiar de tema, los siguientes elementos visuales se actualizan automáticamente:

- Fondo de la ranura del control deslizante, color del control deslizante y relleno de sub-página/agregar página
- Colores de las etiquetas de banda
- Colores de las etiquetas de escala (+10, 0, −10)
- Colores de fondo del botón de restablecimiento y color de acento al presionarlo
- Fondo general del contenedor del applet

Los controles deslizantes usan el color de acento de primer plano (relleno) del tema, en lugar del token de control deslizante estándar, para coincidir con la apariencia visual prevista. Las áreas de sub-página y agregar página de la ranura mantienen el color de fondo de la ranura para evitar rellenos de acento no deseados del estilo de control deslizante global.

## Consejos

- Debido a que RX y TX son rutas independientes, puede dejar la ecualización de TX plana mientras da forma solo al audio de RX, o viceversa.
- Use ON para comparar rápidamente el audio ecualizado versus el plano sin mover ningún control deslizante. Actívelo y desactívelo mientras escucha para evaluar su curva.
- El botón de restablecimiento (reset arc) restablece las ocho bandas a la vez. Si solo desea ajustar una banda, mueva ese control deslizante manualmente de vuelta a 0.
- La ventana emergente de valor de arrastre aparece cerca del control deslizante mientras lo arrastra. La ventana emergente permanece brevemente después de soltar el botón del mouse para que pueda leer el valor final. Al ajustar los controles deslizantes con el teclado, aparece un destello de la ventana emergente que muestra el nuevo valor y luego se desvanece con la misma duración que al soltar el mouse.
- El applet recuerda si estaba en RX o TX la última vez que lo usó, incluso después de reiniciar el programa.

## Relacionados

- [Enable radio-side graphic EQ for TX](enable-radio-side-graphic-eq-for-tx.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
