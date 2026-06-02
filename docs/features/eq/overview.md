# Descripción general del Ecualizador (Gráfico)

La applet Ecualizador (Gráfico) proporciona un ecualizador gráfico de 8 bandas que se ejecuta dentro del propio radio Flex, aplicado a través de la API TCP/IP del radio. Úselo para dar forma a la respuesta de frecuencia del audio recibido o de la señal transmitida en ocho bandas fijas de octava, desde 63 Hz hasta 8 kHz.

Este ecualizador es independiente de cualquier ecualizador paramétrico del lado del cliente en AetherSDR. Los cambios tienen efecto en el DSP del radio, no en el software de su computadora.

## Antes de comenzar

- Conecte AetherSDR a un radio Flex. La applet requiere una conexión activa con el radio.
- Haga visible el panel de applets. Si está oculto, vaya a `View > Applet Panel` para mostrarlo.

## Cómo funciona

Haga clic en el botón de la bandeja EQ en la barra lateral derecha para abrir o cerrar el mosaico del Ecualizador. El mosaico aparece en la fila superior del panel de applets.

La applet siempre muestra una ruta a la vez — ya sea RX o TX. Use los botones RX y TX para cambiar qué ruta está viendo y editando. La applet se abre en la vista TX de forma predeterminada. AetherSDR recuerda la última vista seleccionada (RX o TX) entre sesiones; si cierra la applet mientras ve el ecualizador RX, se abrirá en RX la próxima vez que inicie el programa.

Cada una de las ocho bandas tiene un control deslizante vertical. Mover un control deslizante envía el nuevo valor al radio inmediatamente; el valor en dB debajo de cada control deslizante se actualiza en vivo. Mientras arrastra un control deslizante, aparece una ventana emergente cerca del control que muestra el valor actual en dB (formateado con un signo, por ejemplo, "+3 dB" o "-5 dB"). Activar o desactivar el ecualizador con ON también tiene efecto inmediato en la ruta seleccionada actualmente.

Las rutas RX y TX son independientes. Puede tener curvas diferentes en cada una y activarlas o desactivarlas por separado.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Apagado (desmarcado) | Encendido / Apagado | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (RX o TX). Se resalta en verde cuando está activado. |
| Botón de reinicio (icono de deshacer) | Botón pulsador | — | — | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Información sobre herramientas: "Restablecer todas las bandas a 0 dB". |
| RX | Botón de alternancia | Apagado (desmarcado) | Encendido / Apagado | Selecciona la ruta del ecualizador de recepción para visualización y edición. Se resalta en azul cuando está activo. Excluyente con TX. |
| TX | Botón de alternancia | Encendido (marcado) | Encendido / Apagado | Selecciona la ruta del ecualizador de transmisión para visualización y edición. Se resalta en azul cuando está activo. Excluyente con RX. |
| 63 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante. |
| 125 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante. |
| 250 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante. |
| 500 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante. |
| 1k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante. |
| 2k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante. |
| 4k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante. |
| 8k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. Muestra una ventana emergente con el valor de arrastre mientras se mueve el control deslizante. |
| Etiqueta de valor por banda | Indicador | 0 | −10 a +10 | Muestra el valor actual en dB de cada banda debajo de su control deslizante. Se actualiza en vivo a medida que se mueve el control deslizante. |
| Escala +10 / 0 / −10 dB | Indicador | — | — | Etiquetas de referencia en los bordes izquierdo y derecho del área de controles deslizantes que muestran el rango del control deslizante. |

Ningún valor de los controles deslizantes de banda de esta applet se conserva en la configuración local de AetherSDR; todos los valores de los controles deslizantes se almacenan y recuperan del radio. La selección de vista RX/TX se almacena localmente para que la applet se reabra en su última ruta utilizada.

## Compatibilidad con temas

La applet Ecualizador es totalmente compatible con el cambio de tema en vivo. Cuando cambia de tema, los siguientes elementos visuales se actualizan automáticamente:

- Fondo de la ranura del control deslizante, color del control y relleno de sub-página/agregar-página
- Colores de las etiquetas de banda
- Colores de las etiquetas de escala (+10, 0, −10)
- Colores de fondo del botón de reinicio y color de acento al presionarlo
- Fondo general del contenedor de la applet

Los controles deslizantes usan el color de acento de primer plano (relleno) del tema en lugar del token de control estándar para coincidir con la expresión visual prevista. Las áreas de sub-página y agregar-página de la ranura mantienen el color de fondo de la ranura para evitar rellenos de acento no deseados del estilo de control deslizante global.

## Consejos

- Debido a que RX y TX son rutas independientes, puede dejar la ecualización de TX plana mientras da forma solo al audio de RX, o viceversa.
- Use ON para comparar rápidamente el audio ecualizado con el audio plano sin mover ningún control deslizante. Actívelo y desactívelo mientras escucha para evaluar su curva.
- El botón de reinicio restablece las ocho bandas a la vez. Si solo desea ajustar una banda, mueva ese control deslizante manualmente de vuelta a 0.
- La ventana emergente con el valor de arrastre aparece cerca del control deslizante mientras lo arrastra. La ventana emergente permanece brevemente después de soltar el botón del mouse para que pueda leer el valor final.
- La applet recuerda si estaba en RX o TX la última vez que la usó, incluso después de reiniciar el programa.

## Relacionados

- [Enable radio-side graphic EQ for TX](enable-radio-side-graphic-eq-for-tx.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
