# Navegar por las memorias almacenadas del radio

El Explorador de Memorias es un panel lateral que enumera todas las memorias almacenadas en el FLEX-8600 conectado. Úselo para revisar frecuencias almacenadas de un vistazo, sintonizar rápidamente cualquier entrada o guardar el slice actual como una nueva memoria.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El Explorador de Memorias requiere una conexión activa con el radio.
- Debe haber al menos una memoria almacenada en el radio. Si no existe ninguna, el panel muestra "No memories are available yet." y la tabla no se muestra.
- La exploración de memorias debe estar habilitada para que el panel aparezca en la ventana principal. Consulte `Settings > Memory...` para configurar las opciones de memoria.

## Pasos

1. Abra el panel lateral Explorador de Memorias. Aparece acoplado en el divisor de la ventana principal cuando la exploración de memorias está habilitada.
2. Revise la tabla de memorias. Las columnas son **Frequency** (en MHz, con seis decimales) y **Name**.
3. Desplácese por la lista. Las memorias están ordenadas por frecuencia en orden ascendente. Las entradas con la misma frecuencia se ordenan por su índice interno.
4. Observe la fila resaltada. La fila con un color de fondo distintivo es la memoria cuya frecuencia está más cercana a la frecuencia sintonizada actual.
5. Para activar una memoria, haga doble clic en su fila, o selecciónela y presione Enter.
6. Para guardar el slice actual como una nueva memoria, haga clic en **Add Memory** en la parte superior del panel, inmediatamente sobre la lista de filas desplazable.

## Qué hace cada control

| Control                          | Comportamiento                                                                                              | Notas                                                                                                                          |
|----------------------------------|-------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| Tabla de memorias                | Muestra cada memoria ordenada por frecuencia; un clic o Enter activa el slice sintonizado en esa memoria.   | Columnas: Frequency, Name. La memoria más cercana a la sintonía actual se resalta con un fondo distintivo. Doble clic también sintoniza. |
| Fila resaltada                   | Marca la memoria más cercana a la frecuencia sintonizada actual. El panel se desplaza automáticamente para mantenerla visible. | Se actualiza cada vez que cambia la frecuencia sintonizada.                                                                         |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando el radio no tiene memorias cargadas.                                 | Desaparece una vez que hay memorias disponibles.                                                                               |
| Add Memory                       | Guarda el slice actual como una nueva entrada de memoria. Ubicado en la parte superior del panel, inmediatamente sobre la lista de filas desplazable. | Agregado en v26.5.1 (#2533). Reemplaza la variante anterior de insignia de letra de slice. Movido a la parte superior del panel en v26.7.4. |

## Consejos

- La columna **Name** muestra el nombre de la memoria si está definido. Si no hay nombre pero se ha asignado un grupo, se muestra el nombre del grupo en su lugar. Si no hay ninguno de los dos, la entrada aparece como "Memory" seguido de su número de índice.
- Las memorias con una frecuencia de 0 o sin definir se excluyen de la tabla por completo.
- Los nombres largos y las frecuencias que exceden el ancho de la columna se truncan con puntos suspensivos. Pase el cursor sobre cualquier celda para ver el valor completo en una información sobre herramientas.
- El botón **Add Memory** permanece visible independientemente de qué tan lejos se desplace en la tabla de memorias. Su borde superior siempre está visible; la parte inferior del botón puede quedar recortada por panadapters cortos.
- El panel del Explorador de Memorias y sus controles ahora usan el esquema de colores del tema activo. Los colores del panel, tabla, encabezado, barra de desplazamiento, etiqueta y botón están definidos por el tema en lugar de valores fijos. Los archivos de tema personalizados pueden ajustar la apariencia mediante parámetros del tema como `color.background.0`, `color.background.1`, `color.background.2`, `color.text.primary`, `color.text.label` y `color.accent.dim`.

## Relacionados

- [Memory Browser overview](overview.md)
- [Activate a memory with a single double-click](activate-a-memory-with-a-single-double-click.md)
- [Jump to the memory closest to the current frequency](jump-to-the-memory-closest-to-the-current-frequency.md)
- Guardar el slice actual como una memoria
