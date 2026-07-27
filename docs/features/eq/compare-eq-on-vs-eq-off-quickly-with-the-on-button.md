# Compare rápidamente EQ activado vs desactivado con el botón ON

Use el botón ON para activar y desactivar el ecualizador del lado de la radio mientras escucha, de modo que pueda oír la diferencia entre la configuración actual de su banda y una respuesta plana sin mover ningún control deslizante.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. La applet EQ requiere una conexión activa con la radio.
- Abra el mosaico Equalizer haciendo clic en el botón de la bandeja EQ en el panel de applets de la barra lateral derecha.
- Ajuste los controles deslizantes de la banda a una curva no plana. Activar ON cuando todas las bandas están a 0 dB no produce ninguna diferencia audible.

## Pasos

1. En el mosaico Equalizer, haga clic en RX o TX para seleccionar la ruta que desea evaluar.
2. Confirme que los controles deslizantes muestran la curva que desea comparar con la respuesta plana.
3. Haga clic en ON. El botón se resalta en verde y el ecualizador se aplica a la ruta seleccionada en la radio.
4. Escuche el audio.
5. Vuelva a hacer clic en ON. El resalte verde desaparece y el ecualizador se omite: la radio vuelve a una respuesta plana en esa ruta.
6. Repita los pasos 3 a 5 tantas veces como sea necesario para comparar.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (RX o TX). Se resalta en verde cuando está activado. Las posiciones de los controles deslizantes se conservan mientras está desactivado. | Desactivado (sin marcar) |
| Reset arc (icono de revertir) | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. Se muestra como una flecha circular de 3/4 de círculo. Información sobre herramientas: "Reset all bands to 0 dB". | N/A |
| RX | Selecciona la ruta de recepción para su visualización y edición. ON actúa sobre el ecualizador RX cuando RX está activo. Se resalta en azul cuando está activo. | Sin marcar |
| TX | Selecciona la ruta de transmisión para su visualización y edición. ON actúa sobre el ecualizador TX cuando TX está activo. Se resalta en azul cuando está activo. La applet se abre en la vista TX de forma predeterminada. | Marcado |
| 63 | Ajusta la banda de 63 Hz para la ruta seleccionada. La etiqueta de valor debajo del control deslizante se actualiza en vivo. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 125 | Ajusta la banda de 125 Hz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 250 | Ajusta la banda de 250 Hz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 500 | Ajusta la banda de 500 Hz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 1k | Ajusta la banda de 1 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 2k | Ajusta la banda de 2 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 4k | Ajusta la banda de 4 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 8k | Ajusta la banda de 8 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| +10 / 0 / -10 dB scale | Etiquetas de referencia izquierda y derecha que muestran el rango de +/-10 dB de los controles deslizantes. | N/A |

## Ventana emergente de valor al arrastrar

Al hacer clic y arrastrar cualquier control deslizante de banda EQ, aparece una pequeña ventana emergente cerca del control que muestra el valor exacto en dB con un signo más o menos (por ejemplo, "+3 dB" o "-5 dB"). La ventana sigue el control mientras arrastra y desaparece poco después de soltar el botón del ratón.

Esto facilita ver el valor exacto sin tener que mirar el número debajo del control deslizante, especialmente cuando se está concentrando en los cambios de audio.

## Ventana emergente de valor para ajustes con teclado

Si usa el teclado para ajustar un control deslizante de banda EQ (cuando los atajos de teclado están disponibles para el ajuste del control deslizante), aparece brevemente una ventana emergente de valor en el centro del control deslizante para mostrar el nuevo valor en dB. La ventana persiste y se desvanece con el mismo tiempo de espera que al soltar el ratón, para que pueda ver el resultado de cada paso de teclado. Esto replica el comportamiento de la lectura al arrastrar con el ratón para los ajustes con teclado.

## Consejos

- ON es específico de la ruta. Activar ON mientras RX está seleccionado no afecta al ecualizador TX, y viceversa. Cambie de ruta con RX o TX antes de activar si desea comparar la otra dirección.
- Las posiciones de los controles deslizantes de la banda no se modifican al activar o desactivar ON. Puede activar y desactivar repetidamente sin perder su curva.
- La applet se abre en la vista TX de forma predeterminada.
- Use el botón Reset arc para aplanar rápidamente todas las bandas de la ruta seleccionada sin hacer clic en cada control deslizante.
- La applet EQ admite el cambio de tema en vivo. Cuando cambia el tema de la aplicación, los colores del mosaico EQ se actualizan en tiempo real para coincidir, incluidos los controles deslizantes, las etiquetas y los fondos de los botones.
- Las subclases de controles deslizantes personalizados que anulan los controladores del ratón para la posición con clic (como WaterfallRateSlider) siguen mostrando la ventana emergente de valor al arrastrar correctamente, porque la implementación interna de la ventana emergente utiliza acceso protegido (no privado).

## Relacionados

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Enable radio-side graphic EQ for TX](enable-radio-side-graphic-eq-for-tx.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- Reset all EQ bands to flat
