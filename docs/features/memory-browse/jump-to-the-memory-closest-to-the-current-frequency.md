# Saltar a la memoria más cercana a la frecuencia actual

El Explorador de Memorias resalta automáticamente la memoria almacenada cuya frecuencia es la más próxima a su sintonía actual. Esto le permite ver y desplazarse rápidamente hasta la memoria más relevante sin necesidad de buscar en toda la lista.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Explorador de Memorias requiere una conexión activa con el radio.
- El radio debe tener al menos una memoria con una frecuencia válida almacenada. Si no hay memorias cargadas, el panel muestra "No memories are available yet." y no se produce ningún resaltado.
- El panel lateral del Explorador de Memorias debe estar abierto. Consulte [Descripción general del Explorador de Memorias](overview.md) para saber cómo habilitarlo.

## Pasos

1. Abra el panel lateral del Explorador de Memorias. Aparece junto al panadapter en la ventana principal.
2. Sintonice el radio en cualquier frecuencia usando su método habitual (control VFO, clic en el panadapter o entrada directa).
3. Observe la tabla de memorias. La fila cuya frecuencia es la más cercana a la sintonía actual se resalta con un fondo distintivo.
4. El panel desplaza automáticamente la tabla para que la fila resaltada quede centrada en la vista. No se requiere ninguna acción adicional.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Tabla de memorias | Lista todas las memorias almacenadas ordenadas por frecuencia, de menor a mayor. | Columnas: Frecuencia (MHz, seis decimales), Nombre. |
| Fila resaltada | Marca la memoria más cercana a la frecuencia sintonizada actualmente. | Los empates se resuelven por índice de memoria: gana el índice más bajo. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando el radio no tiene memorias válidas cargadas. | Desaparece en cuanto hay al menos una memoria con una frecuencia distinta de cero disponible. |

## Consejos

- El resaltado se actualiza cada vez que cambia la frecuencia sintonizada. Si vuelve a sintonizar, la fila resaltada se desplaza a la memoria que ahora esté más cercana.
- Las memorias con una frecuencia de 0 MHz quedan excluidas de la tabla por completo y no pueden seleccionarse como la coincidencia más cercana.
- Si una memoria no tiene nombre, el panel muestra en su lugar el nombre de su grupo. Si ninguno de los dos está definido, muestra "Memory" seguido de su número de índice.

## Relacionado

- [Descripción general del Explorador de Memorias](overview.md)
- [Explorar las memorias almacenadas del radio](browse-the-radio-s-stored-memories.md)
- [Activar una memoria con un doble clic](activate-a-memory-with-a-single-double-click.md)
