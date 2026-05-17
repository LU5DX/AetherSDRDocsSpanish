# Restablecer todas las bandas a planas con un solo clic

La función de restablecimiento ajusta las ocho bandas del ecualizador para la ruta seleccionada actualmente (RX o TX) a 0 dB en una sola acción. Úsela para borrar una curva personalizada y volver a una respuesta plana sin ajustar cada control deslizante individualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet EQ requiere una conexión activa con la radio.
- El applet EQ debe estar abierto. Si no está visible, haga clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha para mostrarlo.

## Pasos

1. Haga clic en el botón EQ de la bandeja en la barra lateral derecha para abrir el mosaico Equalizer si aún no está visible.
2. Seleccione la ruta que desea restablecer: haga clic en RX para trabajar en el ecualizador de recepción, o haga clic en TX para trabajar en el ecualizador de transmisión. El applet se abre en la última ruta utilizada; la primera vez que lo abre, se selecciona la vista TX.
3. Haga clic en el botón de arco de restablecimiento (el icono de flecha circular de 3/4, inmediatamente a la derecha de ON). Su información sobre herramientas dice "Reset all bands to 0 dB."

Los ocho controles deslizantes de banda (63, 125, 250, 500 Hz y 1k, 2k, 4k, 8k) se mueven a 0 dB y sus etiquetas de valor se actualizan a 0.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Rango |
|---|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada (RX o TX). Se muestra en verde cuando está activado. | sin marcar | — |
| RX | Selecciona la ruta de recepción para visualización y edición. Se muestra en azul cuando está activa. | sin marcar | — |
| TX | Selecciona la ruta de transmisión para visualización y edición. Se muestra en azul cuando está activa. | marcado en el primer inicio; luego recuerda la última selección | — |
| Botón de arco de restablecimiento | Restablece las 8 bandas de la ruta actualmente seleccionada a 0 dB. | — | — |
| Controles deslizantes de banda (63–8k) | Controles deslizantes de orientación vertical; cada uno ajusta una banda de octava para la ruta seleccionada. La etiqueta de valor debajo de cada control deslizante se actualiza en vivo. | 0 dB | −10 a +10 dB |

## Consejos

- El applet recuerda qué vista (RX o TX) usó por última vez entre sesiones. La primera vez que abre el applet después de la instalación, se establece por defecto en TX.
- El restablecimiento actúa solo en la ruta actualmente mostrada. Para restablecer ambas rutas, seleccione RX, haga clic en el botón de arco de restablecimiento, luego seleccione TX y haga clic nuevamente.
- Restablecer las bandas no desactiva el ecualizador. ON permanece en su estado actual después de un restablecimiento.
- Una etiqueta de escala "+10 / 0 / -10 dB" aparece a la izquierda y derecha de la columna de controles deslizantes para indicar el rango.

## Relacionados

- [Equalizer (Graphic) overview](overview.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
