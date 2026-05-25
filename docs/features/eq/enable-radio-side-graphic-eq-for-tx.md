# Activar el ecualizador gráfico del lado radio para TX

Esta página explica cómo activar el ecualizador gráfico para la ruta de transmisión. El ecualizador se ejecuta dentro del propio radio Flex, dando forma a su audio transmitido en ocho bandas fijas antes de que salga del radio.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio Flex. El applet del EQ requiere una conexión activa al radio.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha. El mosaico Equalizer se abre en la fila superior del panel de applets.
2. Confirme que TX esté seleccionado. El botón TX está marcado por defecto cuando se abre el applet. Si no está resaltado, haga clic en TX.
3. Haga clic en ON. El botón se vuelve verde, indicando que el ecualizador de transmisión está ahora activo en el radio.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango |
|---|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (TX o RX). Verde cuando está activo. | Off | On / Off |
| TX | Selecciona las bandas del ecualizador de transmisión para mostrar y editar. | Marcado (restaurado de la sesión anterior) | — |
| RX | Selecciona las bandas del ecualizador de recepción para mostrar y editar. | Sin marcar | — |
| Botón de arco Reset | Restablece las 8 bandas de la ruta actual a 0 dB. Información sobre herramientas: "Reset all bands to 0 dB". | — | — |
| 63 | Ajusta la banda de 63 Hz. La etiqueta de valor debajo del deslizador se actualiza en vivo. Mientras arrastra, un panel emergente muestra el valor en dB con signo (p. ej., "+3 dB" o "-10 dB"). | 0 dB | −10 a +10 dB |
| 125 | Ajusta la banda de 125 Hz. Mientras arrastra, un panel emergente muestra el valor en dB con signo. | 0 dB | −10 a +10 dB |
| 250 | Ajusta la banda de 250 Hz. Mientras arrastra, un panel emergente muestra el valor en dB con signo. | 0 dB | −10 a +10 dB |
| 500 | Ajusta la banda de 500 Hz. Mientras arrastra, un panel emergente muestra el valor en dB con signo. | 0 dB | −10 a +10 dB |
| 1k | Ajusta la banda de 1 kHz. Mientras arrastra, un panel emergente muestra el valor en dB con signo. | 0 dB | −10 a +10 dB |
| 2k | Ajusta la banda de 2 kHz. Mientras arrastra, un panel emergente muestra el valor en dB con signo. | 0 dB | −10 a +10 dB |
| 4k | Ajusta la banda de 4 kHz. Mientras arrastra, un panel emergente muestra el valor en dB con signo. | 0 dB | −10 a +10 dB |
| 8k | Ajusta la banda de 8 kHz. Mientras arrastra, un panel emergente muestra el valor en dB con signo. | 0 dB | −10 a +10 dB |

## Consejos

- El botón TX está marcado por defecto la primera vez que abre el applet, y AetherSDR recuerda qué vista (RX o TX) seleccionó por última vez entre sesiones. Cada vez que abre el applet, restaura la ruta utilizada por última vez.
- Al hacer clic en ON por segunda vez se desactiva el ecualizador sin borrar la configuración de sus bandas. Las posiciones de sus deslizadores se conservan.
- Para comenzar desde una respuesta plana antes de dar forma, haga clic en el botón de arco Reset antes de activar ON.
- Al arrastrar un deslizador de banda del EQ, aparece un panel emergente cerca del control deslizante que muestra el valor actual con un signo "+" para valores positivos (p. ej., "+3 dB") y un signo "-" para valores negativos (p. ej., "-5 dB"). El panel emergente permanece brevemente después de soltar el botón del ratón.

## Solución de problemas

- **ON no permanece encendido después de hacer clic** — El applet perdió su conexión al radio. Verifique que AetherSDR todavía esté conectado al radio. Desconecte y vuelva a conectar si es necesario.
- **Los deslizadores se mueven pero el audio transmitido suena igual** — Confirme que ON esté iluminado en verde y que TX sea la ruta seleccionada, no RX.

## Relacionados

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
