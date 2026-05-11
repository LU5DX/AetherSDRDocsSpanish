# Ir a la memoria más cercana a la frecuencia actual

El Navegador de Memorias resalta automáticamente la memoria almacenada cuya frecuencia esté más próxima a su sintonización actual. Esto le permite ver y desplazarse rápidamente a la memoria más relevante sin tener que buscar en toda la lista.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Navegador de Memorias requiere una conexión activa con la radio.
- La radio debe tener al menos una memoria con una frecuencia válida almacenada. Si no hay memorias cargadas, el panel muestra "No memories are available yet." y no se produce ningún resaltado.
- El panel lateral del Navegador de Memorias debe estar abierto. Consulte [Resumen del Navegador de Memorias](overview.md) para saber cómo habilitarlo.

## Pasos

1. Abra el panel lateral del Navegador de Memorias. Aparece junto al panadapter en la ventana principal.
2. Sintonice la radio a cualquier frecuencia usando su método habitual (perilla VFO, clic en el panadapter o ingreso directo).
3. Observe la tabla de memorias. La fila cuya frecuencia esté más cercana a la sintonización actual se resalta con un fondo distintivo.
4. El panel desplaza automáticamente la tabla para que la fila resaltada quede centrada en la vista. No requiere ninguna acción adicional.
5. Para guardar la franja actual como una nueva entrada de memoria, haga clic en **Add Memory** en la parte inferior del panel. Este botón permanece visible sin importar la posición de desplazamiento.

## Función de cada control

| Control                           | Comportamiento                                                                                                 | Notas                                                                                                                                   |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| Tabla de memorias                 | Muestra cada memoria ordenada por frecuencia; un solo clic o Enter para activar la franja sintonizada en esa memoria. | Columnas: Frecuencia, Nombre. La memoria más cercana a la sintonización actual se resalta con un fondo distintivo. Un doble clic también sintoniza. |
| Fila resaltada                    | Marca la memoria más cercana a la frecuencia sintonizada actual.                                               | Los empates se resuelven por el índice de la memoria: gana el índice más bajo.                                                               |
| "No memories are available yet."  | Se muestra en lugar de la tabla cuando la radio no tiene memorias válidas cargadas.                            | Desaparece tan pronto como haya al menos una memoria con una frecuencia distinta de cero disponible.                                           |
| Add Memory                        | Guarda la franja actual como una nueva entrada de memoria. Anclado en la parte inferior del panel, siempre visible. | Agregado en v26.5.1 (#2533). Reemplaza la variante anterior de insignia de letra de franja. Información sobre herramientas: "Guardar la franja actual en este panadapter como una memoria." |

## Consejos

- El resaltado se actualiza cada vez que cambia la frecuencia sintonizada. Si vuelve a sintonizar, la fila resaltada se mueve a la memoria que ahora esté más cercana.
- Las memorias con una frecuencia de 0 MHz se excluyen por completo de la tabla y no se pueden seleccionar como la coincidencia más cercana.
- Si una memoria no tiene nombre, el panel muestra el nombre de su grupo. Si no se ha definido ninguno, muestra "Memory" seguido de su número de índice.
- El botón **Add Memory** está fuera del área de desplazamiento de la tabla, por lo que permanece visible en todo momento. Esto es especialmente útil cuando la lista de memorias es larga.

## Relacionados

- [Resumen del Navegador de Memorias](overview.md)
- [Examinar las memorias almacenadas de la radio](browse-the-radio-s-stored-memories.md)
- [Activar una memoria con un solo doble clic](activate-a-memory-with-a-single-double-click.md)
