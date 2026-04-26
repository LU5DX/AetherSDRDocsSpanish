# Seleccionar un ajuste preestablecido de ancho de filtro para el modo actual

Los ajustes preestablecidos de ancho de filtro permiten aplicar un ancho de banda estándar al slice activo con un solo clic, o guardar su propio ancho preferido como ajuste preestablecido. Los preestablecidos son específicos del modo actual.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls requiere una conexión activa con el radio.
- El slice que desea ajustar debe estar seleccionado. Si tiene múltiples slices, use las pestañas de slice (A..H) en la parte superior del applet RX Controls para seleccionar el correcto.
- Los ajustes preestablecidos de ancho de filtro no están disponibles en los modos FM, NFM ni DFM. Cambie a un modo diferente si los botones de preestablecidos no son visibles.

## Pasos

### Aplicar un preestablecido

1. Abra el applet RX Controls. Si no está visible, haga clic en el botón **RX** de la bandeja en la barra lateral derecha.
2. Si usa múltiples slices, haga clic en la pestaña de slice correcta (A..H) para vincular el applet a ese slice.
3. En la fila de preestablecidos de filtro, haga clic en el botón que muestra el ancho deseado. El indicador de ancho de filtro actual (p. ej., **2.7K**) se actualiza de inmediato.

### Guardar un preestablecido personalizado

1. Establezca la banda de paso del filtro al ancho que desea guardar arrastrando los bordes inferior/superior del widget de banda de paso del filtro.
2. Haga clic derecho en cualquier botón de preestablecido de ancho de filtro.
3. Seleccione la opción para guardar el ancho actual en esa posición de preestablecido. La etiqueta del botón se actualiza para reflejar el nuevo valor. El valor personalizado se conserva en `FilterPresets`.

## Qué hace cada control

| Control | Comportamiento | Preestablecidos predeterminados por modo | Clave de configuración |
|---|---|---|---|
| Preestablecidos de ancho de filtro | Haga clic para aplicar ese ancho al filtro del slice. Haga clic derecho para sobrescribir el preestablecido con el ancho de filtro actual. Oculto en los modos FM/NFM/DFM. Los preestablecidos son por modo. | Ver tabla a continuación | `FilterPresets` |
| Indicador de ancho de filtro (**2.7K**) | Visualización de solo lectura que muestra el ancho de banda del filtro actual en kHz o Hz. Se actualiza cuando se aplica un preestablecido o se arrastran los bordes de la banda de paso. | — | — |
| Widget de banda de paso del filtro | Arrastre el borde inferior o superior para establecer un ancho de filtro personalizado. | — | — |

**Valores de preestablecidos predeterminados por modo:**

| Modo | Anchos de preestablecido |
|---|---|
| USB, LSB | 1800 / 2100 / 2400 / 2700 / 2900 / 3300 Hz |
| AM, SAM | 5600 / 6000 / 8000 / 10000 / 12000 / 14000 Hz |
| CW | 50 / 100 / 250 / 400 Hz |
| DIGU, DIGL | 100 / 300 / 600 / 1000 / 1500 / 2000 Hz |
| RTTY | 250 / 300 / 350 / 400 / 500 / 1000 Hz |
| FM, NFM, DFM | Sin preestablecidos (botones ocultos) |

## Consejos

- Al cambiar de modo (p. ej., de USB a CW), los botones de preestablecidos se actualizan con los anchos del nuevo modo. Los preestablecidos personalizados que haya guardado se almacenan por modo en `FilterPresets`.
- Para un control fino más allá de lo que ofrecen los preestablecidos, arrastre directamente los bordes del widget de banda de paso del filtro. Luego haga clic derecho en un botón de preestablecido para guardar ese ancho para uso futuro.

## Solución de problemas

- **Los botones de preestablecidos no son visibles** — El slice activo está en modo FM, NFM o DFM. Los preestablecidos de filtro no están disponibles para los modos de la familia FM. Cambie a un modo diferente para ver los botones de preestablecidos.

## Relacionado

- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Descripción general de RX Controls](overview.md)
