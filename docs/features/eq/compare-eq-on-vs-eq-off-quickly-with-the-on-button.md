# Compare el EQ activado vs. EQ desactivado rápidamente con el botón ON

Use el botón ON para alternar el ecualizador del lado de la radio dentro y fuera mientras escucha, de modo que pueda oír la diferencia entre la configuración actual de su banda y una respuesta plana sin mover ningún control deslizante.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet EQ requiere una conexión de radio activa.
- Abra el mosaico Equalizer haciendo clic en el botón de la bandeja EQ en el panel de applets de la barra lateral derecha.
- Ajuste los controles deslizantes de su banda a una curva no plana. Alternar ON cuando todas las bandas están a 0 dB no produce ninguna diferencia audible.

## Pasos

1. En el mosaico Equalizer, haga clic en RX o TX para seleccionar la ruta que desea evaluar.
2. Confirme que los controles deslizantes muestren la curva que desea comparar con la respuesta plana.
3. Haga clic en ON. El botón se resalta en verde y el ecualizador se aplica a la ruta seleccionada en la radio.
4. Escuche el audio.
5. Vuelva a hacer clic en ON. El resaltado verde desaparece y el ecualizador se desvía: la radio vuelve a una respuesta plana en esa ruta.
6. Repita los pasos 3 a 5 tantas veces como sea necesario para comparar.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (RX o TX). Se resalta en verde cuando está activado. Las posiciones de los controles deslizantes se conservan mientras está desviado. | Desactivado (sin marcar) |
| Reset arc (icono de revertir) | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Se muestra como una flecha circular de 3/4. Información sobre herramientas: "Restablecer todas las bandas a 0 dB". | N/A |
| RX | Selecciona la ruta de recepción para visualización y edición. ON actúa sobre el ecualizador RX cuando RX está activo. Se resalta en azul cuando está activo. | Sin marcar |
| TX | Selecciona la ruta de transmisión para visualización y edición. ON actúa sobre el ecualizador TX cuando TX está activo. Se resalta en azul cuando está activo. El applet se abre en la vista TX por defecto, o restaura la última vista seleccionada entre sesiones. | Marcado |
| 63 | Ajusta la banda de 63 Hz para la ruta seleccionada. La etiqueta de valor debajo del control deslizante se actualiza en vivo. Mientras se arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 125 | Ajusta la banda de 125 Hz para la ruta seleccionada. Mientras se arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 250 | Ajusta la banda de 250 Hz para la ruta seleccionada. Mientras se arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 500 | Ajusta la banda de 500 Hz para la ruta seleccionada. Mientras se arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 1k | Ajusta la banda de 1 kHz para la ruta seleccionada. Mientras se arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 2k | Ajusta la banda de 2 kHz para la ruta seleccionada. Mientras se arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 4k | Ajusta la banda de 4 kHz para la ruta seleccionada. Mientras se arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| 8k | Ajusta la banda de 8 kHz para la ruta seleccionada. Mientras se arrastra, una ventana emergente muestra el valor dB con signo (+/-). | 0 dB |
| Escala +10 / 0 / -10 dB | Etiquetas de referencia izquierda y derecha que muestran el rango de +/-10 dB de los controles deslizantes. | N/A |

## Ventana emergente de valor al arrastrar

Cuando hace clic y arrastra cualquier control deslizante de banda del EQ, aparece una pequeña ventana emergente cerca del control que muestra el valor dB exacto con un signo más o menos (p. ej., "+3 dB" o "-5 dB"). La ventana sigue al control mientras arrastra y desaparece unos instantes después de soltar el botón del ratón.

Esto facilita ver el valor exacto sin mirar el número debajo del control, especialmente cuando se está concentrando en los cambios de audio.

## Ventana emergente de valor para ajustes con teclado

Si usa el teclado para ajustar un control deslizante de banda del EQ (cuando los atajos de teclado están disponibles para el ajuste del control), aparece brevemente una ventana emergente de valor en el centro del control para mostrar el nuevo valor dB. La ventana permanece y se desvanece con el mismo tiempo de espera que al soltar el ratón, para que pueda ver el resultado de cada paso del teclado. Esto refleja el comportamiento de la lectura al arrastrar con el ratón para los ajustes de teclado.

## Consejos

- ON es específico de la ruta. Alternar ON mientras RX está seleccionado no afecta al ecualizador TX, y viceversa. Cambie de ruta con RX o TX antes de alternar si desea comparar la otra dirección.
- Las posiciones de los controles deslizantes de su banda no se modifican al alternar ON. Puede activar y desactivar de forma segura repetidamente sin perder su curva.
- El applet recuerda qué vista (RX o TX) seleccionó por última vez y la restaura la próxima vez que abra el mosaico Equalizer. La vista TX sigue siendo la predeterminada para el primer uso.
- Use el botón Reset arc para aplanar rápidamente todas las bandas de la ruta seleccionada sin hacer clic en cada control deslizante individual.
- El applet EQ ahora admite el cambio de tema en vivo. Cuando cambia el tema de la aplicación, los colores del mosaico EQ se actualizan en tiempo real para coincidir, incluidos los controles deslizantes, las etiquetas y los fondos de los botones.

## Relacionados

- [Descripción general del ecualizador (gráfico)](overview.md)
- [Activar EQ gráfico del lado de la radio para RX](enable-radio-side-graphic-eq-for-rx.md)
- [Activar EQ gráfico del lado de la radio para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Cambiar entre dar forma al audio RX y al audio TX](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Aumentar o atenuar bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- Restablecer todas las bandas del EQ a plano
