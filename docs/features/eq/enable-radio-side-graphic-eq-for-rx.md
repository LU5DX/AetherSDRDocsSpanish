# Habilitar el ecualizador gráfico en el radio para RX

Abra el applet Equalizer y active la ruta del ecualizador RX para que el radio Flex aplique un ecualizador gráfico de 8 bandas al audio recibido dentro del propio radio.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio Flex. El applet de EQ requiere una conexión activa con el radio.
- Si el panel de applets no está visible, habilítelo mediante `View > Applet Panel`.

## Pasos

1. Haga clic en el botón EQ del panel lateral derecho para abrir el tile Equalizer.
2. Haga clic en RX. El botón se ilumina en azul y los controles deslizantes cambian a la ruta de recepción.
3. Haga clic en ON. El botón se ilumina en verde. El ecualizador RX está ahora activo en el radio.
4. Ajuste los controles deslizantes de banda (63, 125, 250, 500, 1k, 2k, 4k, 8k) según sea necesario. Cada control deslizante ajusta su banda entre −10 y +10 dB. La etiqueta de valor debajo de cada control se actualiza en tiempo real.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| ON | Botón de alternancia | Off (desactivado) | On / Off | Habilita o deshabilita el ecualizador para la ruta seleccionada. Resaltado en verde cuando está habilitado. |
| RX | Botón de alternancia | Off (desactivado) | — | Selecciona la ruta de recepción para visualización y edición. Resaltado en azul cuando está activo. Mutuamente excluyente con TX. |
| TX | Botón de alternancia | On (activado) | — | Selecciona la ruta de transmisión. El applet se abre en la vista TX de manera predeterminada. |
| Reset arc | Botón de acción | — | — | Restablece las 8 bandas de la ruta seleccionada a 0 dB. Información emergente: "Reset all bands to 0 dB". |
| 63 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 63 Hz para la ruta seleccionada. |
| 125 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 125 Hz para la ruta seleccionada. |
| 250 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 250 Hz para la ruta seleccionada. |
| 500 | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 500 Hz para la ruta seleccionada. |
| 1k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 1 kHz para la ruta seleccionada. |
| 2k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 2 kHz para la ruta seleccionada. |
| 4k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 4 kHz para la ruta seleccionada. |
| 8k | Control deslizante vertical | 0 dB | −10 a +10 dB | Ajusta la banda de 8 kHz para la ruta seleccionada. |

## Consejos

- El applet siempre se abre mostrando la ruta TX. Haga clic en RX antes de ajustar los controles deslizantes para asegurarse de que está editando las bandas de recepción y no las de transmisión.
- Para comparar rápidamente el audio recibido con y sin ecualización, haga clic en ON repetidamente mientras escucha. El radio aplica o elimina el EQ de inmediato.
- Para comenzar desde cero, haga clic en el botón Reset arc. Todas las bandas RX vuelven a 0 dB con un solo clic.

## Solución de problemas

- **El botón ON no responde** — Confirme que AetherSDR está conectado al radio. El applet de EQ requiere una conexión activa con el radio para enviar los cambios.
- **Los cambios en los controles deslizantes afectan TX en lugar de RX** — TX es la vista predeterminada. Haga clic en RX primero para cambiar el applet a la ruta de recepción antes de editar las bandas.

## Relacionado

- [Descripción general del Equalizer (gráfico)](overview.md)
- [Habilitar el ecualizador gráfico en el radio para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Aumentar o reducir bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Restablecer todas las bandas a plano con un solo clic](reset-all-bands-to-flat-with-one-click.md)
- [Cambiar entre moldear el audio RX y el audio TX](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Comparar EQ activado frente a EQ desactivado rápidamente con el botón ON](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
