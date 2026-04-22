# Saltar a la memoria más cercana a la frecuencia actual

El Memory Browser resalta automáticamente la memoria cuya frecuencia almacenada es la más próxima a su sintonía actual. Esta página explica cómo interpretar ese resaltado y usarlo para orientarse dentro de sus memorias guardadas.

## Antes de comenzar

- La radio debe estar conectada. El Memory Browser requiere una conexión activa con la radio.
- Al menos una memoria con una frecuencia válida debe estar cargada en la radio. Si no hay memorias disponibles, el panel muestra "No memories are available yet." y no hay nada que resaltar.
- El panel lateral del Memory Browser debe estar visible. Consulte [Descripción general del Memory Browser](overview.md) para saber cómo habilitarlo.

## Pasos

1. Sintonice el VFO de su radio a cualquier frecuencia usando su método habitual.
2. Observe el panel del Memory Browser junto al panadapter. El panel se actualiza automáticamente — no es necesario presionar ningún botón.
3. Localice la fila resaltada en la tabla de memorias. Esa fila corresponde a la memoria cuya frecuencia almacenada es la más cercana a su frecuencia sintonizada actual.
4. El panel se desplaza automáticamente para mantener la fila resaltada centrada en la vista.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Tabla de memorias | Lista todas las memorias con frecuencias válidas, ordenadas por frecuencia. Columnas: Frequency (MHz, seis decimales), Name. |
| Fila resaltada | Marca la única memoria más cercana a la frecuencia sintonizada actual. Se actualiza cada vez que cambia la sintonía. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias con frecuencias válidas cargadas. |

## Consejos

- La tabla está ordenada por frecuencia, no por índice de memoria, por lo que la fila resaltada siempre aparecerá cerca de otras entradas con frecuencias similares.
- Si dos memorias están a igual distancia de la frecuencia actual, se resalta la que tiene el índice de memoria menor.
- El resaltado se actualiza mientras sintoniza, por lo que puede barrer el VFO y observar cómo el resaltado se desplaza por la lista para encontrar un grupo de memorias en un segmento de banda.

## Relacionado

- [Descripción general del Memory Browser](overview.md)
- [Explorar las memorias almacenadas en la radio](browse-the-radio-s-stored-memories.md)
- [Activar una memoria con un doble clic](activate-a-memory-with-a-single-double-click.md)
