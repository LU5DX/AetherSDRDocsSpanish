# Explorar las memorias almacenadas en el radio

El Explorador de memorias es un panel lateral de solo lectura que enumera todas las memorias almacenadas en el radio. Úselo para revisar qué hay guardado, ver frecuencias y nombres de un vistazo, y saltar o activar cualquier entrada.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Explorador de memorias requiere una conexión activa con el radio.
- Las memorias deben estar configuradas previamente en el radio. Si no existe ninguna, el panel muestra "No memories are available yet." en lugar de una lista.
- La exploración de memorias debe estar habilitada para que el panel aparezca en la ventana principal. Consulte [Descripción general del Explorador de memorias](overview.md) para saber cómo habilitarla.

## Pasos

1. Abra `Settings > Memory...` para verificar que las memorias estén configuradas en el radio.
2. Cierre el diálogo. El panel del Explorador de memorias aparece como un panel lateral junto al panadapter cuando la exploración de memorias está habilitada.
3. Desplace la tabla de memorias para encontrar la entrada que desea. Las columnas son **Frequency** y **Name**.
4. Sintonice su VFO. La fila más cercana a la frecuencia sintonizada actual se resalta automáticamente, y la tabla se desplaza para mantener esa fila visible.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Tabla de memorias | Enumera todas las memorias almacenadas con una frecuencia válida. Las filas están ordenadas por frecuencia, de menor a mayor. | Columnas: Frequency (MHz, 6 decimales), Name. Los nombres demasiado largos se truncan con puntos suspensivos. |
| Fila resaltada | Marca la memoria cuya frecuencia es la más cercana a la frecuencia sintonizada actual. Se actualiza a medida que sintoniza. | Solo una fila está resaltada a la vez. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando el radio no tiene memorias cargadas. | La tabla se oculta mientras este indicador es visible. |

## Consejos

- La columna **Name** de una memoria muestra el nombre de la memoria si está definido, el nombre del grupo si no hay nombre de memoria, o "Memory N" (donde N es el índice) si ninguno está definido.
- Las memorias con una frecuencia de cero se excluyen completamente de la tabla.
- La fila resaltada se desplaza automáticamente al centro del área visible cuando el cambio de sintonía modifica la coincidencia más cercana.

## Relacionados

- [Descripción general del Explorador de memorias](overview.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
- [Activar una memoria con un doble clic](activate-a-memory-with-a-single-double-click.md)
