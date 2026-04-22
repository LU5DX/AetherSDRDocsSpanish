# Restablecer todas las bandas a plano con un solo clic

La función de restablecimiento lleva las ocho bandas del ecualizador correspondientes a la ruta seleccionada (RX o TX) a 0 dB en una sola acción. Úsela para borrar una curva personalizada y volver a una respuesta plana sin ajustar cada control deslizante individualmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet de EQ requiere una conexión activa con el radio.
- El applet de EQ debe estar abierto. Si no está visible, haga clic en el botón de bandeja EQ del panel de applets de la barra lateral derecha para mostrarlo.

## Pasos

1. Haga clic en el botón de bandeja EQ de la barra lateral derecha para abrir el panel del Ecualizador si aún no está visible.
2. Seleccione la ruta que desea restablecer: haga clic en RX para trabajar con el ecualizador de recepción, o haga clic en TX para trabajar con el ecualizador de transmisión. El applet se abre en la vista TX de forma predeterminada.
3. Haga clic en el botón de arco de restablecimiento (el ícono de flecha en 3/4 de círculo, inmediatamente a la derecha de ON). Su información emergente indica "Reset all bands to 0 dB."

Los ocho controles deslizantes de banda (63, 125, 250, 500 Hz y 1k, 2k, 4k, 8k) se mueven a 0 dB y sus etiquetas de valor se actualizan a 0.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Rango |
|---|---|---|---|
| RX | Selecciona la ruta de recepción para visualización y edición. | sin marcar | — |
| TX | Selecciona la ruta de transmisión para visualización y edición. | marcado | — |
| Botón de arco de restablecimiento | Restablece las 8 bandas de la ruta seleccionada a 0 dB. | — | — |
| Controles deslizantes de banda (63–8k) | Ajuste individual por banda; todos vuelven a 0 tras un restablecimiento. | 0 dB | −10 a +10 dB |

## Consejos

- El restablecimiento actúa únicamente sobre la ruta que se muestra en ese momento. Para restablecer ambas rutas, seleccione RX, haga clic en el botón de arco de restablecimiento, luego seleccione TX y vuelva a hacer clic.
- Restablecer las bandas no desactiva el ecualizador. ON permanece en su estado actual después del restablecimiento.

## Relacionados

- [Descripción general del Ecualizador (Gráfico)](overview.md)
- [Aumentar o reducir bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Cambiar entre ajustar el audio de RX y el audio de TX](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Comparar EQ activado y EQ desactivado rápidamente con el botón ON](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
