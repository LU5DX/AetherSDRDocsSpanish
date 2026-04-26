# Explorar las memorias almacenadas en el radio

El Explorador de memorias es un panel lateral de solo lectura que lista todas las memorias almacenadas en el FLEX-8600 conectado, ordenadas por frecuencia. Úselo para ver qué memorias están disponibles y para saltar a una específica o activarla sin abandonar la vista del panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Explorador de memorias requiere una conexión de radio activa.
- Las memorias deben estar configuradas previamente en el radio. Si no existe ninguna, el panel muestra "No memories are available yet."
- La exploración de memorias debe estar habilitada para que el panel aparezca en la ventana principal. Consulte `Settings > Memory...` para configurar los ajustes de memoria.

## Pasos

1. Abra `Settings > Memory...` para confirmar que la exploración de memorias está habilitada y que el radio tiene memorias cargadas.
2. El panel del Explorador de memorias aparece como un panel lateral junto al panadapter en la ventana principal.
3. Desplace la tabla de memorias para revisar la lista. Las columnas son **Frequency** (en MHz, seis decimales) y **Name**.
4. Observe la fila resaltada. La fila con un fondo diferenciado indica la memoria más cercana a la frecuencia sintonizada actualmente.
5. Para activar una memoria, haga doble clic en su fila, o selecciónela y presione Enter.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Tabla de memorias | Lista todas las memorias almacenadas con frecuencias válidas, ordenadas por frecuencia de forma ascendente. | Columnas: Frequency, Name. Solo selección individual. |
| Fila resaltada | Marca la memoria cuya frecuencia es la más cercana a la frecuencia actual del VFO. | Se actualiza automáticamente al sintonizar. El panel se desplaza para mantener visible la fila resaltada. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando el radio no tiene memorias cargadas o todas las memorias carecen de una frecuencia válida. | Desaparece una vez que hay memorias disponibles. |

## Consejos

- La columna Name muestra el nombre de la memoria si está definido, el nombre del grupo si no hay nombre individual, o una etiqueta alternativa con el formato `Memory N` si ninguno está configurado.
- Las memorias sin frecuencia (cero o sin definir) quedan excluidas de la lista por completo.
- Si dos memorias comparten la misma frecuencia, la de índice menor se resalta como la más cercana.
- El panel tiene un tamaño fijo y no cambia de tamaño con la ventana principal.

## Relacionados

- [Descripción general del Explorador de memorias](overview.md)
- [Activar una memoria con un solo doble clic](activate-a-memory-with-a-single-double-click.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
