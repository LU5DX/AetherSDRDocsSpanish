# Activar una memoria con un solo doble clic

El Memory Browser permite sintonizar la radio directamente en una memoria almacenada haciendo doble clic en su fila dentro de la tabla de memorias. Esto es más rápido que ingresar una frecuencia manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Memory Browser requiere una conexión activa con la radio.
- Al menos una memoria con una frecuencia válida debe estar almacenada en la radio. Si no existe ninguna, el panel muestra "No memories are available yet." y la tabla no se muestra.
- El panel lateral del Memory Browser debe estar visible en la ventana principal.

## Pasos

1. Localice el panel lateral del Memory Browser a la izquierda o a la derecha del panadapter.
2. Encuentre la memoria deseada en la tabla de memorias. Las columnas son **Frequency** y **Name**.
3. Haga doble clic en la fila correspondiente a esa memoria.

La radio se sintoniza inmediatamente en la frecuencia almacenada de esa memoria.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Tabla de memorias | Muestra todas las memorias almacenadas que tienen una frecuencia válida, ordenadas por frecuencia. Haga doble clic o presione Enter para activar una fila. |
| Fila resaltada | Indica la memoria más cercana a la frecuencia actualmente sintonizada. El panel se desplaza automáticamente para mantener esta fila visible. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias con una frecuencia válida cargada. |

## Consejos

- También puede presionar Enter para activar la fila seleccionada actualmente sin necesidad de usar el ratón.
- La fila resaltada sigue su sintonía actual de forma automática. Si sintoniza a lo largo de la banda, el resaltado se desplaza hacia la memoria almacenada más cercana a su frecuencia actual.
- Si una memoria no tiene nombre, la tabla muestra en su lugar el nombre del grupo. Si ninguno de los dos existe, muestra una etiqueta generada automáticamente, como "Memory 3".

## Solución de problemas

- **La tabla de memorias no es visible** — La radio no tiene memorias con una frecuencia válida. En su lugar aparece la etiqueta "No memories are available yet.". Agregue memorias a través de `Settings > Memory...` o directamente en la radio; luego reconecte o actualice.
- **El doble clic no hace nada** — Confirme que la radio sigue conectada. El Memory Browser requiere una conexión activa con la radio para activar memorias.

## Relacionados

- [Descripción general del Memory Browser](overview.md)
- [Explorar las memorias almacenadas en la radio](browse-the-radio-s-stored-memories.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
