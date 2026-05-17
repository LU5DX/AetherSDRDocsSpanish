# Cambiar entre ecualización de audio de RX y audio de TX

El applet del Ecualizador mantiene configuraciones de bandas separadas para las rutas de recepción y transmisión. Use los botones selectores RX y TX para elegir sobre qué ruta actúan los deslizadores y el botón ON. El applet recuerda la vista (RX o TX) que usó por última vez y se abre en esa vista al reiniciar AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet EQ requiere una conexión activa con la radio.
- Abra el mosaico del Ecualizador haciendo clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha.

## Pasos

1. Haga clic en el botón EQ de la bandeja en la barra lateral derecha para abrir el mosaico del Ecualizador si aún no está visible.
2. Para editar la ruta de recepción, haga clic en RX. Los deslizadores y el botón ON ahora reflejan y controlan las bandas del ecualizador de RX.
3. Para editar la ruta de transmisión, haga clic en TX. Los deslizadores y el botón ON ahora reflejan y controlan las bandas del ecualizador de TX.
4. La próxima vez que abra el mosaico del Ecualizador, se mostrará la misma vista (RX o TX) que seleccionó por última vez.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| RX | Botón de alternancia | Sin marcar al iniciar; luego recuerda la última selección | — | Selecciona la ruta del ecualizador de recepción para su visualización y edición. Resaltado en azul cuando está activo. |
| TX | Botón de alternancia | Marcado al iniciar; luego recuerda la última selección | — | Selecciona la ruta del ecualizador de transmisión para su visualización y edición. Resaltado en azul cuando está activo. El applet se abre en la vista TX al iniciar por primera vez. |
| ON | Botón de alternancia | Sin marcar | — | Activa o desactiva el ecualizador para la ruta (RX o TX) actualmente seleccionada. Resaltado en verde cuando está activado. |
| 63 | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada; la etiqueta de valor debajo del deslizador se actualiza en vivo. |
| 125 | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. |
| 250 | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. |
| 500 | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. |
| 1k | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. |
| 2k | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. |
| 4k | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. |
| 8k | Deslizador | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. |
| Arco de restablecimiento (icono de revertir) | Botón pulsador | — | — | Restablece todas las 8 bandas de la ruta actualmente seleccionada a 0 dB. |
| Escala +10 / 0 / −10 dB | Indicador | — | — | Etiquetas de referencia izquierda y derecha que muestran el rango de ±10 dB de los deslizadores. |

## Consejos

- RX y TX son mutuamente excluyentes. Al hacer clic en uno, se deselecciona automáticamente el otro. No puede editar ambas rutas al mismo tiempo.
- El botón ON, todos los deslizadores y el botón de restablecimiento siempre operan sobre la ruta actualmente seleccionada. Cambie a RX antes de restablecer o ajustar si tiene la intención de modificar la ruta de recepción.
- Cuando cambia de TX a RX (o viceversa), los deslizadores se actualizan inmediatamente para mostrar los valores almacenados de la ruta recién seleccionada. Sus cambios en la ruta anterior no se pierden.
- La última vista seleccionada (RX o TX) se guarda en la configuración de la aplicación (`EqApplet.showTx`). Esto persiste al reiniciar AetherSDR. Al iniciar por primera vez, el applet se abre por defecto en la vista TX.

## Relacionados

- [Descripción general del Ecualizador (Gráfico)](overview.md)
- [Activar ecualizador gráfico del lado de la radio para RX](enable-radio-side-graphic-eq-for-rx.md)
- [Activar ecualizador gráfico del lado de la radio para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Aumentar o atenuar bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Restablecer todas las bandas a planas con un solo clic](reset-all-bands-to-flat-with-one-click.md)
