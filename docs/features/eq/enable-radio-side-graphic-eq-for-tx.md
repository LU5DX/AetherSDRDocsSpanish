# Activar el ecualizador gráfico del lado del radio para TX

Esta página explica cómo activar el ecualizador gráfico para la ruta de transmisión. El ecualizador se ejecuta dentro del propio radio Flex, dando forma a su audio transmitido en ocho bandas fijas antes de que salga del radio.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio Flex. El applet del ecualizador requiere una conexión activa al radio.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha. El mosaico Equalizer se abre en la fila superior del panel de applets.
2. Confirme que TX esté seleccionado. El botón TX está marcado por defecto cuando se abre el applet. Si no está resaltado, haga clic en TX.
3. Haga clic en ON. El botón se vuelve verde, indicando que el ecualizador de transmisión está ahora activo en el radio.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango |
|---|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta actualmente seleccionada (TX o RX). Verde cuando está activo. | Off | On / Off |
| TX | Selecciona las bandas del ecualizador de transmisión para visualización y edición. | Marcado (restaurado de la sesión anterior) | — |
| RX | Selecciona las bandas del ecualizador de recepción para visualización y edición. | Sin marcar | — |
| Botón de arco Reset | Restablece las 8 bandas de la ruta actual a 0 dB. Información sobre herramientas: "Reset all bands to 0 dB". | — | — |
| 63 | Ajusta la banda de 63 Hz. La etiqueta de valor debajo del deslizador se actualiza en vivo. Mientras se arrastra, aparece un emergente que muestra el valor en dB formateado con signo (p. ej., "+3 dB" o "-10 dB"). | 0 dB | −10 a +10 dB |
| 125 | Ajusta la banda de 125 Hz. Mientras se arrastra, aparece un emergente que muestra el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| 250 | Ajusta la banda de 250 Hz. Mientras se arrastra, aparece un emergente que muestra el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| 500 | Ajusta la banda de 500 Hz. Mientras se arrastra, aparece un emergente que muestra el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| 1k | Ajusta la banda de 1 kHz. Mientras se arrastra, aparece un emergente que muestra el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| 2k | Ajusta la banda de 2 kHz. Mientras se arrastra, aparece un emergente que muestra el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| 4k | Ajusta la banda de 4 kHz. Mientras se arrastra, aparece un emergente que muestra el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| 8k | Ajusta la banda de 8 kHz. Mientras se arrastra, aparece un emergente que muestra el valor en dB formateado con signo. | 0 dB | −10 a +10 dB |
| Escala +10 / 0 / -10 dB | Etiquetas de referencia junto a la columna de deslizadores que muestran el rango de +/-10 dB. | — | — |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Etiqueta de valor por banda | -10 a +10 | Valor en dB en vivo de cada deslizador mostrado debajo de su manija. |

## Consejos

- El botón TX está marcado por defecto la primera vez que abre el applet, y AetherSDR recuerda qué vista (RX o TX) seleccionó por última vez entre sesiones. Cada vez que abre el applet, restaura la ruta utilizada por última vez.
- Hacer clic en ON por segunda vez desactiva el ecualizador sin borrar la configuración de sus bandas. Las posiciones de sus deslizadores se conservan.
- Para comenzar desde una respuesta plana antes de dar forma, haga clic en el botón de arco Reset antes de activar ON.
- Al arrastrar un deslizador de banda del EQ, aparece un emergente cerca de la manija del deslizador que muestra el valor actual con un signo "+" para valores positivos (p. ej., "+3 dB") y un signo "-" para valores negativos (p. ej., "-5 dB"). El emergente permanece brevemente después de soltar el botón del ratón.
- El applet ahora es totalmente compatible con los colores del tema. La manija del deslizador del EQ utiliza el color de acento del tema activo, mientras que la ranura del deslizador y las etiquetas de escala utilizan los colores de fondo y texto secundario apropiados. El botón de restablecimiento y las etiquetas de banda también se adaptan a los colores del tema para una apariencia coherente.

## Solución de problemas

- **ON no permanece iluminado después de hacer clic** — El applet perdió su conexión con el radio. Verifique que AetherSDR todavía esté conectado al radio. Desconéctelo y reconéctelo si es necesario.
- **Los deslizadores se mueven pero el audio transmitido no cambia** — Confirme que ON esté iluminado en verde y que TX sea la ruta seleccionada, no RX.

## Relacionados

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
