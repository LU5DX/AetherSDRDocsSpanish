# Applet de ecualizador (gráfico)

El applet EQ proporciona un ecualizador gráfico de 8 bandas aplicado dentro de la propia radio a través de la API TCP/IP. Cada deslizador vertical controla una banda de octava de 63 Hz a 8 kHz con un rango de ±10 dB. El applet tiene vistas separadas de RX y TX para que pueda dar forma al audio de recepción y transmisión de forma independiente.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El applet EQ requiere una conexión activa con la radio.
- El applet EQ debe estar abierto. Si no está visible, haga clic en el botón de la bandeja EQ en el panel de applets de la barra lateral derecha para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja EQ en la barra lateral derecha para abrir el mosaico Equalizer si aún no está visible.
2. Seleccione la ruta que desea modificar: haga clic en RX para trabajar en el ecualizador de recepción, o haga clic en TX para trabajar en el ecualizador de transmisión. El applet se abre en la última ruta utilizada; la primera vez que lo abre, se selecciona la vista TX.
3. Ajuste cualquier deslizador de banda (63, 125, 250, 500 Hz o 1k, 2k, 4k, 8k) arrastrando el control hacia arriba o hacia abajo. La etiqueta de valor debajo del deslizador se actualiza en vivo.
4. Al arrastrar un deslizador, aparece un menú emergente cerca del control que muestra el valor exacto en dB con un signo (por ejemplo, "+3 dB" o "-5 dB").

## Restablecer todas las bandas a planas con un solo clic

La función de restablecimiento configura las ocho bandas del ecualizador para la ruta seleccionada actualmente (RX o TX) de vuelta a 0 dB en una sola acción. Úsela para borrar una curva personalizada y volver a una respuesta plana sin ajustar cada deslizador individualmente.

1. Seleccione la ruta que desea restablecer: haga clic en RX para trabajar en el ecualizador de recepción, o haga clic en TX para trabajar en el ecualizador de transmisión.
2. Haga clic en el botón de arco de restablecimiento (el icono de flecha de 3/4 de círculo, inmediatamente a la derecha de ON). Su información sobre herramientas dice "Reset all bands to 0 dB."

Los ocho deslizadores de banda se mueven a 0 dB y sus etiquetas de valor se actualizan a 0.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Rango |
|---|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada (RX o TX). Se muestra en verde cuando está activado. | desmarcado | — |
| RX | Selecciona la ruta de recepción para visualización y edición. Se muestra en azul cuando está activo. | desmarcado | — |
| TX | Selecciona la ruta de transmisión para visualización y edición. Se muestra en azul cuando está activo. | marcado en el primer inicio; luego recuerda la última selección | — |
| Botón de arco de restablecimiento | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. | — | — |
| Deslizadores de banda (63–8k) | Deslizadores de orientación vertical; cada uno ajusta una banda de octava para la ruta seleccionada. La etiqueta de valor debajo de cada deslizador se actualiza en vivo. Al arrastrar un deslizador, un menú emergente cerca del control muestra el valor exacto en dB con un signo (por ejemplo, "+3 dB" o "-5 dB"). El control del deslizador tiene el color del acento del tema. | 0 dB | −10 a +10 dB |
| Escala +10 / 0 / -10 dB | Etiquetas de referencia a la izquierda y derecha de la columna de deslizadores que indican el rango de los deslizadores. | — | — |

## Consejos

- El applet recuerda qué vista (RX o TX) usó por última vez entre sesiones. La primera vez que abre el applet después de la instalación, se establece de forma predeterminada en TX.
- El restablecimiento actúa solo en la ruta mostrada actualmente. Para restablecer ambas rutas, seleccione RX, haga clic en el botón de arco de restablecimiento, luego seleccione TX y haga clic nuevamente.
- Restablecer las bandas no desactiva el ecualizador. ON permanece en su estado actual después de un restablecimiento.
- El menú emergente de arrastre muestra el valor con un signo (por ejemplo, "+3 dB" para valores positivos, "0 dB" para cero, "-5 dB" para valores negativos). Esto coincide con el comportamiento de otros deslizadores en la aplicación.
- Después de soltar un control de deslizador, el menú emergente permanece brevemente antes de desaparecer para que pueda leer el valor final.
- El applet utiliza los colores del tema para todos los elementos de la interfaz de usuario. Los colores se actualizan en vivo cuando cambia el tema de la aplicación.

## Relacionados

- [Equalizer (Graphic) overview](overview.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
