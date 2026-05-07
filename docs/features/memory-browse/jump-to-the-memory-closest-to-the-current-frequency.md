# Saltar a la memoria más cercana a la frecuencia actual

El Explorador de Memorias resalta automáticamente la memoria almacenada cuya frecuencia esté más cerca de su sintonización actual. Esto le permite ver y desplazarse rápidamente a la memoria más relevante sin tener que buscar en toda la lista.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Explorador de Memorias requiere una conexión activa con la radio.
- La radio debe tener al menos una memoria con una frecuencia válida almacenada. Si no hay memorias cargadas, el panel muestra "No memories are available yet." y no se produce ningún resaltado.
- El panel lateral del Explorador de Memorias debe estar abierto. Consulte [Memory Browser overview](overview.md) para saber cómo habilitarlo.

## Pasos

1. Abra el panel lateral del Explorador de Memorias. Aparece junto al panadapter en la ventana principal.
2. Sintonice la radio a cualquier frecuencia usando su método habitual (perilla VFO, clic en el panadapter o entrada directa).
3. Observe la tabla de memorias. La fila cuya frecuencia esté más cerca de la sintonización actual se resalta con un fondo distintivo.
4. El panel desplaza automáticamente la tabla para que la fila resaltada quede centrada en la vista. No se requiere ninguna acción adicional.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Tabla de memorias | Muestra todas las memorias almacenadas ordenadas por frecuencia, de menor a mayor. | Columnas: Frecuencia (MHz, seis decimales), Nombre. |
| Fila resaltada | Marca la memoria más cercana a la frecuencia sintonizada actualmente. | Los empates se resuelven por el índice de la memoria: gana el índice más bajo. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias válidas cargadas. | Desaparece tan pronto como hay al menos una memoria con una frecuencia distinta de cero disponible. |

## Consejos

- El resaltado se actualiza cada vez que la frecuencia sintonizada cambia. Si vuelve a sintonizar, la fila resaltada se mueve a la memoria que ahora esté más cerca.
- Las memorias con una frecuencia de 0 MHz se excluyen por completo de la tabla y no pueden seleccionarse como la coincidencia más cercana.
- Si una memoria no tiene nombre, el panel muestra su nombre de grupo en su lugar. Si no se ha establecido ninguno, se muestra "Memory" seguido de su número de índice.

## Relacionados

- [Memory Browser overview](overview.md)
- [Browse the radio's stored memories](browse-the-radio-s-stored-memories.md)
- [Activate a memory with a single double-click](activate-a-memory-with-a-single-double-click.md)
