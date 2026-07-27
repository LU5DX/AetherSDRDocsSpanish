# Resumen del Navegador de Memorias

El Navegador de Memorias es un panel lateral de solo lectura que lista las memorias almacenadas de su radio FLEX-8600 conectado, junto al panadapter. Resalta automáticamente la memoria más cercana a su frecuencia sintonizada actual y le permite saltar a cualquier memoria con un doble clic o la tecla Enter.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El Navegador de Memorias requiere una conexión activa con el radio.
- Las memorias deben estar configuradas previamente en el radio. Abra `Settings > Memory...` para gestionarlas.

## Cómo funciona

El Navegador de Memorias se sitúa como un panel lateral dentro del divisor de la ventana principal cuando la navegación de memorias está habilitada. Recibe la lista de memorias del radio y se mantiene sincronizado con su frecuencia VFO actual.

La tabla muestra todas las memorias que tienen una frecuencia válida, ordenadas por frecuencia en orden ascendente. Cada vez que cambia su frecuencia sintonizada, el panel evalúa todas las memorias y resalta la fila cuya frecuencia está más cercana a donde está sintonizado. Luego, el panel se desplaza automáticamente para mantener visible esa fila resaltada.

Cuando no hay memorias cargadas en el radio, el panel reemplaza la tabla con el mensaje "No memories are available yet."

Activar una memoria — ya sea haciendo doble clic en una fila o presionando Enter en una fila seleccionada — sintoniza el radio a la frecuencia de esa memoria.

## Función de cada control

| Control                          | Descripción                                                                                                                                            | Notas                                                                                                                          |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| Tabla de memorias                | Muestra cada memoria ordenada por frecuencia; un solo clic o Enter activa el slice sintonizado en esa memoria.                                         | Columnas: Frequency, Name. La memoria más cercana a la sintonía actual se resalta con un fondo distintivo. Doble clic también sintoniza. |
| Fila resaltada                   | La fila cuya frecuencia está más cercana a la frecuencia sintonizada actualmente. El panel se desplaza para mantener esta fila centrada cuando cambia la frecuencia sintonizada. |                                                                                                                                |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando el radio no tiene memorias cargadas.                                                                            |                                                                                                                                |
| Add Memory                       | Guarda el slice actual como una nueva entrada de memoria. Se ubica en la parte superior del panel, inmediatamente encima de las filas desplazables.     | Agregado en v26.5.1 (#2533). Reemplaza la variante anterior de la insignia de letra de slice. En v26.7.4, se movió de anclado inferior a la parte superior del panel. |

## Consejos

- La columna Name muestra el nombre de la memoria si está configurado, luego el nombre del grupo si no hay un nombre individual, y luego una etiqueta generada con el formato `Memory N` como alternativa.
- Los nombres largos se truncan con puntos suspensivos. Pase el cursor sobre cualquier fila para ver la frecuencia o el nombre completo en una información emergente.
- Las memorias con frecuencia de 0 MHz o inferior se excluyen por completo de la tabla.
- Haga clic en **Add Memory** para guardar el slice activo en el panadapter actual como una nueva entrada de memoria. El botón se encuentra en la parte superior del panel, inmediatamente encima de las filas desplazables. Si el panadapter es corto, la parte inferior del cajón puede estar recortada, pero la parte superior del botón permanece visible.
- El panel y sus controles ahora utilizan un estilo sensible al tema, adaptando sus colores (fondos, bordes, texto, acentos, barras de desplazamiento) al tema de AetherSDR que haya seleccionado. Anteriormente, estos colores estaban codificados de forma fija.

## Relacionados

- [Browse the radio's stored memories](browse-the-radio-s-stored-memories.md)
- [Jump to the memory closest to the current frequency](jump-to-the-memory-closest-to-the-current-frequency.md)
- [Activate a memory with a single double-click](activate-a-memory-with-a-single-double-click.md)
