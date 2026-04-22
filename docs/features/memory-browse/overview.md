# Descripción general del Explorador de memorias

El Explorador de memorias es un panel lateral de solo lectura que lista las memorias almacenadas en su radio FLEX-8600 conectada, junto al panadapter. Resalta automáticamente la memoria más cercana a la frecuencia sintonizada en ese momento y permite saltar a cualquier memoria con un doble clic o la tecla Enter.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El Explorador de memorias requiere una conexión de radio activa.
- La radio debe tener memorias configuradas. Use `Settings > Memory...` para abrir el diálogo de configuración de memorias si no aparece ninguna.

## Cómo funciona

El Explorador de memorias se ubica como panel lateral en la ventana principal cuando la navegación por memorias está habilitada. No tiene botón en la bandeja del sistema ni modo de ventana independiente.

Cuando las memorias están cargadas, el panel las muestra en una tabla de dos columnas ordenada por frecuencia en orden ascendente. A medida que sintoniza, el panel compara continuamente su frecuencia actual con todas las memorias almacenadas y resalta la fila correspondiente a la coincidencia más cercana. El panel se desplaza automáticamente para mantener visible la fila resaltada.

Si la radio no tiene memorias cargadas, la tabla se oculta y el panel muestra en su lugar el mensaje "No memories are available yet."

Las entradas sin valor de frecuencia quedan excluidas completamente de la lista.

Cuando el nombre de una memoria no está definido, el panel recurre al nombre del grupo de esa memoria. Si ninguno de los dos está definido, muestra el número de índice de la memoria con el formato `Memory N`.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Tabla de memorias | Lista | Muestra todas las memorias con una frecuencia válida. Las columnas son **Frequency** (MHz, 6 decimales) y **Name**. Haga doble clic en una fila, o selecciónela y pulse Enter, para activar esa memoria. La tabla está ordenada por frecuencia, de forma ascendente. |
| Fila resaltada | Indicador | La fila cuya frecuencia es la más cercana a la frecuencia sintonizada actualmente queda resaltada. El panel se desplaza para mantener esta fila centrada. |
| "No memories are available yet." | Indicador | Se muestra en lugar de la tabla cuando la radio no tiene memorias con una frecuencia válida. |

El Explorador de memorias no tiene configuraciones propias persistentes.

## Consejos

- Al pasar el cursor sobre una celda **Frequency** o **Name** truncada, se muestra el valor completo en un tooltip.
- Si dos memorias están a la misma distancia de la frecuencia actual, se resalta la que tiene el número de índice menor.

## Temas relacionados

- [Explorar las memorias almacenadas en la radio](browse-the-radio-s-stored-memories.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
- [Activar una memoria con un doble clic](activate-a-memory-with-a-single-double-click.md)
