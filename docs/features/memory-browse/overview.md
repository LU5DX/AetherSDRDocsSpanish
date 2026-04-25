# Descripción general del Explorador de Memorias

El Explorador de Memorias es un panel lateral de solo lectura que muestra las memorias almacenadas en su radio junto al panadapter. Al sintonizar, resalta automáticamente la memoria más cercana a su frecuencia actual para que pueda orientarse rápidamente y saltar a un canal almacenado sin abandonar la pantalla principal.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- La radio debe tener al menos una memoria configurada. Use `Settings > Memory...` para administrar las memorias.

## Cómo funciona

El Explorador de Memorias aparece como un panel lateral en la ventana principal. Cuando hay memorias presentes, el panel muestra una tabla de dos columnas con todas las memorias almacenadas que tienen una frecuencia válida. La tabla está ordenada por frecuencia, de menor a mayor.

Al sintonizar la radio, el panel recalcula continuamente qué memoria es la más cercana a la frecuencia activa y resalta esa fila. El panel se desplaza automáticamente para mantener la fila resaltada visible.

Cuando no hay memorias cargadas, el panel muestra el mensaje "No memories are available yet." en lugar de la tabla.

**Activar una memoria:** Haga doble clic en cualquier fila, o seleccione una fila y presione Enter, para activar esa memoria en la radio.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Tabla de memorias | Lista todas las memorias con una frecuencia válida. Columnas: Frequency (MHz, 6 decimales) y Name. Selección simple; solo lectura. Haga doble clic o presione Enter en una fila para activar esa memoria. |
| Fila resaltada | Indica la memoria cuya frecuencia es la más cercana a la frecuencia sintonizada actualmente. El panel se desplaza para mantener esta fila centrada. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias con una frecuencia válida. Desaparece automáticamente una vez que hay memorias disponibles. |

**Visualización del nombre:** La columna Name muestra el nombre de la memoria si está definido, el nombre del grupo si no hay nombre de memoria, o "Memory N" (donde N es el índice de la memoria) si ninguno está definido.

## Consejos

- La fila resaltada se actualiza al sintonizar — no es necesario realizar ninguna acción para refrescarla.
- Si dos memorias están a la misma distancia de la frecuencia actual, se resalta la que tiene el índice de memoria más bajo.
- Las memorias con una frecuencia de 0 o sin frecuencia definida se excluyen completamente de la tabla.

## Relacionado

- [Explorar las memorias almacenadas de la radio](browse-the-radio-s-stored-memories.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
- [Activar una memoria con un solo doble clic](activate-a-memory-with-a-single-double-click.md)
