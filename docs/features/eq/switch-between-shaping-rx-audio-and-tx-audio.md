# Alternar entre la configuración del audio de recepción y transmisión

El applet Equalizer mantiene configuraciones de bandas separadas para las rutas de recepción y transmisión. Utilice los botones selectores RX y TX para elegir sobre qué ruta actúan los deslizadores y el botón ON.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El applet EQ requiere una conexión activa con la radio.
- Abra el mosaico Equalizer haciendo clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha.

## Pasos

1. Haga clic en el botón EQ de la bandeja en la barra lateral derecha para abrir el mosaico Equalizer si aún no está visible.
2. Para editar la ruta de recepción, haga clic en RX. Los deslizadores y el botón ON ahora reflejan y controlan las bandas del ecualizador de RX.
3. Para editar la ruta de transmisión, haga clic en TX. Los deslizadores y el botón ON ahora reflejan y controlan las bandas del ecualizador de TX.

## Función de cada control

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| RX | Botón de alternancia | Desactivado | Selecciona la ruta del ecualizador de recepción para visualización y edición. Resaltado en azul cuando está activo. |
| TX | Botón de alternancia | Activado | Selecciona la ruta del ecualizador de transmisión para visualización y edición. Resaltado en azul cuando está activo. El applet se abre en esta vista. |
| ON | Botón de alternancia | Desactivado | Activa o desactiva el ecualizador para la ruta (RX o TX) actualmente seleccionada. Resaltado en verde cuando está activado. |
| 63, 125, 250, 500, 1k, 2k, 4k, 8k | Deslizadores | 0 dB cada uno | Ajusta la banda de frecuencia correspondiente para la ruta seleccionada. Rango: −10 a +10 dB. La etiqueta de valor debajo de cada deslizador se actualiza en tiempo real. |
| Arco de reinicio (icono de restaurar) | Botón pulsador | — | Restablece las 8 bandas de la ruta actualmente seleccionada a 0 dB. |

## Consejos

- RX y TX son mutuamente excluyentes. Al hacer clic en uno se deselecciona automáticamente el otro. No puede editar ambas rutas al mismo tiempo.
- El botón ON, todos los deslizadores y el botón de reinicio siempre operan sobre la ruta actualmente seleccionada. Cambie a RX antes de reiniciar o ajustar si desea modificar la ruta de recepción.
- Cuando cambie de TX a RX (o viceversa), los deslizadores se actualizan inmediatamente para mostrar los valores almacenados para la ruta recién seleccionada. Los cambios realizados en la ruta anterior no se pierden.

## Relacionados

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Enable radio-side graphic EQ for TX](enable-radio-side-graphic-eq-for-tx.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)
- [Reset all bands to flat with one click](reset-all-bands-to-flat-with-one-click.md)
