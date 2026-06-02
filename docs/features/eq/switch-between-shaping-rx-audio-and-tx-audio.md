# Cambiar entre la ecualización de audio de RX y TX

El applet Equalizer mantiene configuraciones de bandas separadas para las rutas de recepción y transmisión. Use los botones selectores RX y TX para elegir en qué ruta actúan los deslizadores y el botón ON. El applet recuerda qué vista (RX o TX) usó por última vez y se reabre en esa vista al reiniciar AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet EQ requiere una conexión activa con la radio.
- Abra el mosaico Equalizer haciendo clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha.

## Pasos

1. Haga clic en el botón EQ de la bandeja en la barra lateral derecha para abrir el mosaico Equalizer si aún no está visible.
2. Para editar la ruta de recepción, haga clic en RX. Los deslizadores y el botón ON ahora reflejan y controlan las bandas del ecualizador de RX.
3. Para editar la ruta de transmisión, haga clic en TX. Los deslizadores y el botón ON ahora reflejan y controlan las bandas del ecualizador de TX.
4. La próxima vez que abra el mosaico Equalizer, mostrará la misma vista (RX o TX) que seleccionó por última vez.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| RX | Botón de alternancia | Sin marcar en el primer inicio; luego recuerda la última selección | — | Selecciona la ruta del ecualizador de recepción para visualización y edición. Resaltado en azul cuando está activo. |
| TX | Botón de alternancia | Marcado en el primer inicio; luego recuerda la última selección | — | Selecciona la ruta del ecualizador de transmisión para visualización y edición. Resaltado en azul cuando está activo. El applet se abre en la vista TX en el primer inicio. |
| ON | Botón de alternancia | Sin marcar | — | Activa o desactiva el ecualizador para la ruta (RX o TX) actualmente seleccionada. Resaltado en verde cuando está activado. |
| 63 | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada; la etiqueta de valor debajo del deslizador se actualiza en vivo. Al arrastrar, aparece una ventana emergente con el valor dB con signo. |
| 125 | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente con el valor dB con signo. |
| 250 | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente con el valor dB con signo. |
| 500 | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente con el valor dB con signo. |
| 1k | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente con el valor dB con signo. |
| 2k | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente con el valor dB con signo. |
| 4k | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente con el valor dB con signo. |
| 8k | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente con el valor dB con signo. |
| Arco de reinicio (icono de revertir) | Botón pulsador | — | — | Restablece las 8 bandas de la ruta actualmente seleccionada a 0 dB. |
| Escala +10 / 0 / −10 dB | Indicador | — | — | Etiquetas de referencia izquierda y derecha que muestran el rango de ±10 dB de los deslizadores. |

## Consejos

- RX y TX son mutuamente excluyentes. Al hacer clic en uno, se deselecciona automáticamente el otro. No puede editar ambas rutas al mismo tiempo.
- El botón ON, todos los deslizadores y el botón de reinicio siempre operan en la ruta actualmente seleccionada. Cambie a RX antes de reiniciar o ajustar si desea modificar la ruta de recepción.
- Cuando cambie de TX a RX (o viceversa), los deslizadores se actualizan inmediatamente para mostrar los valores almacenados de la ruta recién seleccionada. Los cambios realizados en la ruta anterior no se pierden.
- La última vista seleccionada (RX o TX) se guarda en la configuración de la aplicación (`EqApplet.showTx`). Esto persiste al reiniciar AetherSDR. En el primer inicio, el applet se abre de forma predeterminada en la vista TX.
- Mientras arrastra cualquier deslizador de banda, aparece una pequeña ventana emergente cerca del control mostrando el valor dB con signo actual (por ejemplo, "+3 dB" o "-5 dB"). La ventana permanece brevemente después de soltar el botón del ratón.
- El applet Equalizer admite el cambio de tema en vivo. Los controles y etiquetas de los deslizadores actualizan automáticamente sus colores al cambiar el tema activo. La ranura del deslizador no cambia de color, lo que garantiza que el control siga siendo el único elemento de color de acento en la columna de bandas.

## Relacionados

- [Descripción general del ecualizador gráfico](overview.md)
- [Habilitar el ecualizador gráfico del lado de la radio para RX](enable-radio-side-graphic-eq-for-rx.md)
- [Habilitar el ecualizador gráfico del lado de la radio para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Aumentar o atenuar bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Restablecer todas las bandas a planas con un solo clic](reset-all-bands-to-flat-with-one-click.md)
