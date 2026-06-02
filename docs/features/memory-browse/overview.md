# Resumen del explorador de memorias

El explorador de memorias es un panel lateral de solo lectura que muestra las memorias almacenadas de su radio FLEX-8600 conectada junto al panadapter. Resalta automáticamente la memoria más cercana a su frecuencia sintonizada actual y le permite saltar a cualquier memoria con un doble clic o la tecla Enter.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El explorador de memorias requiere una conexión activa con la radio.
- Las memorias ya deben estar configuradas en la radio. Abra `Settings > Memory...` para administrarlas.

## Cómo funciona

El explorador de memorias se ubica como un panel lateral dentro del divisor de la ventana principal cuando la exploración de memorias está habilitada. Recibe la lista de memorias de la radio y se mantiene sincronizado con su frecuencia VFO actual.

La tabla muestra todas las memorias que tienen una frecuencia válida, ordenadas por frecuencia en orden ascendente. Cada vez que cambia su frecuencia sintonizada, el panel evalúa todas las memorias y resalta la fila cuya frecuencia está más cerca de donde está sintonizado. Luego, el panel se desplaza automáticamente para mantener visible esa fila resaltada.

Cuando no hay memorias cargadas en la radio, el panel reemplaza la tabla con el mensaje "No memories are available yet."

Activar una memoria — haciendo doble clic en una fila o presionando Enter en una fila seleccionada — sintoniza la radio a la frecuencia de esa memoria.

## Función de cada control

| Control                          | Descripción                                                                                                                                            | Notas                                                                                                                           |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Tabla de memorias                | Muestra cada memoria ordenada por frecuencia; un clic o Enter para activar el slice sintonizado en esa memoria.                                         | Columnas: Frequency, Name. La memoria más cercana a la sintonización actual se resalta con un fondo distintivo. El doble clic también sintoniza. |
| Fila resaltada                   | La fila cuya frecuencia está más cerca de la frecuencia sintonizada actual. El panel se desplaza para mantener esta fila centrada cada vez que cambia la frecuencia sintonizada. |                                                                                                                                 |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias cargadas.                                                                            |                                                                                                                                 |
| Add Memory                       | Guarda el slice actual como una nueva entrada de memoria. Anclado en la parte inferior del panel, siempre visible.                                      | Añadido en v26.5.1 (#2533). Reemplaza la variante anterior de insignia de letra de slice.                                      |

## Consejos

- La columna Name muestra el nombre de la memoria si está configurado, luego el nombre del grupo si no existe un nombre individual, y luego una etiqueta generada con el formato `Memory N` como alternativa.
- Los nombres largos se truncan con puntos suspensivos. Pase el cursor sobre cualquier fila para ver la frecuencia o el nombre completo en una información sobre herramientas.
- Las memorias con una frecuencia de 0 MHz o inferior se excluyen por completo de la tabla.
- Haga clic en **Add Memory** para guardar el slice activo en el panadapter actual como una nueva entrada de memoria. El botón permanece visible en la parte inferior del panel independientemente de la posición de desplazamiento.
- El panel y sus controles ahora usan un estilo que reconoce el tema, adaptando sus colores (fondos, bordes, texto, acentos, barras de desplazamiento) al tema de AetherSDR que haya seleccionado. Anteriormente, estos colores estaban codificados de forma fija.

## Relacionado

- [Browse the radio's stored memories](browse-the-radio-s-stored-memories.md)
- [Jump to the memory closest to the current frequency](jump-to-the-memory-closest-to-the-current-frequency.md)
- [Activate a memory with a single double-click](activate-a-memory-with-a-single-double-click.md)
