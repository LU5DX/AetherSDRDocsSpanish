# Activar una memoria con un solo doble clic

El Memory Browser le permite sintonizar el radio directamente en una memoria almacenada haciendo doble clic en su fila dentro de la tabla de memorias. Esto es más rápido que ingresar una frecuencia manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Memory Browser requiere una conexión activa con el radio.
- Al menos una memoria con una frecuencia válida debe estar almacenada en el radio. Si no existe ninguna, el panel muestra "No memories are available yet." y la tabla no se despliega.
- El panel lateral del Memory Browser debe estar visible en la ventana principal.

## Pasos

1. Localice el panel lateral del Memory Browser a la izquierda o a la derecha del panadapter.
2. Encuentre la memoria que desea en la tabla de memorias. Las columnas son **Frequency** y **Name**.
3. Haga doble clic en la fila de esa memoria.

El radio se sintoniza de inmediato en la frecuencia almacenada de esa memoria.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Tabla de memorias | Lista todas las memorias almacenadas que tienen una frecuencia válida, ordenadas por frecuencia. Haga doble clic o presione Enter para activar una fila. |
| Fila resaltada | Indica la memoria más cercana a la frecuencia sintonizada actualmente. El panel se desplaza de forma automática para mantener esta fila visible. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando el radio no tiene memorias con una frecuencia válida cargada. |

## Consejos

- También puede presionar Enter para activar la fila seleccionada actualmente sin necesidad de usar el mouse.
- La fila resaltada sigue su sintonía actual de forma automática. Si sintoniza a lo largo de la banda, el resaltado se desplaza hacia la memoria almacenada más cercana a su frecuencia actual.
- Si una memoria no tiene nombre, la tabla muestra el nombre de su grupo en su lugar. Si ninguno de los dos existe, muestra una etiqueta generada como "Memory 3".

## Solución de problemas

- **La tabla de memorias no es visible** — El radio no tiene memorias con una frecuencia válida. En su lugar aparece la etiqueta "No memories are available yet.". Agregue memorias a través de `Settings > Memory...` o directamente en el radio, luego vuelva a conectar o actualice.
- **El doble clic no hace nada** — Confirme que el radio sigue conectado. El Memory Browser requiere una conexión activa con el radio para activar memorias.

## Relacionados

- [Descripción general del Memory Browser](overview.md)
- [Explorar las memorias almacenadas del radio](browse-the-radio-s-stored-memories.md)
- [Ir a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
