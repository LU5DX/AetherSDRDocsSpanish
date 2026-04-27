# Descripción general del Explorador de Memorias

El Explorador de Memorias es un panel lateral de solo lectura que muestra las memorias almacenadas de su radio FLEX-8600 conectado, junto al panadapter. Resalta automáticamente la memoria más cercana a la frecuencia sintonizada en ese momento y permite saltar a cualquier memoria con un doble clic o la tecla Enter.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El Explorador de Memorias requiere una conexión de radio activa.
- Las memorias deben estar configuradas previamente en el radio. Abra `Settings > Memory...` para administrarlas.

## Cómo funciona

El Explorador de Memorias se ubica como panel lateral dentro del divisor de la ventana principal cuando la exploración de memorias está habilitada. Recibe la lista de memorias del radio y se mantiene sincronizado con la frecuencia actual del VFO.

La tabla muestra todas las memorias que tienen una frecuencia válida, ordenadas por frecuencia en orden ascendente. Cada vez que cambia la frecuencia sintonizada, el panel evalúa todas las memorias y resalta la fila cuya frecuencia es la más cercana a donde está sintonizado. El panel se desplaza automáticamente para mantener visible la fila resaltada.

Cuando no hay memorias cargadas en el radio, el panel reemplaza la tabla con el mensaje "No memories are available yet."

Activar una memoria — con un doble clic en una fila o presionando Enter sobre una fila seleccionada — sintoniza el radio a la frecuencia de esa memoria.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Tabla de memorias | Muestra todas las memorias con una frecuencia válida. Las columnas son **Frequency** (MHz, seis decimales) y **Name**. Ordenadas por frecuencia. Haga doble clic o presione Enter para activar una memoria. |
| Fila resaltada | La fila cuya frecuencia es la más cercana a la frecuencia sintonizada en ese momento. El panel se desplaza para mantener esta fila centrada cada vez que cambia la frecuencia sintonizada. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando el radio no tiene memorias cargadas. |

## Consejos

- La columna Name muestra el nombre de la memoria si se ha definido uno; luego el nombre del grupo si no existe un nombre individual; y finalmente una etiqueta generada con el formato `Memory N` como último recurso.
- Los nombres largos se truncan con puntos suspensivos. Pase el cursor sobre cualquier fila para ver la frecuencia o el nombre completo en un tooltip.
- Las memorias con una frecuencia de 0 MHz o inferior quedan excluidas de la tabla por completo.

## Relacionados

- [Explorar las memorias almacenadas del radio](browse-the-radio-s-stored-memories.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
- [Activar una memoria con un doble clic](activate-a-memory-with-a-single-double-click.md)
