# Activar una memoria con un solo doble clic

El Explorador de Memorias le permite sintonizar el radio directamente a una memoria almacenada haciendo doble clic en su fila en la tabla de memorias. Esto es más rápido que ingresar una frecuencia manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Explorador de Memorias requiere una conexión activa con el radio.
- Debe tener al menos una memoria con una frecuencia válida almacenada en el radio. Si no existe ninguna, el panel muestra "No memories are available yet." y la tabla no se muestra.
- El panel lateral del Explorador de Memorias debe estar visible en la ventana principal.

## Pasos

1. Ubique el panel lateral del Explorador de Memorias a la izquierda o derecha del panadapter.
2. Encuentre la memoria que desea en la tabla de memorias. Las columnas son **Frequency** y **Name**.
3. Haga doble clic en la fila de esa memoria.

El radio se sintoniza inmediatamente a la frecuencia almacenada en la memoria.

## Qué hace cada control

| Control                          | Comportamiento                                                                                                           | Notas                                                                                                                          |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| Tabla de memorias                | Muestra cada memoria ordenada por frecuencia; un solo clic o Enter activa esa memoria en el slice sintonizado.           | Columnas: Frequency, Name. La memoria más cercana a la sintonía actual se resalta con un fondo distintivo. El doble clic también sintoniza. |
| Fila resaltada                   | Indica la memoria más cercana a la frecuencia sintonizada actualmente. El panel se desplaza automáticamente para mantener esta fila visible. |                                                                                                                                |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando el radio no tiene memorias cargadas con una frecuencia válida.                    |                                                                                                                                |
| Add Memory                       | Guarda el slice actual como una nueva entrada de memoria. Anclado en la parte inferior del panel, siempre visible.       | Añadido en v26.5.1 (#2533). Reemplaza la variante anterior de insignia de letra de slice. Haga clic para guardar el slice actual en este panadapter como memoria. |

## Consejos

- También puede presionar Enter para activar la fila seleccionada actualmente sin necesidad de usar el ratón.
- La fila resaltada sigue su sintonía actual automáticamente. Si se desplaza por la banda, el resaltado se mueve a la memoria almacenada más cercana a su frecuencia actual.
- Si una memoria no tiene nombre, la tabla muestra el nombre de su grupo en su lugar. Si tampoco existe un grupo, muestra una etiqueta generada como "Memory 3".
- El botón **Add Memory** permanece visible incluso cuando se desplaza por una larga lista de memorias porque está anclado en la parte inferior del panel, fuera del área de desplazamiento de la tabla.

## Solución de problemas

- **La tabla de memorias no es visible** — El radio no tiene memorias con una frecuencia válida. Aparece la etiqueta "No memories are available yet.". Agregue memorias a través de `Settings > Memory...` o directamente en el radio, luego reconéctese o actualice.
- **El doble clic no hace nada** — Confirme que el radio sigue conectado. El Explorador de Memorias requiere una conexión activa con el radio para activar memorias.

## Relacionado

- [Memory Browser overview](overview.md)
- [Browse the radio's stored memories](browse-the-radio-s-stored-memories.md)
- [Jump to the memory closest to the current frequency](jump-to-the-memory-closest-to-the-current-frequency.md)
