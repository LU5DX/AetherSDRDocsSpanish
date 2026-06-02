# Saltar a la memoria más cercana a la frecuencia actual

El Explorador de Memorias resalta automáticamente la memoria almacenada cuya frecuencia esté más cerca de su sintonización actual. Esto le permite ver y desplazarse rápidamente a la memoria más relevante sin tener que buscar en toda la lista.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Explorador de Memorias requiere una conexión activa con la radio.
- La radio debe tener al menos una memoria con una frecuencia válida almacenada. Si no hay memorias cargadas, el panel muestra "No memories are available yet." y no se resalta ninguna.
- El panel lateral del Explorador de Memorias debe estar abierto. Consulte [Información general del Explorador de Memorias](overview.md) para saber cómo activarlo.

## Pasos

1. Abra el panel lateral del Explorador de Memorias. Aparece junto al panadapter en la ventana principal.
2. Sintonice la radio a cualquier frecuencia usando su método habitual (perilla VFO, clic en el panadapter o entrada directa).
3. Observe la tabla de memorias. La fila cuya frecuencia esté más cerca de la sintonización actual se resalta con un fondo distintivo.
4. El panel desplaza automáticamente la tabla para que la fila resaltada quede centrada en la vista. No requiere ninguna acción adicional.
5. Para guardar el slice actual como una nueva entrada de memoria, haga clic en **Add Memory** en la parte inferior del panel. Este botón permanece visible independientemente de la posición de desplazamiento.

## Función de cada control

| Control                          | Comportamiento                                                                                                           | Notas                                                                                                                                                            |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tabla de memorias                | Muestra cada memoria ordenada por frecuencia; un clic o Enter activa el slice sintonizado en esa memoria.                | Columnas: Frecuencia, Nombre. La memoria más cercana a la sintonización actual se resalta con un fondo distintivo. Un doble clic también sintoniza.              |
| Fila resaltada                   | Marca la memoria más cercana a la frecuencia sintonizada actual.                                                         | Los empates se resuelven por el índice de memoria: gana el índice más bajo.                                                                                      |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias válidas cargadas.                                      | Desaparece en cuanto hay al menos una memoria con una frecuencia distinta de cero disponible.                                                                    |
| Add Memory                       | Guarda el slice actual como una nueva entrada de memoria. Anclado en la parte inferior del panel, siempre visible.       | Agregado en v26.5.1 (#2533). Reemplaza la variante anterior de insignia de letra de slice. Información sobre herramientas: "Save the current slice on this panadapter as a memory." |

## Consejos

- El resaltado se actualiza cada vez que cambia la frecuencia sintonizada. Si vuelve a sintonizar, la fila resaltada se mueve a la memoria que ahora esté más cercana.
- Las memorias con una frecuencia de 0 MHz se excluyen por completo de la tabla y no se pueden seleccionar como la coincidencia más cercana.
- Si una memoria no tiene nombre, el panel muestra su nombre de grupo en su lugar. Si no se ha configurado ninguno, muestra "Memory" seguido de su número de índice.
- El botón **Add Memory** está fuera del área de desplazamiento de la tabla, por lo que permanece visible en todo momento. Esto es especialmente útil cuando la lista de memorias es larga.
- El panel del Explorador de Memorias ahora usa el tema activo para su fondo, bordes y colores de texto. Cuando cambie de tema en AetherSDR, el Explorador de Memorias se actualiza automáticamente para coincidir con el nuevo esquema de colores.

## Relacionados

- [Información general del Explorador de Memorias](overview.md)
- [Examinar las memorias almacenadas de la radio](browse-the-radio-s-stored-memories.md)
- [Activar una memoria con un solo doble clic](activate-a-memory-with-a-single-double-click.md)
