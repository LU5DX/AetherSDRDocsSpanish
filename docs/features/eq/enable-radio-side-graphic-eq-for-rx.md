# Activar el ecualizador gráfico del lado de la radio para RX

Abra el applet Equalizer y active la ruta del ecualizador de RX para que la radio Flex aplique un ecualizador gráfico de 8 bandas al audio recibido dentro de la propia radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El applet EQ requiere una conexión activa con la radio.
- Si el panel del applet no está visible, actívelo mediante `View > Applet Panel`.

## Pasos

1. Haga clic en el botón EQ de la barra lateral derecha para abrir el tile Equalizer.
2. Haga clic en RX. El botón se resalta en azul y los controles deslizantes cambian a la ruta de recepción.
3. Haga clic en ON. El botón se resalta en verde. El ecualizador de RX ya está activo en la radio.
4. Ajuste los controles deslizantes de banda (63, 125, 250, 500, 1k, 2k, 4k, 8k) según sea necesario. Cada deslizador recorta su banda de −10 a +10 dB. La etiqueta de valor debajo de cada deslizador se actualiza en vivo.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Off (sin marcar) | On / Off | Activa o desactiva el ecualizador para la ruta seleccionada actualmente. Resaltado en verde cuando está activado. |
| RX | Botón de alternancia | Off (sin marcar) | — | Selecciona la ruta de recepción para su visualización y edición. Resaltado en azul cuando está activo. Excluyente con TX. |
| TX | Botón de alternancia | On (marcado) | — | Selecciona la ruta de transmisión. El applet se abre en la vista TX de forma predeterminada. |
| Reset arc | Botón pulsador | — | — | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Tooltip: "Reset all bands to 0 dB". |
| 63 | Deslizador vertical | 0 dB | −10 a +10 dB | Recorta la banda de 63 Hz para la ruta seleccionada. |
| 125 | Deslizador vertical | 0 dB | −10 a +10 dB | Recorta la banda de 125 Hz para la ruta seleccionada. |
| 250 | Deslizador vertical | 0 dB | −10 a +10 dB | Recorta la banda de 250 Hz para la ruta seleccionada. |
| 500 | Deslizador vertical | 0 dB | −10 a +10 dB | Recorta la banda de 500 Hz para la ruta seleccionada. |
| 1k | Deslizador vertical | 0 dB | −10 a +10 dB | Recorta la banda de 1 kHz para la ruta seleccionada. |
| 2k | Deslizador vertical | 0 dB | −10 a +10 dB | Recorta la banda de 2 kHz para la ruta seleccionada. |
| 4k | Deslizador vertical | 0 dB | −10 a +10 dB | Recorta la banda de 4 kHz para la ruta seleccionada. |
| 8k | Deslizador vertical | 0 dB | −10 a +10 dB | Recorta la banda de 8 kHz para la ruta seleccionada. |

## Consejos

- El applet siempre se abre mostrando la ruta TX. Haga clic en RX antes de ajustar los deslizadores para asegurarse de que está editando las bandas de recepción, no las de transmisión.
- Para comparar rápidamente el audio de recepción ecualizado y plano, haga clic en ON repetidamente mientras escucha. La radio aplica o elimina el EQ de inmediato.
- Para empezar de nuevo, haga clic en el botón Reset arc. Todas las bandas de RX vuelven a 0 dB con un solo clic.

## Solución de problemas

- **El botón ON no responde** — Confirme que AetherSDR está conectado a la radio. El applet EQ requiere una conexión activa con la radio para enviar cambios.
- **Los cambios en los deslizadores afectan a TX en lugar de RX** — TX es la vista predeterminada. Haga clic primero en RX para cambiar el applet a la ruta de recepción antes de editar las bandas.

## Relacionados

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for TX](enable-radio-side-graphic-eq-for-tx.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
