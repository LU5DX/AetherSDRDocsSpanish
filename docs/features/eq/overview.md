# Resumen del ecualizador gráfico

El applet Equalizer (Graphic) proporciona un ecualizador gráfico de 8 bandas que se ejecuta dentro del propio radio Flex, aplicado mediante la API TCP/IP del radio. Úselo para dar forma a la respuesta de frecuencia del audio recibido o de la señal transmitida en ocho bandas de octava fijas, de 63 Hz a 8 kHz.

Este ecualizador es independiente de cualquier EQ paramétrico del lado del cliente en AetherSDR. Los cambios tienen efecto en el DSP del radio, no en el software de su computadora.

## Antes de comenzar

- Conecte AetherSDR a un radio Flex. El applet requiere una conexión activa al radio.
- Haga visible el panel de applets. Si está oculto, vaya a `View > Applet Panel` para mostrarlo.

## Cómo funciona

Haga clic en el botón de la bandeja EQ en la barra lateral derecha para abrir o cerrar el mosaico Equalizer. El mosaico aparece en la fila superior del panel de applets.

El applet siempre muestra una ruta a la vez — RX o TX. Use los botones RX y TX para cambiar qué ruta está viendo y editando. El applet se abre en la vista TX de forma predeterminada. AetherSDR recuerda la última vista seleccionada (RX o TX) entre sesiones — si cierra el applet mientras ve el ecualizador RX, se abrirá en RX la próxima vez que inicie el programa.

Cada una de las ocho bandas tiene un control deslizante vertical. Al mover un control deslizante, el nuevo valor se envía al radio inmediatamente; el valor en dB debajo de cada control se actualiza en vivo. Mientras arrastra un control deslizante, aparece una ventana emergente cerca del control que muestra el valor actual en dB (con signo, por ejemplo, "+3 dB" o "-5 dB"). Activar o desactivar el ecualizador con ON también tiene efecto inmediato en la ruta seleccionada actualmente.

Cuando ajusta un control deslizante con el teclado (por ejemplo, con las teclas de flecha), aparece una ventana emergente de valor de arrastre que muestra el nuevo valor, luego permanece y se desvanece con el mismo tiempo de espera que al soltar el mouse. Esto le permite leer el valor final después de un paso con el teclado.

Las rutas RX y TX son independientes. Puede tener curvas diferentes en cada una y activarlas o desactivarlas por separado.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Desactivado (sin marcar) | Activado / Desactivado | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (RX o TX). Se resalta en verde cuando está activado. |
| Botón de reinicio (ícono de revertir) | Botón pulsador | — | — | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Información sobre herramientas: "Reset all bands to 0 dB". |
| RX | Botón de alternancia | Desactivado (sin marcar) | Activado / Desactivado | Selecciona la ruta del ecualizador de recepción para visualización y edición. Se resalta en azul cuando está activo. Mutuamente excluyente con TX. |
| TX | Botón de alternancia | Activado (marcado) | Activado / Desactivado | Selecciona la ruta del ecualizador de transmisión para visualización y edición. Se resalta en azul cuando está activo. Mutuamente excluyente con RX. |
| 63 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada. |
| 125 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. |
| 250 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. |
| 500 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. |
| 1k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. |
| 2k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. |
| 4k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. |
| 8k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. |
| Etiqueta de valor por banda | Indicador | 0 | −10 a +10 | Muestra el valor actual en dB de cada banda debajo de su control deslizante. Se actualiza en vivo mientras mueve el control. |
| Escala de +10 / 0 / −10 dB | Indicador | — | — | Etiquetas de referencia en los bordes izquierdo y derecho del área de los controles deslizantes que muestran el rango del control. |

Ningún valor de los controles deslizantes de banda de este applet se guarda en la configuración local de AetherSDR; todos los valores de los controles se almacenan y se recuperan del radio. La selección de vista RX/TX se guarda localmente para que el applet se reabra en la ruta de su último uso.

## Compatibilidad con temas

El applet Equalizer es totalmente compatible con el cambio de tema en vivo. Cuando cambia de tema, los siguientes elementos visuales se actualizan automáticamente:

- Fondo de la ranura del control deslizante, color del mango y relleno de subpágina/añadir página
- Colores de las etiquetas de banda
- Colores de las etiquetas de escala (+10, 0, −10)
- Colores de fondo del botón de reinicio y color de acento al presionarlo
- Fondo general del contenedor del applet

Los mangos de los controles deslizantes usan el color de acento de relleno (primer plano) del tema en lugar del token estándar de mango para coincidir con la expresión visual prevista. Las áreas de subpágina y añadir página de la ranura mantienen el color de fondo de la ranura para evitar rellenos de acento no deseados del estilo global del control deslizante.

Los controles deslizantes de banda también reciben una corrección automática de supresión al pasar el mouse que evita que aparezcan píxeles obsoletos en escalas de interfaz fraccionarias cuando el mouse se mueve sobre ellos, lo que garantiza una representación limpia en todos los niveles de zoom de la pantalla.

## Consejos

- Debido a que las rutas RX y TX son independientes, puede dejar la ecualización TX plana mientras moldea solo el audio RX, o viceversa.
- Use ON para comparar rápidamente el audio ecualizado versus el audio plano sin mover ningún control. Actívelo y desactívelo mientras escucha para evaluar su curva.
- El botón de reinicio restablece las ocho bandas a la vez. Si solo desea ajustar una banda, mueva únicamente ese control de vuelta a 0 manualmente.
- La ventana emergente de valor de arrastre aparece cerca del control deslizante mientras arrastra. La ventana permanece brevemente después de soltar el botón del mouse para que pueda leer el valor final. Al ajustar los controles con el teclado, un destello de la ventana muestra el nuevo valor, luego se desvanece con la misma duración de permanencia que al soltar el mouse.
- El applet recuerda si estaba en RX o TX en su último uso, incluso entre reinicios del programa.

## Relacionados

- [Habilitar EQ gráfico del radio para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Habilitar EQ gráfico del radio para RX](enable-radio-side-graphic-eq-for-rx.md)
- [Aumentar o cortar bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Restablecer todas las bandas a planas con un clic](reset-all-bands-to-flat-with-one-click.md)
- [Cambiar entre moldear audio RX y audio TX](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Comparar EQ activado vs EQ desactivado rápidamente con el botón ON](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
