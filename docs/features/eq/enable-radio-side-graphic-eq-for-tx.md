# Activar el ecualizador gráfico del lado radio para TX

Esta página explica cómo activar el ecualizador gráfico para la ruta de transmisión. El ecualizador funciona dentro de la propia radio Flex, moldeando el audio transmitido en ocho bandas fijas antes de que salga de la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El applet del ecualizador requiere una conexión activa con la radio.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha. El panel Equalizer se abre en la fila superior del panel de applets.
2. Confirme que TX está seleccionado. El botón TX está marcado de forma predeterminada cuando se abre el applet. Si no está resaltado, haga clic en TX.
3. Haga clic en ON. El botón se vuelve verde, indicando que el ecualizador de transmisión está ahora activo en la radio.

## Descripción de cada control

| Control | Descripción | Predeterminado | Rango |
|---|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada (TX o RX). Verde cuando está activo. | Off | On / Off |
| TX | Selecciona las bandas del ecualizador de transmisión para mostrar y editar. | Marcado (restaurado de la sesión anterior) | — |
| RX | Selecciona las bandas del ecualizador de recepción para mostrar y editar. | Sin marcar | — |
| Botón de arco Reset | Restablece las 8 bandas de la ruta actual a 0 dB. Información sobre herramientas: "Reset all bands to 0 dB". | — | — |
| 63 | Ajusta la banda de 63 Hz. La etiqueta de valor debajo del control deslizante se actualiza en vivo. Al arrastrar, aparece un mensaje emergente con el valor en dB formateado con signo (ej.: "+3 dB" o "-10 dB"). | 0 dB | −10 a +10 dB |
| 125 | Ajusta la banda de 125 Hz. Al arrastrar, aparece un mensaje emergente con el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| 250 | Ajusta la banda de 250 Hz. Al arrastrar, aparece un mensaje emergente con el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| 500 | Ajusta la banda de 500 Hz. Al arrastrar, aparece un mensaje emergente con el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| 1k | Ajusta la banda de 1 kHz. Al arrastrar, aparece un mensaje emergente con el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| 2k | Ajusta la banda de 2 kHz. Al arrastrar, aparece un mensaje emergente con el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| 4k | Ajusta la banda de 4 kHz. Al arrastrar, aparece un mensaje emergente con el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| 8k | Ajusta la banda de 8 kHz. Al arrastrar, aparece un mensaje emergente con el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| Escala +10 / 0 / -10 dB | Etiquetas de referencia junto a la columna de controles deslizantes que muestran el rango de +/-10 dB. | — | — |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Etiqueta de valor por banda | -10 a +10 | Valor dB en vivo de cada control deslizante mostrado debajo de su manija. |

## Consejos

- El botón TX está marcado de forma predeterminada la primera vez que abre el applet, y AetherSDR recuerda qué vista (RX o TX) seleccionó por última vez entre sesiones. Cada vez que abre el applet, restaura la última ruta utilizada.
- Al hacer clic en ON por segunda vez, se desactiva el ecualizador sin borrar la configuración de las bandas. Las posiciones de sus controles deslizantes se conservan.
- Para comenzar desde una respuesta plana antes de moldear, haga clic en el botón de arco Reset antes de activar ON.
- Al arrastrar un control deslizante de banda del EQ, aparece un mensaje emergente cerca de la manija del control deslizante que muestra el valor actual con un signo "+" para valores positivos (ej.: "+3 dB") y un signo "-" para valores negativos (ej.: "-5 dB"). El mensaje emergente permanece brevemente después de soltar el botón del ratón.
- Los ajustes con el teclado (ej.: usando atajos asignados) también activan la ventana emergente de valor, proporcionando la misma retroalimentación visual que al arrastrar con el ratón. Después de un paso de teclado, la ventana emergente aparece y se desvanece con el mismo tiempo de espera que al soltar el ratón.
- El applet ahora es totalmente compatible con los colores del tema. La manija del control deslizante del EQ utiliza el color de acento del tema activo, mientras que la ranura del control deslizante y las etiquetas de escala utilizan los colores de fondo y de texto secundario apropiados. El botón de reinicio y las etiquetas de banda también se adaptan a los colores del tema para una apariencia consistente.

## Solución de problemas

- **ON no permanece iluminado después de hacer clic** — El applet perdió la conexión con la radio. Verifique que AetherSDR aún esté conectado a la radio. Desconéctelo y reconéctelo si es necesario.
- **Los controles deslizantes se mueven pero el audio transmitido suena sin cambios** — Confirme que ON esté iluminado en verde y que TX sea la ruta seleccionada, no RX.

## Relacionado

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
