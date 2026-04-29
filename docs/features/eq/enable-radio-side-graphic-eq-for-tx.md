# Activar el ecualizador gráfico en el radio para TX

Esta página explica cómo activar el ecualizador gráfico en la ruta de transmisión. El ecualizador opera dentro del propio radio Flex, modelando el audio transmitido en ocho bandas fijas antes de que salga del radio.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio Flex. El applet del ecualizador requiere una conexión de radio activa.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de bandeja EQ en el panel de applets de la barra lateral derecha. El mosaico Equalizer se abre en la fila superior del panel de applets.
2. Confirme que TX está seleccionado. El botón TX está marcado de forma predeterminada cuando se abre el applet. Si no aparece resaltado, haga clic en TX.
3. Haga clic en ON. El botón se vuelve verde, lo que indica que el ecualizador de transmisión está ahora activo en el radio.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango |
|---|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (TX o RX). Verde cuando está activo. | Apagado | On / Off |
| TX | Selecciona las bandas del ecualizador de transmisión para visualización y edición. | Marcado | — |
| RX | Selecciona las bandas del ecualizador de recepción para visualización y edición. | Desmarcado | — |
| Botón de arco Reset | Restablece las 8 bandas de la ruta actual a 0 dB. Información emergente: "Reset all bands to 0 dB". | — | — |
| 63 | Ajusta la banda de 63 Hz. La etiqueta de valor debajo del control deslizante se actualiza en tiempo real. | 0 dB | −10 a +10 dB |
| 125 | Ajusta la banda de 125 Hz. | 0 dB | −10 a +10 dB |
| 250 | Ajusta la banda de 250 Hz. | 0 dB | −10 a +10 dB |
| 500 | Ajusta la banda de 500 Hz. | 0 dB | −10 a +10 dB |
| 1k | Ajusta la banda de 1 kHz. | 0 dB | −10 a +10 dB |
| 2k | Ajusta la banda de 2 kHz. | 0 dB | −10 a +10 dB |
| 4k | Ajusta la banda de 4 kHz. | 0 dB | −10 a +10 dB |
| 8k | Ajusta la banda de 8 kHz. | 0 dB | −10 a +10 dB |

## Consejos

- El botón TX está marcado de forma predeterminada cada vez que se abre el applet, por lo que no es necesario cambiar de ruta si solo desea ajustar el audio de TX.
- Hacer clic en ON por segunda vez desactiva el ecualizador sin borrar la configuración de bandas. Las posiciones de los controles deslizantes se conservan.
- Para comenzar desde una respuesta plana antes de modelar el sonido, haga clic en el botón de arco Reset antes de activar ON.

## Solución de problemas

- **ON no permanece encendido después de hacer clic** — El applet perdió la conexión con el radio. Verifique que AetherSDR siga conectado al radio. Desconecte y vuelva a conectar si es necesario.
- **Los controles deslizantes se mueven pero el audio transmitido no cambia** — Confirme que ON esté iluminado en verde y que TX sea la ruta seleccionada, no RX.

## Relacionados

- [Descripción general del Ecualizador (Gráfico)](overview.md)
- [Activar el ecualizador gráfico en el radio para RX](enable-radio-side-graphic-eq-for-rx.md)
- [Aumentar o reducir bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Restablecer todas las bandas a plano con un solo clic](reset-all-bands-to-flat-with-one-click.md)
- [Cambiar entre modelar el audio de RX y el audio de TX](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Comparar el EQ activado y desactivado rápidamente con el botón ON](compare-eq-on-vs-eq-off-quickly-with-the-on-button.md)
