# Compare EQ activado vs EQ desactivado rápidamente con el botón ON

Use el botón ON para activar y desactivar el ecualizador del lado de la radio mientras escucha, para que pueda oír la diferencia entre la configuración actual de su banda y una respuesta plana sin mover ningún control deslizante.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet EQ requiere una conexión activa con la radio.
- Abra el panel Equalizer haciendo clic en el botón de la bandeja EQ en el panel de applets de la barra lateral derecha.
- Ajuste los controles deslizantes de su banda a una curva no plana. Activar ON cuando todas las bandas están a 0 dB no produce ninguna diferencia audible.

## Pasos

1. En el panel Equalizer, haga clic en RX o TX para seleccionar la ruta que desea evaluar.
2. Confirme que los controles deslizantes muestren la curva que desea comparar con la respuesta plana.
3. Haga clic en ON. El botón se resalta en verde y el ecualizador se aplica a la ruta seleccionada en la radio.
4. Escuche el audio.
5. Vuelva a hacer clic en ON. El resaltado verde desaparece y el ecualizador se omite (bypass), la radio vuelve a una respuesta plana en esa ruta.
6. Repita los pasos 3 a 5 tantas veces como sea necesario para comparar.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (RX o TX). Se resalta en verde cuando está activado. Las posiciones de los controles deslizantes se conservan mientras está desactivado. | Desactivado (sin marcar) |
| Reset arc (icono de revertir) | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Se muestra como una flecha de 3/4 de círculo. Información sobre herramientas: "Reset all bands to 0 dB". | N/A |
| RX | Selecciona la ruta de recepción para visualización y edición. ON actúa sobre el ecualizador RX cuando RX está activo. Se resalta en azul cuando está activo. | Sin marcar |
| TX | Selecciona la ruta de transmisión para visualización y edición. ON actúa sobre el ecualizador TX cuando TX está activo. Se resalta en azul cuando está activo. El applet se abre en la vista TX de forma predeterminada, o restaura la última vista seleccionada entre sesiones. | Marcado |
| 63 | Ajusta la banda de 63 Hz para la ruta seleccionada. La etiqueta de valor debajo del control deslizante se actualiza en vivo. Mientras arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 125 | Ajusta la banda de 125 Hz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 250 | Ajusta la banda de 250 Hz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 500 | Ajusta la banda de 500 Hz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 1k | Ajusta la banda de 1 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 2k | Ajusta la banda de 2 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 4k | Ajusta la banda de 4 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 8k | Ajusta la banda de 8 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| Escala +10 / 0 / -10 dB | Etiquetas de referencia izquierda y derecha que muestran el rango de +/-10 dB de los controles deslizantes. | N/A |

## Ventana emergente del valor al arrastrar

Cuando hace clic y arrastra cualquier control deslizante de banda del EQ, aparece una pequeña ventana emergente cerca del mango del control deslizante que muestra el valor dB exacto con un signo más o menos (p. ej., "+3 dB" o "-5 dB"). La ventana emergente sigue al mango mientras arrastra y desaparece un momento después de soltar el botón del ratón.

Esto facilita ver el valor exacto sin mirar el número debajo del control deslizante, especialmente cuando se está concentrando en los cambios de audio.

## Consejos

- ON es específico de la ruta. Activar ON mientras RX está seleccionado no afecta al ecualizador TX, y viceversa. Cambie de ruta con RX o TX antes de activarlo si desea comparar la otra dirección.
- Las posiciones de sus controles deslizantes de banda no se modifican al activar o desactivar ON. Puede activar y desactivar repetidamente sin perder su curva.
- El applet recuerda qué vista (RX o TX) seleccionó la última vez y la restaura la próxima vez que abra el panel Equalizer. La vista TX sigue siendo la predeterminada para el primer uso.
- Use el botón Reset arc para aplanar rápidamente todas las bandas de la ruta seleccionada sin hacer clic en cada control deslizante individual.
- El applet EQ ahora admite el cambio de tema en vivo. Cuando cambia el tema de la aplicación, los colores del panel EQ se actualizan en tiempo real para coincidir, incluyendo los mangos de los controles deslizantes, las etiquetas y los fondos de los botones.

## Relacionado

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Enable radio-side graphic EQ for TX](enable-radio-side-graphic-eq-for-tx.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- Reset all EQ bands to flat
