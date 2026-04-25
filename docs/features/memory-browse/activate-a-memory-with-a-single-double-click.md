# Activar una memoria con un solo doble clic

El Memory Browser le permite sintonizar su radio directamente en una memoria almacenada haciendo doble clic en su fila dentro de la tabla de memorias. Esto es más rápido que ingresar una frecuencia manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel Memory Browser debe estar abierto y visible en la ventana principal.
- Al menos una memoria con una frecuencia válida debe estar almacenada en la radio. Si no hay ninguna cargada, el panel muestra "No memories are available yet." en lugar de la tabla.

## Pasos

1. Ubique el panel lateral Memory Browser junto al panadapter.
2. Encuentre la memoria que desea en la tabla de memorias. Las columnas son **Frequency** y **Name**. La fila resaltada con un color de fondo distintivo es la memoria más cercana a su frecuencia de sintonía actual.
3. Haga doble clic en cualquier fila de la tabla de memorias para activar esa memoria. Su radio se sintoniza inmediatamente en la frecuencia de esa memoria.

Alternativamente, haga clic en una fila para seleccionarla y luego presione **Enter** para activarla.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Tabla de memorias | Lista todas las memorias almacenadas que tienen una frecuencia válida, ordenadas por frecuencia. Haga doble clic o presione Enter en una fila para activarla. |
| Fila resaltada | Indica la memoria cuya frecuencia es la más cercana a la frecuencia de sintonía actual. El panel se desplaza automáticamente para mantener esta fila visible. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias cargadas. |

## Consejos

- La fila resaltada se actualiza automáticamente mientras sintoniza. Si está explorando cerca de un segmento de banda en particular, la memoria más cercana ya estará marcada antes de que haga doble clic.
- Si una memoria no tiene nombre, el panel muestra en su lugar el nombre del grupo. Si ninguno está definido, se utiliza una etiqueta basada en el índice de la memoria.

## Relacionado

- [Descripción general del Memory Browser](overview.md)
- [Explorar las memorias almacenadas en la radio](browse-the-radio-s-stored-memories.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
