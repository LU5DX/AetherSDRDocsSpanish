# Descripción general del Ecualizador (Gráfico)

El applet Ecualizador (Gráfico) proporciona un ecualizador gráfico de 8 bandas que se ejecuta dentro del propio radio Flex, aplicado a través de la API TCP/IP del radio. Úselo para dar forma a la respuesta en frecuencia de su audio recibido o de su señal transmitida en ocho bandas de octava fijas, desde 63 Hz hasta 8 kHz.

Este ecualizador es independiente de cualquier EQ paramétrico del lado del cliente en AetherSDR. Los cambios surten efecto en el DSP del radio, no en el software de su computadora.

## Antes de comenzar

- Conecte AetherSDR a un radio Flex. El applet requiere una conexión de radio activa.
- Haga visible el panel del applet. Si está oculto, vaya a `View > Applet Panel` para mostrarlo.

## Cómo funciona

Haga clic en el botón de bandeja EQ en la barra lateral derecha para abrir o cerrar el mosaico del Ecualizador. El mosaico aparece en la fila superior del panel de applets.

El applet siempre muestra una ruta a la vez: ya sea RX o TX. Use los botones RX y TX para cambiar la ruta que está viendo y editando. El applet se abre en la vista TX de forma predeterminada.

Cada una de las ocho bandas tiene un control deslizante vertical. Mover un control deslizante envía el nuevo valor al radio de inmediato; el valor en dB debajo de cada control deslizante se actualiza en tiempo real. Activar o desactivar el ecualizador con ON también surte efecto inmediatamente en la ruta seleccionada actualmente.

Las rutas RX y TX son independientes. Puede tener curvas diferentes en cada una, y activarlas o desactivarlas por separado.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Apagado (sin marcar) | On / Off | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (RX o TX). Se resalta en verde cuando está activado. |
| Arco de reinicio (ícono de reversión) | Botón de acción | — | — | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Información sobre herramienta: "Reset all bands to 0 dB". |
| RX | Botón de alternancia | Apagado (sin marcar) | On / Off | Selecciona la ruta del ecualizador de recepción para visualización y edición. Se resalta en azul cuando está activo. Mutuamente exclusivo con TX. |
| TX | Botón de alternancia | Activado (marcado) | On / Off | Selecciona la ruta del ecualizador de transmisión para visualización y edición. Se resalta en azul cuando está activo. Mutuamente exclusivo con RX. |
| 63 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada. |
| 125 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. |
| 250 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. |
| 500 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. |
| 1k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. |
| 2k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. |
| 4k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. |
| 8k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. |
| Etiqueta de valor por banda | Indicador | 0 | −10 a +10 | Muestra el valor actual en dB de cada banda debajo del control deslizante. Se actualiza en tiempo real al mover el control deslizante. |
| Escala +10 / 0 / −10 dB | Indicador | — | — | Etiquetas de referencia en los bordes izquierdo y derecho del área de controles deslizantes que muestran el rango de los mismos. |

Ninguna configuración de este applet se guarda en la configuración local de AetherSDR. Todos los valores se almacenan en el radio y se recuperan desde él.

## Consejos

- Dado que RX y TX son rutas independientes, puede dejar la ecualización de TX sin cambios mientras da forma solo al audio de RX, o viceversa.
- Use ON para comparar rápidamente el audio ecualizado frente al audio plano sin mover ningún control deslizante. Actívelo y desactívelo mientras escucha para evaluar su curva.
- El botón de arco de reinicio restablece las ocho bandas a la vez. Si solo desea ajustar una banda, mueva manualmente ese control deslizante de regreso a 0.

## Temas relacionados

- [Activar el EQ gráfico del radio para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Activar el EQ gráfico del radio para RX](enable-radio-side-graphic-eq-for-rx.md)
- [Aumentar o reducir bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Restablecer todas las bandas a plano con un solo clic](reset-all-bands-to-flat-with-one-click.md)
- [Cambiar entre dar forma al audio de RX y al audio de TX](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Comparar EQ activado y desactivado rápidamente con el botón ON](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
