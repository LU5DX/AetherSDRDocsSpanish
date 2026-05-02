# Cambiar el modo desde el panel VFO

Use la pestaña Mode del panel VFO para cambiar el modo de demodulación de cualquier slice — por ejemplo, de USB a CW o FM — sin salir de la vista del espectro.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa con el radio.
- El panel VFO debe estar abierto. Si no es visible, haga clic en la bandera marcadora VFO en el display del espectro correspondiente al slice que desea cambiar.

## Pasos

1. Haga clic en la bandera marcadora VFO en el display del espectro para el slice de destino. El panel VFO se abre, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **Mode** dentro del panel VFO.
3. Haga clic en el **Mode combo** y seleccione el modo deseado de la lista.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Ajuste persistido |
|---|---|---|---|
| Mode combo | USB | USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY | — |
| Botones de preajuste de filtro | — | Preajustes de ancho de filtro guardados | `FilterPresets` |

**Mode combo** — establece el modo de demodulación para el slice. Al seleccionar un nuevo modo, el cambio se aplica de inmediato en el radio.

**Botones de preajuste de filtro** — aparecen en la misma pestaña Mode. Cada botón aplica un ancho de filtro guardado. Haga clic derecho en un botón para guardar el ancho de filtro actual en esa posición. Los preajustes se almacenan en `FilterPresets`.

## Consejos

- Cambiar el modo puede modificar la banda de paso del filtro activo. Verifique la etiqueta de ancho de filtro en la fila de encabezado después de cambiar el modo y aplique un preajuste de filtro si es necesario.
- La etiqueta de ancho de filtro en el encabezado del panel VFO muestra el ancho de banda actual. Haga clic en ella para recorrer los botones de preajuste de filtro en la pestaña Mode.

## Relacionados

- [Aplicar un preajuste de ancho de filtro desde el panel VFO](apply-a-filter-width-preset-from-the-vfo-panel.md)
- [Establecer un borde de filtro personalizado desde el panel VFO](set-a-custom-filter-edge-from-the-vfo-panel.md)
- [Descripción general del panel VFO](overview.md)
