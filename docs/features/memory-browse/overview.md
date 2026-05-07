# Resumen del Explorador de Memorias

El Explorador de Memorias es un panel lateral de solo lectura que enumera las memorias almacenadas de su radio FLEX-8600 conectada, junto al panadapter. Resalta automáticamente la memoria más cercana a su frecuencia sintonizada actual y le permite saltar a cualquier memoria con un doble clic o la tecla Intro.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El Explorador de Memorias requiere una conexión de radio activa.
- Las memorias ya deben estar configuradas en la radio. Abra `Settings > Memory...` para gestionarlas.

## Cómo funciona

El Explorador de Memorias se ubica como un panel lateral dentro del divisor de la ventana principal cuando la exploración de memorias está habilitada. Recibe la lista de memorias de la radio y se mantiene sincronizado con su frecuencia VFO actual.

La tabla enumera todas las memorias que tienen una frecuencia válida, ordenadas por frecuencia en orden ascendente. Cada vez que cambia su frecuencia sintonizada, el panel evalúa todas las memorias y resalta la fila cuya frecuencia esté más cercana a donde está sintonizado. Luego, el panel se desplaza automáticamente para mantener visible esa fila resaltada.

Cuando no hay memorias cargadas en la radio, el panel reemplaza la tabla con el mensaje "No memories are available yet."

Activar una memoria — haciendo doble clic en una fila o presionando Intro en una fila seleccionada — sintoniza la radio a la frecuencia de esa memoria.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Memory table | Enumera todas las memorias con una frecuencia válida. Las columnas son **Frequency** (MHz, seis decimales) y **Name**. Ordenadas por frecuencia. Haga doble clic o presione Intro para activar una memoria. |
| Highlighted row | La fila cuya frecuencia está más cercana a la frecuencia actualmente sintonizada. El panel se desplaza para mantener esta fila centrada cada vez que cambia la frecuencia sintonizada. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias cargadas. |

## Consejos

- La columna Name muestra el nombre de la memoria si está configurado, luego el nombre del grupo si no existe un nombre individual, y luego una etiqueta generada con el formato `Memory N` como alternativa.
- Los nombres largos se truncan con puntos suspensivos. Pase el cursor sobre cualquier fila para ver la frecuencia completa o el nombre en una información sobre herramientas.
- Las memorias con una frecuencia de 0 MHz o inferior se excluyen por completo de la tabla.

## Relacionado

- [Navegar por las memorias almacenadas de la radio](browse-the-radio-s-stored-memories.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
- [Activar una memoria con un solo doble clic](activate-a-memory-with-a-single-double-click.md)
