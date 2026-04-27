# Explorar las memorias almacenadas en el radio

El Memory Browser es un panel lateral de solo lectura que muestra todas las memorias almacenadas en el FLEX-8600 conectado. Úselo para revisar las frecuencias almacenadas de un vistazo y sintonizar rápidamente cualquier entrada.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El Memory Browser requiere una conexión activa con el radio.
- Debe haber al menos una memoria almacenada en el radio. Si no existe ninguna, el panel muestra "No memories are available yet." y la tabla no se visualiza.
- La navegación de memorias debe estar habilitada para que el panel aparezca en la ventana principal. Consulte `Settings > Memory...` para configurar las opciones de memoria.

## Pasos

1. Abra el panel lateral Memory Browser. Aparece acoplado en el divisor de la ventana principal cuando la navegación de memorias está habilitada.
2. Revise la tabla de memorias. Las columnas son **Frequency** (en MHz, seis decimales) y **Name**.
3. Desplácese por la lista. Las memorias están ordenadas por frecuencia en orden ascendente. Las entradas con la misma frecuencia se ordenan según su índice interno.
4. Observe la fila resaltada. La fila destacada con un color de fondo diferenciado corresponde a la memoria cuya frecuencia es la más cercana a la frecuencia sintonizada actualmente.
5. Para activar una memoria, haga doble clic en su fila, o selecciónela y presione Enter.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Tabla de memorias | Muestra todas las memorias almacenadas con frecuencias válidas. Haga doble clic o presione Enter para activar una fila. | Columnas: Frequency, Name. Solo lectura; la edición está deshabilitada. |
| Fila resaltada | Marca la memoria más cercana a la frecuencia sintonizada actualmente. El panel se desplaza automáticamente para mantenerla visible. | Se actualiza cada vez que cambia la frecuencia sintonizada. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando el radio no tiene memorias cargadas. | Desaparece una vez que hay memorias disponibles. |

## Sugerencias

- La columna **Name** muestra el nombre de la memoria si está definido. Si no se ha asignado nombre pero sí un grupo, se muestra el nombre del grupo. Si no se ha definido ninguno de los dos, la entrada aparece como "Memory" seguido de su número de índice.
- Las memorias con una frecuencia de 0 o sin definir quedan excluidas de la tabla por completo.
- Los nombres largos y las frecuencias que superan el ancho de la columna se truncan con puntos suspensivos. Coloque el cursor sobre cualquier celda para ver el valor completo en un tooltip.

## Relacionados

- [Descripción general del Memory Browser](overview.md)
- [Activar una memoria con un solo doble clic](activate-a-memory-with-a-single-double-click.md)
- [Ir a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
