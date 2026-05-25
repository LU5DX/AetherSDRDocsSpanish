# Resumen del ecualizador gráfico

El applet Equalizer (Graphic) proporciona un ecualizador gráfico de 8 bandas que se ejecuta dentro del propio radio Flex, aplicado a través de la API TCP/IP del radio. Úselo para dar forma a la respuesta en frecuencia del audio recibido o de la señal transmitida en ocho bandas de octava fijas, desde 63 Hz hasta 8 kHz.

Este ecualizador es independiente de cualquier EQ paramétrico del lado del cliente en AetherSDR. Los cambios surten efecto en el DSP del radio, no en el software de su computadora.

## Antes de comenzar

- Conecte AetherSDR a un radio Flex. El applet requiere una conexión activa con el radio.
- Haga visible el panel de applets. Si está oculto, vaya a `View > Applet Panel` para mostrarlo.

## Cómo funciona

Haga clic en el botón EQ en la barra lateral derecha para abrir o cerrar el panel del ecualizador. El panel aparece en la fila superior del panel de applets.

El applet siempre muestra una ruta a la vez — RX o TX. Use los botones RX y TX para cambiar qué ruta está viendo y editando. El applet se abre en la vista TX de forma predeterminada. AetherSDR recuerda la última vista seleccionada (RX o TX) entre sesiones — si cierra el applet mientras ve el ecualizador de RX, se abrirá en RX la próxima vez que inicie el programa.

Cada una de las ocho bandas tiene un control deslizante vertical. Mover un control deslizante envía el nuevo valor al radio de inmediato; el valor en dB debajo de cada control deslizante se actualiza en vivo. Mientras arrastra un control deslizante, aparece un mensaje emergente cerca del control mostrando el valor actual en dB (formateado con un signo, por ejemplo, "+3 dB" o "-5 dB"). Habilitar o deshabilitar el ecualizador con ON también surte efecto de inmediato en la ruta seleccionada actualmente.

Las rutas RX y TX son independientes. Puede tener curvas diferentes en cada una, y habilitarlas o deshabilitarlas por separado.

## Función de cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Apagado (desmarcado) | Encendido / Apagado | Habilita o deshabilita el ecualizador para la ruta seleccionada actualmente (RX o TX). Se resalta en verde cuando está habilitado. |
| Reset arc (icono de revertir) | Botón pulsador | — | — | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Información sobre herramientas: "Restablecer todas las bandas a 0 dB". |
| RX | Botón de alternancia | Apagado (desmarcado) | Encendido / Apagado | Selecciona la ruta del ecualizador de recepción para visualización y edición. Se resalta en azul cuando está activo. Mutuamente excluyente con TX. |
| TX | Botón de alternancia | Encendido (marcado) | Encendido / Apagado | Selecciona la ruta del ecualizador de transmisión para visualización y edición. Se resalta en azul cuando está activo. Mutuamente excluyente con RX. |
| 63 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada. Muestra un mensaje emergente con el valor mientras se arrastra el control. |
| 125 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. Muestra un mensaje emergente con el valor mientras se arrastra el control. |
| 250 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. Muestra un mensaje emergente con el valor mientras se arrastra el control. |
| 500 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. Muestra un mensaje emergente con el valor mientras se arrastra el control. |
| 1k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. Muestra un mensaje emergente con el valor mientras se arrastra el control. |
| 2k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. Muestra un mensaje emergente con el valor mientras se arrastra el control. |
| 4k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. Muestra un mensaje emergente con el valor mientras se arrastra el control. |
| 8k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. Muestra un mensaje emergente con el valor mientras se arrastra el control. |
| Etiqueta de valor por banda | Indicador | 0 | −10 a +10 | Muestra el valor actual en dB de cada banda debajo de su control deslizante. Se actualiza en vivo mientras mueve el control. |
| Escala +10 / 0 / −10 dB | Indicador | — | — | Etiquetas de referencia en los bordes izquierdo y derecho del área de controles deslizantes que muestran el rango de estos. |

Ningún valor de las bandas del control deslizante de este applet se conserva en la configuración local de AetherSDR; todos los valores de los controles deslizantes se almacenan y recuperan del radio. La selección de vista RX/TX se almacena localmente para que el applet se reabra en la ruta que usó por última vez.

## Consejos

- Debido a que RX y TX son rutas independientes, puede dejar la ecualización de TX plana mientras da forma solo al audio de RX, o viceversa.
- Use ON para comparar rápidamente el audio ecualizado versus el plano sin mover ningún control deslizante. Actívelo y desactívelo mientras escucha para evaluar su curva.
- El botón Reset arc restablece las ocho bandas a la vez. Si solo desea ajustar una banda, mueva ese control deslizante de vuelta a 0 manualmente.
- El mensaje emergente con el valor aparece cerca del control deslizante mientras lo arrastra. El mensaje permanece brevemente después de soltar el botón del ratón para que pueda leer el valor final.
- El applet recuerda si estaba en RX o TX la última vez que lo usó, incluso después de reiniciar el programa.

## Relacionados

- [Enable radio-side graphic EQ for TX](enable-radio-side-graphic-eq-for-tx.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
