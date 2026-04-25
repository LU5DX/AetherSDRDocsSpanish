# Explorar las memorias almacenadas en la radio

El navegador de memorias (Memory Browser) es un panel lateral de solo lectura que lista todas las memorias almacenadas en el FLEX-8600 conectado. Úselo para ver sus frecuencias guardadas de un vistazo y para navegar a cualquier memoria directamente desde la vista del panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Memory Browser requiere una conexión de radio activa.
- Las memorias deben estar configuradas previamente en la radio. Si no se ha guardado ninguna, el panel muestra "No memories are available yet." y la tabla no aparece.

## Pasos

1. Abra `Settings > Memory...` para verificar que la exploración de memorias esté habilitada y que las memorias estén configuradas.
2. El panel Memory Browser aparece como un panel lateral dentro de la ventana principal, junto al panadapter. No es necesario realizar ninguna acción adicional para abrirlo una vez que la exploración de memorias está habilitada.
3. Desplace la tabla de memorias para encontrar la entrada deseada. La tabla lista todas las memorias con frecuencias válidas, ordenadas por frecuencia de forma ascendente. Cada fila muestra dos columnas: **Frequency** (en MHz, seis decimales) y **Name**.
4. Para identificar qué memoria está más cerca de su frecuencia sintonizada actual, busque la fila resaltada. La fila resaltada indica la memoria cuya frecuencia es la más próxima a la frecuencia VFO actual. El panel se desplaza automáticamente para mantener esa fila visible.
5. Para activar una memoria, haga doble clic en su fila o selecciónela y presione Enter.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Tabla de memorias | Lista todas las memorias almacenadas con frecuencias válidas. Haga doble clic o presione Enter para activar una fila. | Columnas: **Frequency**, **Name**. Ordenadas por frecuencia ascendente. |
| Fila resaltada | Marca la memoria más cercana a la frecuencia sintonizada actual. | Se actualiza automáticamente al sintonizar. El panel se desplaza para mantener la fila resaltada centrada. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias cargadas. | La tabla permanece oculta hasta que exista al menos una memoria con una frecuencia válida. |

## Consejos

- Si una memoria no tiene nombre, el panel recurre al nombre de su grupo. Si ninguno está definido, se muestra como "Memory" seguido de su número de índice.
- Las memorias con una frecuencia de cero o menor quedan excluidas de la tabla por completo.
- La columna **Frequency** tiene un ancho fijo de 96 píxeles. Los nombres largos en la columna **Name** se truncan con puntos suspensivos. Pase el cursor sobre una fila para ver el nombre o la frecuencia completos en un tooltip.

## Temas relacionados

- [Descripción general del Memory Browser](overview.md)
- [Activar una memoria con un solo doble clic](activate-a-memory-with-a-single-double-click.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
