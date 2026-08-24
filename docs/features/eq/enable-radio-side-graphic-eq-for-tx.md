# Activar el ecualizador gráfico del lado del radio para TX

Esta página explica cómo activar el ecualizador gráfico para la ruta de transmisión. El ecualizador se ejecuta dentro del propio radio Flex, moldeando su audio transmitido a través de ocho bandas fijas antes de que salga del radio.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio Flex. El applet de EQ requiere una conexión activa al radio.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja EQ en el panel de applets de la barra lateral derecha. El mosaico Equalizer se abre en la fila superior del panel de applets.
2. Confirme que TX está seleccionado. El botón TX está marcado por defecto cuando se abre el applet. Si no está resaltado, haga clic en TX.
3. Haga clic en ON. El botón se vuelve verde, lo que indica que el ecualizador de transmisión está ahora activo en el radio.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango |
|---|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (TX o RX). Verde cuando está activo. | Apagado | Encendido / Apagado |
| TX | Selecciona las bandas del ecualizador de transmisión para visualización y edición. | Marcado | — |
| RX | Selecciona las bandas del ecualizador de recepción para visualización y edición. | Desmarcado | — |
| Botón de arco Reset | Restablece las 8 bandas de la ruta actual a 0 dB. Información sobre herramientas: "Reset all bands to 0 dB". | — | — |
| 63 | Ajusta la banda de 63 Hz. La etiqueta de valor debajo del control deslizante se actualiza en vivo. Mientras arrastra, una ventana emergente muestra el valor formateado en dB con signo (p. ej., "+3 dB" o "-10 dB"). | 0 dB | −10 a +10 dB |
| 125 | Ajusta la banda de 125 Hz. Mientras arrastra, una ventana emergente muestra el valor formateado en dB con signo. | 0 dB | −10 a +10 dB |
| 250 | Ajusta la banda de 250 Hz. Mientras arrastra, una ventana emergente muestra el valor formateado en dB con signo. | 0 dB | −10 a +10 dB |
| 500 | Ajusta la banda de 500 Hz. Mientras arrastra, una ventana emergente muestra el valor formateado en dB con signo. | 0 dB | −10 a +10 dB |
| 1k | Ajusta la banda de 1 kHz. Mientras arrastra, una ventana emergente muestra el valor formateado en dB con signo. | 0 dB | −10 a +10 dB |
| 2k | Ajusta la banda de 2 kHz. Mientras arrastra, una ventana emergente muestra el valor formateado en dB con signo. | 0 dB | −10 a +10 dB |
| 4k | Ajusta la banda de 4 kHz. Mientras arrastra, una ventana emergente muestra el valor formateado en dB con signo. | 0 dB | −10 a +10 dB |
| 8k | Ajusta la banda de 8 kHz. Mientras arrastra, una ventana emergente muestra el valor formateado en dB con signo. | 0 dB | −10 a +10 dB |
| Escala +10 / 0 / −10 dB | Etiquetas de referencia junto a la columna de controles deslizantes que muestran el rango de ±10 dB. | — | — |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Etiqueta de valor por banda | −10 a +10 | Valor en dB en vivo de cada control deslizante mostrado debajo de su manija. |

## Consejos

- El botón TX está marcado por defecto la primera vez que abre el applet, y AetherSDR recuerda qué vista (RX o TX) seleccionó por última vez entre sesiones. Cada vez que abre el applet, se restaura la última ruta utilizada.
- Hacer clic en ON una segunda vez desactiva el ecualizador sin borrar sus ajustes de banda. Las posiciones de sus controles deslizantes se conservan.
- Para comenzar desde una respuesta plana antes de dar forma, haga clic en el botón de arco Reset antes de activar ON.
- Al arrastrar un control deslizante de banda EQ, aparece una ventana emergente cerca de la manija del control mostrando el valor actual con un signo "+" para valores positivos (p. ej., "+3 dB") y un signo "-" para valores negativos (p. ej., "-5 dB"). La ventana emergente permanece brevemente después de soltar el botón del ratón.
- Los ajustes con el teclado (p. ej., usando accesos directos asignados) también activan la ventana emergente de valor, proporcionando la misma retroalimentación visual que el arrastre con el ratón. Después de un paso con el teclado, la ventana emergente aparece y se desvanece con el mismo tiempo de permanencia que al soltar el ratón.
- El applet ahora admite completamente los colores del tema. La manija del control deslizante EQ usa el color de acento del tema activo, mientras que la ranura del control y las etiquetas de escala usan los colores de fondo y texto secundario apropiados. El botón de reset y las etiquetas de banda también se adaptan a los colores del tema para una apariencia coherente.
- Las implementaciones personalizadas de controles deslizantes (como aquellas con posicionamiento por clic para saltar) también muestran la ventana emergente de valor de arrastre, asegurando una retroalimentación visual coherente independientemente del comportamiento de arrastre del control.

## Solución de problemas

- **ON no permanece encendido después de hacer clic** — El applet perdió su conexión con el radio. Verifique que AetherSDR siga conectado al radio. Desconecte y reconecte si es necesario.
- **Los controles deslizantes se mueven pero el audio transmitido suena igual** — Confirme que ON esté iluminado en verde y que TX sea la ruta seleccionada, no RX.

## Relacionado

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Compare EQ on vs EQ off quickly with the ON button](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
