# Applet de Ecualizador (Gráfico)

El applet EQ proporciona un ecualizador gráfico de 8 bandas aplicado dentro de la propia radio mediante la API TCP/IP. Cada control deslizante vertical controla una banda de octava desde 63 Hz hasta 8 kHz con un rango de ±10 dB. El applet tiene vistas RX y TX separadas para que pueda moldear el audio de recepción y transmisión de forma independiente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet EQ requiere una conexión activa con la radio.
- El applet EQ debe estar abierto. Si no está visible, haga clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha para mostrarlo.

## Pasos

1. Haga clic en el botón EQ de la bandeja en la barra lateral derecha para abrir el mosaico del ecualizador si aún no está visible.
2. Seleccione la ruta que desea moldear: haga clic en RX para trabajar con el ecualizador de recepción, o haga clic en TX para trabajar con el ecualizador de transmisión. El applet se abre en la vista TX de forma predeterminada.
3. Ajuste cualquier control deslizante de banda (63, 125, 250, 500 Hz o 1k, 2k, 4k, 8k) arrastrando el control hacia arriba o hacia abajo. La etiqueta de valor debajo del control se actualiza en vivo.
4. Al arrastrar un control, aparece una ventana emergente cerca del control mostrando el valor exacto en dB con su signo (por ejemplo, "+3 dB" o "-5 dB").

## Ajuste de bandas mediante atajos de teclado

Puede ajustar los controles deslizantes de banda con pequeños pasos de teclado cuando el applet EQ tenga el foco. Aparece la misma ventana emergente de valor de arrastre para mostrar el nuevo valor, y luego permanece brevemente antes de desvanecerse.

1. Asegúrese de que la ventana del applet EQ tenga el foco del teclado.
2. Use las teclas de flecha Arriba o Abajo para ajustar el control actualmente enfocado en un paso pequeño.
3. La ventana emergente de valor aparece cerca del centro del control, refleja la lectura del arrastre con el mouse y se desvanece con el mismo tiempo de espera.

## Restablecer todas las bandas a planas con un solo clic

La función de restablecimiento configura las ocho bandas del ecualizador para la ruta actualmente seleccionada (RX o TX) de nuevo a 0 dB en una sola acción. Úsela para borrar una curva personalizada y volver a una respuesta plana sin ajustar cada control individualmente.

1. Seleccione la ruta que desea restablecer: haga clic en RX para trabajar con el ecualizador de recepción, o haga clic en TX para trabajar con el ecualizador de transmisión.
2. Haga clic en el botón de arco de restablecimiento (el ícono de flecha de 3/4 de círculo, inmediatamente a la derecha de ON). Su información sobre herramientas dice "Reset all bands to 0 dB."

Los ocho controles deslizantes de banda se mueven a 0 dB y sus etiquetas de valor se actualizan a 0.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Rango |
|---|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada (RX o TX). Se muestra en verde cuando está activado. | sin marcar | — |
| Botón de arco de restablecimiento | Restablece las 8 bandas de la ruta actualmente seleccionada a 0 dB. | — | — |
| RX | Selecciona la ruta de recepción para visualización y edición. Se muestra en azul cuando está activo. | sin marcar | — |
| TX | Selecciona la ruta de transmisión para visualización y edición. Se muestra en azul cuando está activo. | marcado | — |
| 63 | Control deslizante vertical que ajusta la banda de 63 Hz para la ruta seleccionada. La etiqueta de valor debajo del control se actualiza en vivo. | 0 dB | −10 a +10 dB |
| 125 | Control deslizante vertical que ajusta la banda de 125 Hz para la ruta seleccionada. La etiqueta de valor debajo del control se actualiza en vivo. | 0 dB | −10 a +10 dB |
| 250 | Control deslizante vertical que ajusta la banda de 250 Hz para la ruta seleccionada. La etiqueta de valor debajo del control se actualiza en vivo. | 0 dB | −10 a +10 dB |
| 500 | Control deslizante vertical que ajusta la banda de 500 Hz para la ruta seleccionada. La etiqueta de valor debajo del control se actualiza en vivo. | 0 dB | −10 a +10 dB |
| 1k | Control deslizante vertical que ajusta la banda de 1 kHz para la ruta seleccionada. La etiqueta de valor debajo del control se actualiza en vivo. | 0 dB | −10 a +10 dB |
| 2k | Control deslizante vertical que ajusta la banda de 2 kHz para la ruta seleccionada. La etiqueta de valor debajo del control se actualiza en vivo. | 0 dB | −10 a +10 dB |
| 4k | Control deslizante vertical que ajusta la banda de 4 kHz para la ruta seleccionada. La etiqueta de valor debajo del control se actualiza en vivo. | 0 dB | −10 a +10 dB |
| 8k | Control deslizante vertical que ajusta la banda de 8 kHz para la ruta seleccionada. La etiqueta de valor debajo del control se actualiza en vivo. | 0 dB | −10 a +10 dB |
| Escala de +10 / 0 / -10 dB | Etiquetas de referencia a la izquierda y derecha de la columna de controles que indican el rango de los controles. | — | — |

## Consejos

- El applet se abre en la vista TX de forma predeterminada. No hay memoria persistente de su última vista utilizada.
- El restablecimiento actúa solo sobre la ruta mostrada actualmente. Para restablecer ambas rutas, seleccione RX, haga clic en el botón de arco de restablecimiento, luego seleccione TX y haga clic nuevamente.
- Restablecer las bandas no desactiva el ecualizador. ON permanece en su estado actual después de un restablecimiento.
- La ventana emergente de arrastre muestra el valor con signo (por ejemplo, "+3 dB" para valores positivos, "0 dB" para cero, "-5 dB" para valores negativos). Esto coincide con el comportamiento de otros controles en la aplicación.
- Después de soltar un control o presionar una tecla de flecha, la ventana emergente permanece brevemente antes de desaparecer para que pueda leer el valor final.
- Los ajustes por teclado para los controles del ecualizador se enrutan mediante una concesión de atajos, de modo que los atajos operativos globales puedan reanudarse después de cada ajuste.
- El applet usa los colores del tema para todos los elementos de la interfaz. Los colores se actualizan en vivo cuando cambia el tema de la aplicación.
- La ventana emergente de valor de arrastre la proporciona una clase base compartida (`GuardedSlider`). Cualquier subclase de control que personalice el manejo del mouse para funciones como el posicionamiento por clic para saltar debe escribirse para conservar este comportamiento de la ventana emergente. Los métodos relevantes son `protected` (no `private`) para permitir la anulación segura por subclase sin perder la ventana emergente.

## Relacionado

- [Descripción general del ecualizador (gráfico)](overview.md)
- [Aumentar o cortar bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Cambiar entre moldear audio RX y audio TX](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Comparar EQ activado versus EQ desactivado rápidamente con el botón ON](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
