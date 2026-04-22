# Activar una memoria con un solo doble clic

El Memory Browser le permite sintonizar la radio directamente en una memoria almacenada haciendo doble clic en su fila dentro de la tabla de memorias. Esto evita tener que ingresar una frecuencia manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Memory Browser requiere una conexión de radio activa.
- El panel del Memory Browser debe estar visible. Aparece como panel lateral en la ventana principal cuando la navegación de memorias está habilitada.
- Debe haber al menos una memoria con una frecuencia válida almacenada en la radio. Si no hay ninguna cargada, el panel muestra "No memories are available yet." en lugar de la tabla.

## Pasos

1. Localice el panel lateral del Memory Browser junto al panadapter.
2. Encuentre la memoria que desea en la tabla de memorias. Las columnas muestran Frequency y Name.
3. Haga doble clic en la fila de esa memoria.

La radio se sintoniza inmediatamente en la frecuencia de esa memoria.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Tabla de memorias | Muestra todas las memorias almacenadas con frecuencias válidas, ordenadas por frecuencia. Haga doble clic o presione Enter para activar una fila. |
| Fila resaltada | Indica la memoria más cercana a la frecuencia sintonizada actualmente. El panel se desplaza de forma automática para mantener esta fila visible. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias cargadas. |

## Consejos

- También puede presionar Enter para activar la fila seleccionada actualmente si prefiere la navegación por teclado.
- La fila resaltada sigue su VFO a medida que sintoniza, de modo que la memoria más cercana siempre es fácil de ubicar.
- Si una memoria no tiene nombre, la tabla recurre al nombre de su grupo, o muestra un marcador de posición como "Memory 1".

## Relacionados

- [Descripción general del Memory Browser](overview.md)
- [Explorar las memorias almacenadas en la radio](browse-the-radio-s-stored-memories.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
