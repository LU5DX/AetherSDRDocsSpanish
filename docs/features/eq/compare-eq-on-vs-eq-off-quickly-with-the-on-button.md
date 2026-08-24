# Comparación rápida de EQ activado vs desactivado con el botón ON

Use el botón ON para activar y desactivar el ecualizador del lado de la radio mientras escucha, de modo que pueda oír la diferencia entre la configuración actual de sus bandas y una respuesta plana sin mover ningún control deslizante.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet EQ requiere una conexión activa con la radio.
- Abra el mosaico Equalizer haciendo clic en el botón de la bandeja EQ en el panel de applets de la barra lateral derecha.
- Configure los controles deslizantes de banda con una curva no plana. Activar ON cuando todas las bandas están en 0 dB no produce ninguna diferencia audible.

## Pasos

1. En el mosaico Equalizer, haga clic en RX o TX para seleccionar la ruta que desea evaluar.
2. Confirme que los controles deslizantes muestran la curva que desea comparar con la respuesta plana.
3. Haga clic en ON. El botón se resalta en verde y el ecualizador se aplica a la ruta seleccionada en la radio.
4. Escuche el audio.
5. Haga clic en ON nuevamente. El resaltado verde desaparece y el ecualizador se omite: la radio vuelve a una respuesta plana en esa ruta.
6. Repita los pasos 3 a 5 tantas veces como sea necesario para comparar.

## Qué hace cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta actualmente seleccionada (RX o TX). Se resalta en verde cuando está activado. Las posiciones de los controles deslizantes se conservan mientras está omitido. | Desactivado (sin marcar) |
| Reset arc (icono de revertir) | Restablece las 8 bandas de la ruta actualmente seleccionada a 0 dB. Se dibuja como una flecha de arco de 3/4 de círculo. Información sobre herramientas: "Restablecer todas las bandas a 0 dB". | N/A |
| RX | Selecciona la ruta de recepción para visualización y edición. ON actúa sobre el ecualizador RX cuando RX está activo. Se resalta en azul cuando está activo. | Sin marcar |
| TX | Selecciona la ruta de transmisión para visualización y edición. ON actúa sobre el ecualizador TX cuando TX está activo. Se resalta en azul cuando está activo. El applet se abre en la vista TX de forma predeterminada. | Marcado |
| 63 | Ajusta la banda de 63 Hz para la ruta seleccionada. La etiqueta de valor debajo del control deslizante se actualiza en vivo. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 125 | Ajusta la banda de 125 Hz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 250 | Ajusta la banda de 250 Hz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 500 | Ajusta la banda de 500 Hz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 1k | Ajusta la banda de 1 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 2k | Ajusta la banda de 2 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 4k | Ajusta la banda de 4 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| 8k | Ajusta la banda de 8 kHz para la ruta seleccionada. Mientras arrastra, una ventana emergente muestra el valor en dB con signo (+/-). | 0 dB |
| Escala +10 / 0 / -10 dB | Etiquetas de referencia izquierda y derecha que muestran el rango de +/-10 dB de los controles deslizantes. | N/A |

## Ventana emergente de valor al arrastrar

Cuando hace clic y arrastra cualquier control deslizante de banda del EQ, aparece una pequeña ventana emergente cerca del control deslizante que muestra el valor exacto en dB con un signo más o menos (por ejemplo, "+3 dB" o "-5 dB"). La ventana emergente sigue al control deslizante mientras arrastra y desaparece poco después de soltar el botón del mouse.

Esto facilita ver el valor exacto sin mirar el número debajo del control deslizante, especialmente cuando se concentra en los cambios de audio.

## Ventana emergente de valor para ajustes con el teclado

Si usa el teclado para ajustar un control deslizante de banda del EQ (cuando los atajos de teclado están disponibles para el ajuste de controles deslizantes), aparece brevemente una ventana emergente de valor en el centro del control deslizante para mostrar el nuevo valor en dB. La ventana emergente permanece y se desvanece con el mismo tiempo de espera que al soltar el mouse, de modo que puede ver el resultado de cada paso del teclado. Esto refleja el comportamiento de lectura al arrastrar con el mouse para los ajustes con el teclado.

## Consejos

- ON es específico de la ruta. Activar ON mientras RX está seleccionado no afecta el ecualizador TX, y viceversa. Cambie las rutas con RX o TX antes de activar si desea comparar la otra dirección.
- Las posiciones de sus controles deslizantes de banda no se modifican al activar ON. Puede activar y desactivar repetidamente sin perder su curva.
- El applet se abre en la vista TX de forma predeterminada.
- Use el botón Reset arc para aplanar rápidamente todas las bandas de la ruta seleccionada sin hacer clic en cada control deslizante.
- El applet EQ admite el cambio de tema en vivo. Cuando cambia el tema de la aplicación, los colores del mosaico EQ se actualizan en tiempo real para coincidir, incluidos los controles deslizantes, las etiquetas y los fondos de los botones.
- Las subclases de control deslizante personalizadas que anulan los controladores del mouse para el posicionamiento con clic para saltar (como el WaterfallRateSlider) aún muestran correctamente la ventana emergente de valor al arrastrar, porque la implementación interna de la ventana emergente usa acceso protegido (no privado).

## Relacionados

- [Descripción general del ecualizador (gráfico)](overview.md)
- [Habilitar el EQ gráfico del lado de la radio para RX](enable-radio-side-graphic-eq-for-rx.md)
- [Habilitar el EQ gráfico del lado de la radio para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Cambiar entre dar forma al audio RX y al audio TX](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Aumentar o reducir bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- Restablecer todas las bandas del EQ a planas
