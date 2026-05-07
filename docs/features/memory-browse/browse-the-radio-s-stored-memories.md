# Explorar las memorias almacenadas del radio

El Explorador de Memorias es un panel lateral de solo lectura que enumera todas las memorias almacenadas en el FLEX-8600 conectado. Úselo para escanear frecuencias almacenadas de un vistazo y sintonizar rápidamente cualquier entrada.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El Explorador de Memorias requiere una conexión activa con el radio.
- Debe haber al menos una memoria almacenada en el radio. Si no existe ninguna, el panel muestra "No memories are available yet." y no se muestra la tabla.
- La exploración de memorias debe estar habilitada para que el panel aparezca en la ventana principal. Consulte `Settings > Memory...` para configurar las opciones de memoria.

## Pasos

1. Abra el panel lateral Explorador de Memorias. Aparece acoplado en el divisor de la ventana principal cuando la exploración de memorias está habilitada.
2. Revise la tabla de memorias. Las columnas son **Frequency** (en MHz, con seis decimales) y **Name**.
3. Desplácese por la lista. Las memorias están ordenadas por frecuencia en orden ascendente. Las entradas con la misma frecuencia se ordenan por su índice interno.
4. Observe la fila resaltada. La fila resaltada con un color de fondo distintivo es la memoria cuya frecuencia está más cerca de la frecuencia sintonizada actual.
5. Para activar una memoria, haga doble clic en su fila, o selecciónela y presione Enter.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Tabla de memorias | Enumera todas las memorias almacenadas con frecuencias válidas. Haga doble clic o presione Enter para activar una fila. | Columnas: Frequency, Name. Solo lectura; la edición está deshabilitada. |
| Fila resaltada | Marca la memoria más cercana a la frecuencia sintonizada actual. El panel se desplaza automáticamente para mantenerla visible. | Se actualiza cada vez que cambia la frecuencia sintonizada. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando el radio no tiene memorias cargadas. | Desaparece una vez que hay memorias disponibles. |

## Consejos

- La columna **Name** muestra el nombre de la memoria si está configurado. Si no se ha establecido un nombre pero se ha asignado un grupo, se muestra el nombre del grupo. Si no se ha establecido ninguno, la entrada aparece como "Memory" seguido de su número de índice.
- Las memorias con una frecuencia de 0 o no configurada se excluyen por completo de la tabla.
- Los nombres largos y las frecuencias que exceden el ancho de la columna se truncan con puntos suspensivos. Pase el cursor sobre cualquier celda para ver el valor completo en una información sobre herramientas.

## Relacionados

- [Memory Browser overview](overview.md)
- [Activate a memory with a single double-click](activate-a-memory-with-a-single-double-click.md)
- [Jump to the memory closest to the current frequency](jump-to-the-memory-closest-to-the-current-frequency.md)
