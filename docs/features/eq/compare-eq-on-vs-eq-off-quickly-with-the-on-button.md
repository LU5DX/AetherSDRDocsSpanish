# Compare el ecualizador activado frente a desactivado rápidamente con el botón ON

Use el botón ON para activar y desactivar el ecualizador del lado de la radio mientras escucha, de modo que pueda oír la diferencia entre la configuración actual de su banda y una respuesta plana sin mover ningún control deslizante.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel EQ requiere una conexión activa con la radio.
- Abra el panel Equalizer haciendo clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha.
- Ajuste los controles deslizantes de banda a una curva no plana. Activar ON cuando todas las bandas están a 0 dB no produce ninguna diferencia audible.

## Pasos

1. En el panel Equalizer, haga clic en RX o TX para seleccionar la ruta que desea evaluar.
2. Confirme que los controles deslizantes muestren la curva que desea comparar con la respuesta plana.
3. Haga clic en ON. El botón se resalta en verde y el ecualizador se aplica a la ruta seleccionada en la radio.
4. Escuche el audio.
5. Vuelva a hacer clic en ON. El resaltado verde desaparece y el ecualizador se desvía: la radio vuelve a una respuesta plana en esa ruta.
6. Repita los pasos 3 a 5 tantas veces como sea necesario para comparar.

## Función de cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (RX o TX). Se resalta en verde cuando está activado. Las posiciones de los controles deslizantes se conservan mientras está desviado. | Desactivado (sin marcar) |
| Reset arc (icono de revertir) | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Se representa como una flecha en forma de 3/4 de círculo. Información sobre herramientas: "Restablecer todas las bandas a 0 dB". | N/A |
| RX | Selecciona la ruta de recepción para visualización y edición. ON actúa sobre el ecualizador de RX cuando RX está activo. Se resalta en azul cuando está activo. | Sin marcar |
| TX | Selecciona la ruta de transmisión para visualización y edición. ON actúa sobre el ecualizador de TX cuando TX está activo. Se resalta en azul cuando está activo. El applet se abre en la vista TX de forma predeterminada o restaura la última vista seleccionada entre sesiones. | Marcado |
| 63 | Ajusta la banda de 63 Hz para la ruta seleccionada. La etiqueta de valor debajo del control deslizante se actualiza en tiempo real. Al arrastrar, aparece una ventana emergente que muestra el valor en dB con signo (+/-). | 0 dB |
| 125 | Ajusta la banda de 125 Hz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente que muestra el valor en dB con signo (+/-). | 0 dB |
| 250 | Ajusta la banda de 250 Hz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente que muestra el valor en dB con signo (+/-). | 0 dB |
| 500 | Ajusta la banda de 500 Hz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente que muestra el valor en dB con signo (+/-). | 0 dB |
| 1k | Ajusta la banda de 1 kHz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente que muestra el valor en dB con signo (+/-). | 0 dB |
| 2k | Ajusta la banda de 2 kHz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente que muestra el valor en dB con signo (+/-). | 0 dB |
| 4k | Ajusta la banda de 4 kHz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente que muestra el valor en dB con signo (+/-). | 0 dB |
| 8k | Ajusta la banda de 8 kHz para la ruta seleccionada. Al arrastrar, aparece una ventana emergente que muestra el valor en dB con signo (+/-). | 0 dB |
| Escala +10 / 0 / -10 dB | Etiquetas de referencia izquierda y derecha que muestran el rango de +/-10 dB de los controles deslizantes. | N/A |

## Ventana emergente de valor al arrastrar

Cuando hace clic y arrastra cualquier control deslizante de banda del ecualizador, aparece una pequeña ventana emergente cerca del control que muestra el valor exacto en dB con un signo más o menos (por ejemplo, "+3 dB" o "-5 dB"). La ventana sigue al control mientras arrastra y desaparece poco después de soltar el botón del ratón.

Esto facilita ver el valor exacto sin tener que mirar el número debajo del control deslizante, especialmente cuando se está concentrando en los cambios de audio.

## Consejos

- ON es específico de cada ruta. Activar ON mientras RX está seleccionado no afecta al ecualizador de TX, y viceversa. Cambie de ruta con RX o TX antes de activar ON si desea comparar la otra dirección.
- Las posiciones de los controles deslizantes de banda no se modifican al activar o desactivar ON. Puede activar y desactivar repetidamente sin perder su curva.
- El applet recuerda qué vista (RX o TX) seleccionó por última vez y la restaura la próxima vez que abra el panel Equalizer. La vista TX sigue siendo la predeterminada para el primer uso.
- Use el botón Reset arc para aplanar rápidamente todas las bandas de la ruta seleccionada sin hacer clic en cada control deslizante individual.

## Relacionados

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Enable radio-side graphic EQ for TX](enable-radio-side-graphic-eq-for-tx.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- Reset all EQ bands to flat
