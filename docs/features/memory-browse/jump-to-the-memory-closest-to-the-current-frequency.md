# Saltar a la memoria más cercana a la frecuencia actual

El Explorador de Memorias resalta automáticamente la memoria cuya frecuencia almacenada es la más próxima a su sintonía actual. Utilice esta función para encontrar y confirmar rápidamente el punto de referencia más cercano sin desplazarse manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel lateral del Explorador de Memorias debe estar abierto. Consulte [Descripción general del Explorador de Memorias](overview.md).
- La radio debe tener al menos una memoria con una frecuencia válida almacenada. Si no hay ninguna cargada, el panel muestra "No memories are available yet." y no se produce ningún resaltado.

## Pasos

1. Abra el panel lateral del Explorador de Memorias. Se encuentra junto al panadapter en la ventana principal.
2. Sintonice la radio en cualquier frecuencia mediante el VFO o el panadapter.
3. Observe la tabla de memorias. La fila correspondiente a la memoria más cercana a su frecuencia actual se resalta automáticamente.
4. Si la fila resaltada no está visible, el panel la desplaza hasta el centro de la tabla.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Tabla de memorias | Lista todas las memorias almacenadas ordenadas por frecuencia. Columnas: Frequency (MHz), Name. |
| Fila resaltada | Marca la única memoria cuya frecuencia es la más cercana a la frecuencia sintonizada actualmente. Se actualiza cada vez que cambia la sintonía. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias cargadas. |

## Consejos

- La tabla está ordenada por frecuencia, de modo que la fila resaltada también indica la posición de su frecuencia actual en relación con todas las memorias almacenadas.
- Si dos memorias están igualmente cerca de la frecuencia actual, se resalta aquella con el índice de memoria más bajo.
- Las memorias con una frecuencia de 0 quedan excluidas de la tabla y del cálculo de la coincidencia más cercana.
- El nombre mostrado de una memoria proviene de su campo de nombre si está definido, del nombre de grupo si el nombre está en blanco, o de "Memory N" como alternativa.

## Relacionado

- [Descripción general del Explorador de Memorias](overview.md)
- [Explorar las memorias almacenadas de la radio](browse-the-radio-s-stored-memories.md)
- [Activar una memoria con un doble clic](activate-a-memory-with-a-single-double-click.md)
