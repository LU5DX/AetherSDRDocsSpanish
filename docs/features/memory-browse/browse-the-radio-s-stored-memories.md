# Navegar por las memorias almacenadas de la radio

El Explorador de memorias es un panel lateral que enumera todas las memorias almacenadas en la FLEX-8600 conectada. Úselo para examinar frecuencias almacenadas de un vistazo, sintonizar rápidamente cualquier entrada o guardar el slice actual como una nueva memoria.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El Explorador de memorias requiere una conexión activa con la radio.
- Debe haber al menos una memoria almacenada en la radio. Si no existe ninguna, el panel muestra "No memories are available yet." y la tabla no se muestra.
- La exploración de memorias debe estar habilitada para que el panel aparezca en la ventana principal. Consulte `Settings > Memory...` para configurar las opciones de memoria.

## Pasos

1. Abra el panel lateral Explorador de memorias. Aparece acoplado en el divisor de la ventana principal cuando la exploración de memorias está habilitada.
2. Revise la tabla de memorias. Las columnas son **Frequency** (en MHz, con seis decimales) y **Name**.
3. Desplácese por la lista. Las memorias están ordenadas por frecuencia ascendente. Las entradas con la misma frecuencia se ordenan por su índice interno.
4. Observe la fila resaltada. La fila resaltada con un color de fondo distintivo es la memoria cuya frecuencia está más cerca de la frecuencia sintonizada actual.
5. Para activar una memoria, haga doble clic en su fila, o selecciónela y presione Enter.
6. Para guardar el slice actual como una nueva memoria, haga clic en **Add Memory** en la parte inferior del panel.

## Qué hace cada control

| Control                          | Comportamiento                                                                                              | Notas                                                                                                                           |
|----------------------------------|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Memory table                     | Muestra cada memoria ordenada por frecuencia; un solo clic o Enter activa el slice sintonizado en esa memoria. | Columnas: Frequency, Name. La memoria más cercana a la sintonización actual se resalta con un fondo distintivo. El doble clic también sintoniza. |
| Highlighted row                  | Marca la memoria más cercana a la frecuencia sintonizada actual. El panel se desplaza automáticamente para mantenerla visible. | Se actualiza cada vez que cambia la frecuencia sintonizada.                                                                     |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias cargadas.                                 | Desaparece cuando hay memorias disponibles.                                                                                     |
| Add Memory                       | Guarda el slice actual como una nueva entrada de memoria. Fijado en la parte inferior del panel, siempre visible. | Añadido en v26.5.1 (#2533). Reemplaza la variante anterior de la insignia de letra de slice.                                    |

## Consejos

- La columna **Name** muestra el nombre de la memoria si está configurado. Si no se ha configurado un nombre pero sí un grupo, se muestra el nombre del grupo en su lugar. Si no se ha configurado ninguno, la entrada aparece como "Memory" seguida de su número de índice.
- Las memorias con frecuencia 0 o sin configurar se excluyen por completo de la tabla.
- Los nombres largos y las frecuencias que exceden el ancho de la columna se truncan con puntos suspensivos. Coloque el cursor sobre cualquier celda para ver el valor completo en una información sobre herramientas.
- El botón **Add Memory** permanece visible sin importar qué tan lejos se desplace en la tabla de memorias.

## Relacionado

- [Memory Browser overview](overview.md)
- [Activate a memory with a single double-click](activate-a-memory-with-a-single-double-click.md)
- [Jump to the memory closest to the current frequency](jump-to-the-memory-closest-to-the-current-frequency.md)
- [Save the current slice as a memory](save-the-current-slice-as-a-memory.md)
