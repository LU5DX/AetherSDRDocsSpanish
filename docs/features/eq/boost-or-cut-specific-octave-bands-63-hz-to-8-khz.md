# Aumentar o reducir bandas de octava específicas (63 Hz a 8 kHz)

Use el applet Equalizer para subir o bajar bandas de frecuencia individuales en la ruta de audio de recepción o transmisión del radio. Cada una de las ocho bandas puede ajustarse entre −10 dB y +10 dB.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Equalizer requiere una conexión activa con el radio.
- Decida si va a dar forma a la ruta RX o TX antes de mover los controles deslizantes.

## Pasos

1. Haga clic en el botón EQ del panel de applets en la barra lateral derecha para abrir el panel Equalizer.
2. Haga clic en TX para editar la ruta de transmisión, o haga clic en RX para editar la ruta de recepción. TX está seleccionado por defecto al abrir el applet.
3. Haga clic en ON para activar el ecualizador en la ruta seleccionada. ON se ilumina en verde cuando está activo.
4. Arrastre el control deslizante de la banda que desea ajustar. Las bandas están etiquetadas como **63**, **125**, **250**, **500**, **1k**, **2k**, **4k** y **8k** (Hz y kHz respectivamente). Arrastre hacia arriba para aumentar y hacia abajo para reducir.
5. Lea la etiqueta de valor directamente debajo de cada control deslizante para confirmar la cantidad en dB. La etiqueta se actualiza en tiempo real mientras arrastra.
6. Repita los pasos 4–5 para cualquier otra banda que desee ajustar.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Desactivado (sin marcar) | Activado / Desactivado | Activa o desactiva el ecualizador para la ruta actualmente seleccionada. Se ilumina en verde cuando está activado. |
| RX | Botón de alternancia | Sin marcar | — | Cambia el applet para mostrar y editar las bandas del ecualizador de recepción. Se ilumina en azul cuando está activo. |
| TX | Botón de alternancia | Marcado | — | Cambia el applet para mostrar y editar las bandas del ecualizador de transmisión. Se ilumina en azul cuando está activo. |
| Botón Reset arc | Botón de acción | — | — | Restablece las 8 bandas de la ruta actualmente seleccionada a 0 dB. Información emergente: "Reset all bands to 0 dB". |
| 63 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada. |
| 125 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. |
| 250 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. |
| 500 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. |
| 1k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. |
| 2k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. |
| 4k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. |
| 8k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. |
| Etiqueta de valor por banda | Indicador | 0 | −10 a +10 | Muestra el valor en dB en tiempo real del control deslizante directamente encima de ella. |

## Consejos

- Los ajustes de RX y TX son independientes. Ajustar bandas mientras TX está seleccionado no tiene ningún efecto en la curva de RX, y viceversa.
- Las etiquetas de escala +10 / 0 / −10 dB en los bordes izquierdo y derecho de la columna de controles deslizantes ofrecen una referencia visual para el punto medio (0 dB) y los límites.
- Para devolver rápidamente todas las bandas a plano sin mover cada control deslizante individualmente, haga clic en el botón Reset arc.

## Solución de problemas

- **Los controles deslizantes se mueven pero el audio no se ve afectado** — Verifique que ON esté iluminado en verde para la ruta activa. El ecualizador no tiene efecto cuando ON está sin marcar, aunque los controles deslizantes estén en valores distintos de cero.
- **Ajustar los controles deslizantes en la ruta TX cambia lo que escucha en RX** — Es posible que esté en la ruta incorrecta. Haga clic en RX para confirmar que está editando las bandas de recepción, o haga clic en TX para las de transmisión. Las dos rutas son independientes; solo se edita la ruta que se muestra en ese momento.

## Relacionados

- [Descripción general de Equalizer (Graphic)](overview.md)
- [Activar el EQ gráfico del lado del radio para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Activar el EQ gráfico del lado del radio para RX](enable-radio-side-graphic-eq-for-rx.md)
- [Restablecer todas las bandas a plano con un solo clic](reset-all-bands-to-flat-with-one-click.md)
- [Cambiar entre dar forma al audio de RX y al audio de TX](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Comparar EQ activado y EQ desactivado rápidamente con el botón ON](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
