# Activar una memoria con un solo doble clic

El Memory Browser le permite sintonizar la radio directamente a una memoria almacenada con solo hacer doble clic en su fila dentro de la tabla de memorias. Esto es más rápido que ingresar una frecuencia manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Memory Browser requiere una conexión activa con la radio.
- Al menos una memoria con una frecuencia válida debe estar almacenada en la radio. Si no existe ninguna, el panel muestra "No memories are available yet." y la tabla no se despliega.
- El panel lateral del Memory Browser debe estar visible en la ventana principal.

## Pasos

1. Localice el panel lateral del Memory Browser a la izquierda o derecha del panadapter.
2. Encuentre la memoria que desea en la tabla de memorias. Las columnas son **Frequency** y **Name**.
3. Haga doble clic en la fila de esa memoria.

La radio se sintoniza inmediatamente a la frecuencia almacenada en la memoria.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Memory table | Enumera todas las memorias almacenadas que tienen una frecuencia válida, ordenadas por frecuencia. Haga doble clic o presione Enter para activar una fila. |
| Highlighted row | Indica la memoria más cercana a la frecuencia actualmente sintonizada. El panel se desplaza automáticamente para mantener visible esta fila. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias con una frecuencia válida cargadas. |

## Consejos

- También puede presionar Enter para activar la fila seleccionada sin necesidad de usar el mouse.
- La fila resaltada sigue automáticamente su sintonización actual. Si cambia de frecuencia a través de la banda, el resaltado se mueve a la memoria almacenada más cercana a su frecuencia actual.
- Si una memoria no tiene nombre, la tabla muestra el nombre de su grupo en su lugar. Si tampoco existe eso, se muestra una etiqueta generada como "Memory 3".

## Solución de problemas

- **La tabla de memorias no es visible** — La radio no tiene memorias con una frecuencia válida. En su lugar aparece la etiqueta "No memories are available yet." Agregue memorias a través de `Settings > Memory...` o directamente en la radio, luego reconéctese o actualice.
- **El doble clic no hace nada** — Confirme que la radio sigue conectada. El Memory Browser requiere una conexión activa con la radio para activar memorias.

## Relacionados

- [Memory Browser overview](overview.md)
- [Browse the radio's stored memories](browse-the-radio-s-stored-memories.md)
- [Jump to the memory closest to the current frequency](jump-to-the-memory-closest-to-the-current-frequency.md)
