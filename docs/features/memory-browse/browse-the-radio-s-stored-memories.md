# Navegar por las memorias almacenadas de la radio

El Navegador de Memorias es un panel lateral que enumera todas las memorias almacenadas en la FLEX-8600 conectada. Úselo para examinar frecuencias almacenadas de un vistazo, sintonizar rápidamente cualquier entrada o guardar el slice actual como una nueva memoria.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El Navegador de Memorias requiere una conexión activa con la radio.
- Al menos una memoria debe estar almacenada en la radio. Si no existe ninguna, el panel muestra "No memories are available yet." y la tabla no se visualiza.
- La navegación de memorias debe estar habilitada para que el panel aparezca en la ventana principal. Consulte `Settings > Memory...` para configurar las opciones de memoria.

## Pasos

1. Abra el panel lateral del Navegador de Memorias. Aparece acoplado en el divisor de la ventana principal cuando la navegación de memorias está habilitada.
2. Revise la tabla de memorias. Las columnas son **Frequency** (en MHz, con seis decimales) y **Name**.
3. Desplácese por la lista. Las memorias están ordenadas por frecuencia en orden ascendente. Las entradas con la misma frecuencia se ordenan por su índice interno.
4. Observe la fila resaltada. La fila resaltada con un color de fondo distintivo es la memoria cuya frecuencia está más cerca de la frecuencia sintonizada actual.
5. Para activar una memoria, haga doble clic en su fila, o selecciónela y presione Enter.
6. Para guardar el slice actual como una nueva memoria, haga clic en **Add Memory** en la parte inferior del panel.

## Qué hace cada control

| Control                          | Comportamiento                                                                                                    | Notas                                                                                                                           |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Tabla de memorias                | Muestra cada memoria ordenada por frecuencia; un clic o Enter activa el slice sintonizado en esa memoria.         | Columnas: Frequency, Name. La memoria más cercana a la sintonía actual se resalta con un fondo distintivo. El doble clic también sintoniza. |
| Fila resaltada                   | Marca la memoria más cercana a la frecuencia sintonizada actual. El panel se desplaza automáticamente para mantenerla visible. | Se actualiza cada vez que cambia la frecuencia sintonizada.                                                                     |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias cargadas.                                       | Desaparece una vez que hay memorias disponibles.                                                                                |
| Add Memory                       | Guarda el slice actual como una nueva entrada de memoria. Anclado en la parte inferior del panel, siempre visible. | Agregado en v26.5.1 (#2533). Reemplaza la variante anterior de la insignia de letra de slice.                                   |

## Consejos

- La columna **Name** muestra el nombre de la memoria si está configurado. Si no se ha asignado un nombre pero sí un grupo, se muestra el nombre del grupo. Si no se ha configurado ninguno, la entrada aparece como "Memory" seguida de su número de índice.
- Las memorias con una frecuencia de 0 o sin configurar se excluyen por completo de la tabla.
- Los nombres largos y las frecuencias que exceden el ancho de la columna se truncan con puntos suspensivos. Pase el cursor sobre cualquier celda para ver el valor completo en una información sobre herramientas.
- El botón **Add Memory** permanece visible sin importar qué tan lejos se desplace en la tabla de memorias.
- El panel del Navegador de Memorias y sus controles ahora utilizan el esquema de colores del tema activo. Los colores del panel, la tabla, el encabezado, la barra de desplazamiento, las etiquetas y los botones están definidos por el tema en lugar de valores fijos. Los archivos de temas personalizados pueden ajustar la apariencia mediante parámetros del tema como `color.background.0`, `color.background.1`, `color.background.2`, `color.text.primary`, `color.text.label` y `color.accent.dim`.

## Relacionados

- [Memory Browser overview](overview.md)
- [Activate a memory with a single double-click](activate-a-memory-with-a-single-double-click.md)
- [Jump to the memory closest to the current frequency](jump-to-the-memory-closest-to-the-current-frequency.md)
- Guardar el slice actual como una memoria
