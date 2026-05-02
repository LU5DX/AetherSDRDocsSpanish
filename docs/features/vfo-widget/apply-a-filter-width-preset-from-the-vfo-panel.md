# Aplicar un ajuste preestablecido de ancho de filtro desde el panel VFO

Los botones de ajustes preestablecidos de filtro permiten cambiar el ancho del filtro de recepción de un slice (canal de recepción) con un solo clic. Úselos para pasar rápidamente entre anchos de banda comunes — por ejemplo, entre un filtro SSB amplio de 3 kHz y un filtro CW estrecho de 500 Hz — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa con el radio.
- El panel VFO del slice de destino debe estar abierto y expandido. Si está contraído en una barra de solo frecuencia, haga clic en cualquier parte de él para expandirlo primero.

## Pasos

1. Haga clic en la bandera marcadora VFO en la pantalla del espectro correspondiente al slice que desea ajustar. El panel VFO se abre anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el botón de ajuste preestablecido de filtro que corresponda al ancho de banda deseado. El radio aplica inmediatamente ese ancho de filtro al slice.

Para guardar el ancho de filtro actual en una ranura de ajuste preestablecido:

1. Configure el filtro con el ancho de banda que desea guardar (consulte [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)).
2. Haga clic derecho en la ranura del botón preestablecido que desea sobreescribir.
3. El ancho de filtro actual queda guardado en esa ranura.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de ajuste |
|---|---|---|---|
| Botones de ajuste preestablecido de filtro (pestaña Mode) | Cada botón aplica un ancho de filtro preestablecido guardado al slice. Clic izquierdo para aplicar; clic derecho para guardar el ancho de filtro actual en esa ranura. Los bordes de filtro alto y bajo personalizados se pueden almacenar por ranura mediante clic derecho. | — | `FilterPresets` |
| Etiqueta de ancho de filtro | Muestra el ancho de banda de filtro actual. Haga clic para recorrer los botones de ajuste preestablecido de filtro en la pestaña Mode. | — | — |

## Consejos

- La etiqueta de ancho de filtro en el encabezado del panel VFO muestra en todo momento el ancho de banda activo. Haga clic directamente sobre ella para recorrer los botones preestablecidos sin necesidad de cambiar primero a la pestaña Mode.
- Las ranuras de ajustes preestablecidos son compartidas entre todos los slices y modos. Sobreescribir una ranura afecta a todos los slices que la utilizan.
- Las líneas de borde de filtro en el panadapter del espectro reflejan el ancho de filtro activo. Si las líneas están ocultas, actívelas con el botón Filter edges en el panel VFO. Consulte [Ocultar o mostrar las líneas de borde de filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md).

## Relacionados

- [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)
- [Cambiar el modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Ocultar o mostrar las líneas de borde de filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Descripción general del panel VFO](overview.md)
