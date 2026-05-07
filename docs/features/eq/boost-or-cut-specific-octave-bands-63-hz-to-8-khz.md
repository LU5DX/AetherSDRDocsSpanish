# Aumentar o reducir bandas de octava específicas (63 Hz a 8 kHz)

Utilice el applet Equalizer para aumentar o reducir bandas de frecuencia individuales en la ruta de audio de recepción o transmisión del equipo. Cada una de las ocho bandas puede ajustarse en cualquier valor entre −10 dB y +10 dB.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El applet Equalizer requiere una conexión de radio activa.
- Decida si va a moldear la ruta de RX o TX antes de mover los deslizadores.

## Pasos

1. Haga clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha para abrir el panel Equalizer.
2. Haga clic en TX para editar la ruta de transmisión, o en RX para editar la ruta de recepción. TX está seleccionado de forma predeterminada cuando se abre el applet.
3. Haga clic en ON para activar el ecualizador en la ruta seleccionada. ON se resalta en verde cuando está activo.
4. Arrastre el deslizador de la banda que desea ajustar. Las bandas están etiquetadas como **63**, **125**, **250**, **500**, **1k**, **2k**, **4k** y **8k** (Hz y kHz respectivamente). Arrastre hacia arriba para aumentar, arrastre hacia abajo para reducir.
5. Lea la etiqueta de valor directamente debajo de cada manija del deslizador para confirmar la cantidad en dB. La etiqueta se actualiza en vivo mientras arrastra.
6. Repita los pasos 4–5 para cualquier otra banda que desee ajustar.

## Función de cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Off (desmarcado) | On / Off | Activa o desactiva el ecualizador para la ruta seleccionada actualmente. Se resalta en verde cuando está activado. |
| RX | Botón de alternancia | Desmarcado | — | Cambia el applet para mostrar y editar las bandas del ecualizador de recepción. Se resalta en azul cuando está activo. |
| TX | Botón de alternancia | Marcado | — | Cambia el applet para mostrar y editar las bandas del ecualizador de transmisión. Se resalta en azul cuando está activo. |
| Reset arc | Botón pulsador | — | — | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Información sobre herramientas: "Reset all bands to 0 dB". |
| 63 | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada. |
| 125 | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. |
| 250 | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. |
| 500 | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. |
| 1k | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. |
| 2k | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. |
| 4k | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. |
| 8k | Deslizador vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. |
| Etiqueta de valor por banda | Indicador | 0 | −10 a +10 | Muestra el valor en dB en vivo del deslizador situado directamente encima. |

## Consejos

- Los ajustes de RX y TX son independientes. Ajustar bandas mientras TX está seleccionado no tiene efecto en la curva de RX, y viceversa.
- Las etiquetas de escala +10 / 0 / −10 dB en los bordes izquierdo y derecho de la columna de deslizadores proporcionan una referencia visual para el punto medio (0 dB) y los límites del deslizador.
- Para devolver rápidamente todas las bandas a plano sin mover cada deslizador individualmente, haga clic en el botón Reset arc.

## Solución de problemas

- **Los deslizadores se mueven pero el audio no se ve afectado** — Verifique que ON esté resaltado en verde para la ruta activa. El ecualizador no tiene ningún efecto cuando ON está desmarcado, incluso si los deslizadores están configurados en valores distintos de cero.
- **Ajustar los deslizadores en la ruta TX cambia lo que escucha en RX** — Es posible que esté en la ruta incorrecta. Haga clic en RX para confirmar que está editando las bandas de recepción, o en TX para transmisión. Las dos rutas son independientes; solo se está editando la ruta mostrada actualmente.

## Relacionados

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for TX](enable-radio-side-graphic-eq-for-tx.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
