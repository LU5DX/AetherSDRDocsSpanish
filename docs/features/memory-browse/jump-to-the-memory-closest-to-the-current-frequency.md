# Saltar a la memoria más cercana a la frecuencia actual

El Navegador de Memorias resalta automáticamente la memoria cuya frecuencia es la más cercana a su sintonía actual. Esta página explica cómo interpretar ese resaltado y desplazarse hasta él.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Navegador de Memorias requiere una conexión de radio activa.
- Debe haber al menos una memoria con una frecuencia válida almacenada en la radio. Si no hay ninguna, el panel muestra "No memories are available yet." en lugar de la tabla.
- El panel lateral del Navegador de Memorias debe estar visible en la ventana principal.

## Pasos

1. Sintonice el VFO de su radio a cualquier frecuencia utilizando su método habitual.
2. Observe el panel del Navegador de Memorias a un lado del panadapter. La tabla de memorias se actualiza automáticamente.
3. Localice la fila resaltada. La fila resaltada corresponde a la memoria cuya frecuencia almacenada es la más cercana a su frecuencia sintonizada actual. Si dos memorias están a igual distancia, se resalta la que tiene el índice de memoria menor.
4. El panel se desplaza automáticamente para centrar la fila resaltada en la vista. No se requiere ninguna acción adicional.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Tabla de memorias | Lista todas las memorias con frecuencias válidas, ordenadas por frecuencia. Columnas: Frecuencia (MHz, seis decimales), Nombre. |
| Fila resaltada | Indica la memoria más cercana a la frecuencia sintonizada actual. Se actualiza cada vez que cambia la sintonía. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias con frecuencias válidas cargadas. |

## Consejos

- El resaltado se actualiza cada vez que cambia su frecuencia sintonizada, por lo que puede usarlo como indicador en tiempo real de la memoria más cercana mientras gira el VFO.
- Los nombres de las memorias se obtienen primero del campo de nombre de la memoria, luego del campo de grupo y, por último, de una etiqueta de reserva con la forma `Memory N`. Los nombres largos se truncan con puntos suspensivos; coloque el cursor sobre una fila para ver el nombre completo en una información emergente.
- Para actuar sobre la memoria resaltada, haga doble clic en su fila o presione Enter para activarla.

## Relacionados

- [Descripción general del Navegador de Memorias](overview.md)
- [Activar una memoria con un solo doble clic](activate-a-memory-with-a-single-double-click.md)
- [Explorar las memorias almacenadas en la radio](browse-the-radio-s-stored-memories.md)
