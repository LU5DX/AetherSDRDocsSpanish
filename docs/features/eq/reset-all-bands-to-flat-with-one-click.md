# Applet de Ecualizador (Gráfico)

El applet de EQ proporciona un ecualizador gráfico de 8 bandas aplicado dentro de la propia radio a través de la API TCP/IP. Cada control deslizante vertical controla una banda de octava desde 63 Hz hasta 8 kHz con un rango de ±10 dB. El applet tiene vistas separadas de RX y TX para que pueda moldear el audio de recepción y transmisión de forma independiente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de EQ requiere una conexión activa con la radio.
- El applet de EQ debe estar abierto. Si no está visible, haga clic en el botón de la bandeja EQ en el panel de applets de la barra lateral derecha para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja EQ en la barra lateral derecha para abrir el mosaico Equalizer si aún no está visible.
2. Seleccione la ruta que desea moldear: haga clic en RX para trabajar en el ecualizador de recepción, o haga clic en TX para trabajar en el ecualizador de transmisión. El applet se abre en la última ruta utilizada; la primera vez que lo abre, se selecciona la vista TX.
3. Ajuste cualquier control deslizante de banda (63, 125, 250, 500 Hz o 1k, 2k, 4k, 8k) arrastrando el control hacia arriba o hacia abajo. La etiqueta de valor debajo del control deslizante se actualiza en vivo.
4. Al arrastrar un control deslizante, aparece una ventana emergente cerca del control que muestra el valor exacto en dB con un signo (por ejemplo, "+3 dB" o "-5 dB").

## Ajustar bandas mediante atajos de teclado

Puede ajustar los controles deslizantes de banda con pequeños pasos de teclado cuando el applet de EQ tiene el foco. Aparece la misma ventana emergente de valor de arrastre para mostrar el nuevo valor, luego permanece brevemente antes de desvanecerse.

1. Asegúrese de que la ventana del applet de EQ tenga el foco del teclado.
2. Use las teclas de Flecha Arriba o Flecha Abajo para ajustar el control deslizante enfocado actualmente en un pequeño paso.
3. La ventana emergente de valor aparece cerca del centro del control deslizante, refleja la lectura del arrastre con el ratón y se desvanece con el mismo tiempo de espera.

## Restablecer todas las bandas a planas con un solo clic

La función de restablecimiento establece las ocho bandas del ecualizador para la ruta seleccionada actualmente (RX o TX) de vuelta a 0 dB en una sola acción. Úsela para borrar una curva personalizada y volver a una respuesta plana sin ajustar cada control deslizante individualmente.

1. Seleccione la ruta que desea restablecer: haga clic en RX para trabajar en el ecualizador de recepción, o haga clic en TX para trabajar en el ecualizador de transmisión.
2. Haga clic en el botón de arco de restablecimiento (el icono de flecha de 3/4 de círculo, inmediatamente a la derecha de ON). Su información sobre herramientas dice "Reset all bands to 0 dB."

Los ocho controles deslizantes de banda se mueven a 0 dB y sus etiquetas de valor se actualizan a 0.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Rango |
|---|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada (RX o TX). Se muestra en verde cuando está activado. | desmarcado | — |
| RX | Selecciona la ruta de recepción para visualización y edición. Se muestra en azul cuando está activa. | desmarcado | — |
| TX | Selecciona la ruta de transmisión para visualización y edición. Se muestra en azul cuando está activa. | marcado en el primer inicio; luego recuerda la última selección | — |
| Botón de arco de restablecimiento | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. | — | — |
| Controles deslizantes de banda (63–8k) | Controles deslizantes de orientación vertical; cada uno recorta una banda de octava para la ruta seleccionada. La etiqueta de valor debajo de cada control deslizante se actualiza en vivo. Al arrastrar un control deslizante o usar las teclas de flecha del teclado para ajustar, una ventana emergente cerca del control muestra el valor exacto en dB con un signo (por ejemplo, "+3 dB" o "-5 dB"). El control deslizante tiene el color de acento del tema. | 0 dB | −10 a +10 dB |
| Escala de +10 / 0 / -10 dB | Etiquetas de referencia a la izquierda y derecha de la columna de controles deslizantes que indican el rango de los controles. | — | — |

## Consejos

- El applet recuerda qué vista (RX o TX) utilizó por última vez entre sesiones. La primera vez que abre el applet después de la instalación, se establece por defecto en TX.
- El restablecimiento actúa solo sobre la ruta mostrada actualmente. Para restablecer ambas rutas, seleccione RX, haga clic en el botón de arco de restablecimiento, luego seleccione TX y haga clic de nuevo.
- Restablecer las bandas no desactiva el ecualizador. ON permanece en su estado actual después de un restablecimiento.
- La ventana emergente de arrastre muestra el valor con un signo (por ejemplo, "+3 dB" para valores positivos, "0 dB" para cero, "-5 dB" para valores negativos). Esto coincide con el comportamiento de otros controles deslizantes en la aplicación.
- Después de soltar un control deslizante o presionar una tecla de flecha del teclado, la ventana emergente permanece brevemente antes de desaparecer para que pueda leer el valor final.
- Los ajustes con teclado para los controles deslizantes de EQ se enrutan a través de una concesión de atajos para que los atajos operativos globales puedan reanudarse después de cada ajuste.
- El applet utiliza los colores del tema para todos los elementos de la interfaz. Los colores se actualizan en vivo cuando cambia el tema de la aplicación.

## Relacionado

- [Equalizer (Graphic) overview](overview.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
