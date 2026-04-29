# Descripción general del Explorador de memorias

El Explorador de memorias es un panel lateral de solo lectura que muestra las memorias almacenadas en su radio FLEX-8600 conectada, junto al panadapter. Resalta automáticamente la memoria más cercana a la frecuencia sintonizada actualmente y le permite saltar a cualquier memoria con un doble clic o la tecla Enter.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El Explorador de memorias requiere una conexión de radio activa.
- Las memorias deben estar configuradas previamente en la radio. Abra `Settings > Memory...` para administrarlas.

## Cómo funciona

El Explorador de memorias se ubica como panel lateral dentro del divisor de la ventana principal cuando la exploración de memorias está habilitada. Recibe la lista de memorias de la radio y se mantiene sincronizado con la frecuencia actual del VFO.

La tabla muestra todas las memorias que tienen una frecuencia válida, ordenadas por frecuencia en orden ascendente. Cada vez que cambia la frecuencia sintonizada, el panel evalúa todas las memorias y resalta la fila cuya frecuencia es la más cercana a donde está sintonizado. El panel luego se desplaza automáticamente para mantener visible la fila resaltada.

Cuando no hay memorias cargadas en la radio, el panel reemplaza la tabla con el mensaje "No memories are available yet."

Activar una memoria — mediante doble clic en una fila o presionando Enter en una fila seleccionada — sintoniza la radio a la frecuencia de esa memoria.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Tabla de memorias | Muestra todas las memorias con una frecuencia válida. Las columnas son **Frequency** (MHz, seis decimales) y **Name**. Ordenadas por frecuencia. Haga doble clic o presione Enter para activar una memoria. |
| Fila resaltada | La fila cuya frecuencia es la más cercana a la frecuencia sintonizada actualmente. El panel se desplaza para mantener esta fila centrada cada vez que cambia la frecuencia sintonizada. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias cargadas. |

## Consejos

- La columna Name muestra el nombre de la memoria si hay uno definido; luego, el nombre del grupo si no existe un nombre individual; y, como alternativa, una etiqueta generada con el formato `Memory N`.
- Los nombres largos se truncan con puntos suspensivos. Coloque el cursor sobre cualquier fila para ver la frecuencia o el nombre completo en una información emergente.
- Las memorias con una frecuencia de 0 MHz o inferior quedan excluidas de la tabla por completo.

## Relacionados

- [Explorar las memorias almacenadas en la radio](browse-the-radio-s-stored-memories.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
- [Activar una memoria con un solo doble clic](activate-a-memory-with-a-single-double-click.md)
