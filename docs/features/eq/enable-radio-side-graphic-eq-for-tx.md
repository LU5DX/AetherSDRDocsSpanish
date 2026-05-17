# Activar ecualizador gráfico del lado radio para TX

Esta página explica cómo activar el ecualizador gráfico para la ruta de transmisión. El ecualizador se ejecuta dentro del propio equipo Flex, dando forma al audio transmitido a través de ocho bandas fijas antes de que salga del radio.

## Antes de comenzar

- AetherSDR debe estar conectado a un equipo Flex. El applet del ecualizador requiere una conexión activa con el radio.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha. El mosaico Equalizer se abre en la fila superior del panel de applets.
2. Confirme que TX esté seleccionado. El botón TX está marcado por defecto cuando se abre el applet. Si no está resaltado, haga clic en TX.
3. Haga clic en ON. El botón se vuelve verde, lo que indica que el ecualizador de transmisión ahora está activo en el equipo.

## Descripción de cada control

| Control | Descripción | Valor predeterminado | Rango |
|---|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada (TX o RX). Verde cuando está activo. | Desactivado | Activado / Desactivado |
| TX | Selecciona las bandas del ecualizador de transmisión para su visualización y edición. | Marcado (restaurado de la sesión anterior) | — |
| RX | Selecciona las bandas del ecualizador de recepción para su visualización y edición. | Sin marcar | — |
| Botón de arco Reset | Restablece las 8 bandas de la ruta actual a 0 dB. Información sobre herramientas: "Restablecer todas las bandas a 0 dB". | — | — |
| 63 | Ajusta la banda de 63 Hz. La etiqueta de valor debajo del deslizador se actualiza en vivo. | 0 dB | −10 a +10 dB |
| 125 | Ajusta la banda de 125 Hz. | 0 dB | −10 a +10 dB |
| 250 | Ajusta la banda de 250 Hz. | 0 dB | −10 a +10 dB |
| 500 | Ajusta la banda de 500 Hz. | 0 dB | −10 a +10 dB |
| 1k | Ajusta la banda de 1 kHz. | 0 dB | −10 a +10 dB |
| 2k | Ajusta la banda de 2 kHz. | 0 dB | −10 a +10 dB |
| 4k | Ajusta la banda de 4 kHz. | 0 dB | −10 a +10 dB |
| 8k | Ajusta la banda de 8 kHz. | 0 dB | −10 a +10 dB |

## Consejos

- El botón TX está marcado por defecto la primera vez que abre el applet, y AetherSDR recuerda qué vista (RX o TX) seleccionó por última vez entre sesiones. Cada vez que abre el applet, se restaura la ruta utilizada por última vez.
- Al hacer clic en ON por segunda vez se desactiva el ecualizador sin borrar la configuración de bandas. Las posiciones de los deslizadores se conservan.
- Para comenzar con una respuesta plana antes de dar forma, haga clic en el botón de arco Reset antes de activar ON.

## Solución de problemas

- **ON no permanece encendido después de hacer clic** — El applet perdió la conexión con el equipo. Verifique que AetherSDR aún esté conectado al radio. Desconecte y reconecte si es necesario.
- **Los deslizadores se mueven pero el audio transmitido no suena diferente** — Confirme que ON esté iluminado en verde y que TX sea la ruta seleccionada, no RX.

## Relacionado

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
