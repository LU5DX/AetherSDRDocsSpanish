# Descripción general del Explorador de Memorias

El Explorador de Memorias es un panel lateral de solo lectura que muestra las memorias almacenadas en su radio junto al panadapter. Resalta automáticamente la memoria más cercana a la frecuencia sintonizada actualmente, para que pueda orientarse con rapidez y saltar a un canal cercano.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel no aparece ni se llena sin una conexión de radio activa.
- Debe haber al menos una memoria almacenada en la radio. Si no hay ninguna cargada, el panel muestra "No memories are available yet." en lugar de la tabla.

## Cómo funciona

El panel del Explorador de Memorias se encuentra dentro del divisor de la ventana principal, a un lado del panadapter. Cuando la exploración de memorias está habilitada, el panel se abre automáticamente dentro de ese diseño — no es una ventana flotante.

El panel rastrea continuamente la frecuencia sintonizada actual. Al sintonizar, el panel encuentra la memoria almacenada cuya frecuencia es la más cercana a su VFO y resalta esa fila. La tabla también se desplaza para mantener la fila resaltada visible, por lo que no es necesario desplazarse manualmente.

Las memorias se listan en orden de frecuencia ascendente. Cada fila muestra dos columnas:

| Columna | Contenido |
|---|---|
| Frequency | Frecuencia de la memoria en MHz, mostrada con seis decimales. |
| Name | Nombre de la memoria si está definido; si no, el nombre del grupo; si no, "Memory _N_" donde _N_ es el índice de la memoria. |

Cuando la radio no reporta memorias, la tabla se oculta y se muestra en su lugar la etiqueta "No memories are available yet."

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Memory table | Lista todas las memorias almacenadas con frecuencias válidas, ordenadas por frecuencia. Haga doble clic en una fila, o selecciónela y presione Enter, para activar esa memoria. |
| Highlighted row | La fila cuya frecuencia es la más cercana a la frecuencia sintonizada actualmente. El panel se desplaza automáticamente para mantener esta fila centrada. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias cargadas. Desaparece en cuanto las memorias están disponibles. |

## Consejos

- Si dos memorias están a la misma distancia de la frecuencia actual, se resalta la que tiene el índice de memoria más bajo.
- Las memorias con una frecuencia de 0 se excluyen completamente de la tabla y nunca se resaltan.
- Los nombres largos que superan el ancho de la columna se truncan con puntos suspensivos. Coloque el cursor sobre una celda para ver el texto completo en un tooltip.

## Relacionados

- [Explorar las memorias almacenadas de la radio](browse-the-radio-s-stored-memories.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
- [Activar una memoria con un doble clic](activate-a-memory-with-a-single-double-click.md)
