# Resumen del ecualizador (gráfico)

El applet Ecualizador (Gráfico) proporciona un ecualizador gráfico de 8 bandas que se ejecuta dentro del propio radio Flex, aplicado a través de la API TCP/IP del radio. Úselo para dar forma a la respuesta de frecuencia del audio recibido o de la señal transmitida en ocho bandas de octava fijas de 63 Hz a 8 kHz.

Este ecualizador es independiente de cualquier ecualizador paramétrico del lado del cliente en AetherSDR. Los cambios surten efecto en el DSP del radio, no en el software de su computadora.

## Antes de comenzar

- Conecte AetherSDR a un radio Flex. El applet requiere una conexión activa al radio.
- Haga visible el panel de applets. Si está oculto, vaya a `View > Applet Panel` para mostrarlo.

## Cómo funciona

Haga clic en el botón de la bandeja EQ en la barra lateral derecha para abrir o cerrar el mosaico del Ecualizador. El mosaico aparece en la fila superior del panel de applets.

El applet siempre muestra una ruta a la vez — ya sea RX o TX. Use los botones RX y TX para cambiar qué ruta está viendo y editando. El applet se abre en la vista TX de forma predeterminada. AetherSDR recuerda la última vista seleccionada (RX o TX) entre sesiones; si cierra el applet mientras ve el ecualizador de RX, se abrirá en RX la próxima vez que inicie el programa.

Cada una de las ocho bandas tiene un deslizador vertical. Al mover un deslizador, el nuevo valor se envía al radio de inmediato; el valor en dB debajo de cada deslizador se actualiza en vivo. Activar o desactivar el ecualizador con ON también surte efecto inmediatamente en la ruta seleccionada actualmente.

Las rutas RX y TX son independientes. Puede tener curvas diferentes en cada una y activarlas o desactivarlas por separado.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Apagado (sin marcar) | On / Off | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (RX o TX). Se resalta en verde cuando está activado. |
| Botón de reinicio (icono de flecha circular) | Botón pulsador | — | — | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Información sobre herramientas: "Restablecer todas las bandas a 0 dB". |
| RX | Botón de alternancia | Apagado (sin marcar) | On / Off | Selecciona la ruta del ecualizador de recepción para visualización y edición. Se resalta en azul cuando está activo. Excluyente con TX. |
| TX | Botón de alternancia | Encendido (marcado) | On / Off | Selecciona la ruta del ecualizador de transmisión para visualización y edición. Se resalta en azul cuando está activo. Excluyente con RX. |
| 63 | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada. |
| 125 | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. |
| 250 | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. |
| 500 | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. |
| 1k | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. |
| 2k | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. |
| 4k | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. |
| 8k | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. |
| Etiqueta de valor por banda | Indicador | 0 | −10 a +10 | Muestra el valor actual en dB de cada banda debajo de su control deslizante. Se actualiza en vivo al mover el deslizador. |
| Escala +10 / 0 / −10 dB | Indicador | — | — | Etiquetas de referencia en los bordes izquierdo y derecho del área de deslizadores que muestran el rango del deslizador. |

Ningún valor de banda de este applet se conserva en la configuración local de AetherSDR; todos los valores de los deslizadores se almacenan y recuperan del radio. La selección de la vista RX/TX se almacena localmente para que el applet se vuelva a abrir en la ruta que usó por última vez.

## Consejos

- Debido a que las rutas RX y TX son independientes, puede dejar la ecualización de TX plana mientras da forma solo al audio de RX, o viceversa.
- Use ON para comparar rápidamente el audio ecualizado versus el audio plano sin mover ningún deslizador. Actívelo y desactívelo mientras escucha para evaluar su curva.
- El botón de reinicio restablece las ocho bandas a la vez. Si solo desea ajustar una banda, mueva ese deslizador de vuelta a 0 manualmente.
- El applet recuerda si estaba en RX o TX la última vez que lo usó, incluso después de reiniciar el programa.

## Relacionado

- [Enable radio-side graphic EQ for TX](enable-radio-side-graphic-eq-for-tx.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
