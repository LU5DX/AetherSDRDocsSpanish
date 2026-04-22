# Cambiar entre ajuste de audio RX y audio TX

El applet Equalizer mantiene configuraciones de banda independientes para las rutas de recepción y transmisión. Use los botones selectores RX y TX para elegir sobre qué ruta actúan los controles deslizantes y el botón ON.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet EQ requiere una conexión de radio activa.
- Abra el panel Equalizer haciendo clic en el botón EQ del bandeja en el panel de applets de la barra lateral derecha.

## Pasos

1. Haga clic en el botón EQ de la bandeja en la barra lateral derecha para abrir el panel Equalizer si aún no está visible.
2. Para editar la ruta de recepción, haga clic en RX. Los controles deslizantes y el botón ON reflejarán y controlarán las bandas del ecualizador RX.
3. Para editar la ruta de transmisión, haga clic en TX. Los controles deslizantes y el botón ON reflejarán y controlarán las bandas del ecualizador TX.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| RX | Botón de alternancia | Sin marcar | Selecciona la ruta del ecualizador de recepción para visualización y edición. Resaltado en azul cuando está activo. |
| TX | Botón de alternancia | Marcado | Selecciona la ruta del ecualizador de transmisión para visualización y edición. Resaltado en azul cuando está activo. El applet se abre en esta vista. |
| ON | Botón de alternancia | Sin marcar | Activa o desactiva el ecualizador para la ruta seleccionada en ese momento (RX o TX). Resaltado en verde cuando está habilitado. |
| 63, 125, 250, 500, 1k, 2k, 4k, 8k | Controles deslizantes | 0 dB cada uno | Ajustan la banda de frecuencia correspondiente para la ruta seleccionada. Rango: −10 a +10 dB. La etiqueta de valor debajo de cada control se actualiza en tiempo real. |
| Arco de restablecimiento (ícono de revertir) | Botón de acción | — | Restablece las 8 bandas de la ruta seleccionada actualmente a 0 dB. |

## Consejos

- RX y TX son mutuamente excluyentes. Al hacer clic en uno se deselecciona el otro automáticamente. No es posible editar ambas rutas al mismo tiempo.
- El botón ON, todos los controles deslizantes y el botón de restablecimiento siempre operan sobre la ruta seleccionada en ese momento. Cambie a RX antes de restablecer o ajustar si desea modificar la ruta de recepción.
- Al cambiar de TX a RX (o viceversa), los controles deslizantes se actualizan de inmediato para mostrar los valores almacenados de la ruta recién seleccionada. Los cambios realizados en la ruta anterior no se pierden.

## Relacionados

- [Descripción general del Ecualizador (Gráfico)](overview.md)
- [Habilitar EQ gráfico del lado de la radio para RX](enable-radio-side-graphic-eq-for-rx.md)
- [Habilitar EQ gráfico del lado de la radio para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Aumentar o reducir bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Restablecer todas las bandas a plano con un solo clic](reset-all-bands-to-flat-with-one-click.md)
