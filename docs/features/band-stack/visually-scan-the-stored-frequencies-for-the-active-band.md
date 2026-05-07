# Examine visualmente las frecuencias almacenadas para la banda activa

El panel Band Stack muestra todas sus frecuencias marcadas como una tira vertical de botones codificados por color junto al panadapter. Con un vistazo puede ver qué frecuencias tiene almacenadas, en qué segmentos de banda se encuentran y cuántos marcadores existen, sin necesidad de sintonizar ninguno de ellos.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El panel Band Stack solo es visible cuando hay un radio conectado.
- Debe tener al menos un marcador guardado. Si el panel está vacío, consulte [Bookmark the current frequency](bookmark-the-current-frequency.md).

## Pasos

1. Observe la estrecha tira vertical ubicada inmediatamente junto al panadapter. Este es el panel Band Stack.
2. Lea las etiquetas de frecuencia en los botones de marcador. Cada botón muestra la frecuencia almacenada en MHz con tres decimales (por ejemplo, `14.225`).
3. Pase el cursor sobre cualquier botón de marcador para ver su detalle completo: frecuencia con seis decimales, modo y antena RX, mostrados en una información sobre herramientas.
4. Para agrupar los marcadores por banda y facilitar el escaneo, haga clic en el botón ⚙ en la parte inferior del panel, luego haga clic en **Group by band**. El panel se redibuja con encabezados de nombre de banda que separan cada grupo. Los marcadores que no pertenecen a una banda definida aparecen bajo un encabezado **Other**.
5. Para volver a la visualización por orden de inserción, haga clic en ⚙ nuevamente y haga clic en **Group by band** para desmarcarlo.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de marcador | Muestran una frecuencia almacenada; haga clic para recuperarla, haga clic derecho para abrir un menú con **Remove**. | El color del botón refleja el segmento del plan de banda para esa frecuencia. La información sobre herramientas muestra frecuencia completa, modo y antena RX. |
| + | Agrega un nuevo marcador en la frecuencia actual del slice activo. | — |
| × | Solicita la eliminación de todos los marcadores. | La información sobre herramientas dice "Clear all bookmarks". |
| ⚙ | Abre el menú de opciones de band stack. | Consulte las opciones a continuación. |
| **Group by band** (menú ⚙) | Alterna entre visualización agrupada o por orden de inserción. Cuando está marcado, aparecen encabezados de nombre de banda y los marcadores se ordenan por banda. | Predeterminado: desmarcado. |
| **Auto-expiry** (menú ⚙) | Elimina automáticamente los marcadores más antiguos que la antigüedad seleccionada: Off, 5 min, 15 min, 30 min o 60 min. | Predeterminado: Off. |
| **Auto-save dwell** (menú ⚙) | Guarda automáticamente un marcador después de que el VFO permanezca en una frecuencia durante el tiempo seleccionado: Off, 10 sec, 30 sec o 60 sec. | Predeterminado: Off. Combine con Auto-expiry para obtener un historial rodante autopodado. |

Los datos de los marcadores se almacenan en `BandStack_<serial>`, donde `<serial>` es el número de serie de su radio.

## Consejos

- Los colores de los botones provienen del plan de banda activo. Los botones para frecuencias en diferentes segmentos (CW, phone, digital) aparecen en diferentes colores, lo que permite ver la distribución de segmentos de un vistazo sin leer cada etiqueta.
- Cuando **Group by band** está activado, puede hacer clic derecho en un encabezado de nombre de banda para borrar solo los marcadores de esa banda, usando el elemento de menú **Clear \<band name\>**.
- Si la lista de marcadores es larga, el panel se desplaza verticalmente. La barra de desplazamiento aparece en el borde derecho del panel; los botones +, × y ⚙ permanecen fijos en la parte inferior.

## Relacionados

- [Band Stack overview](overview.md)
- [Bookmark the current frequency](bookmark-the-current-frequency.md)
- [Recall a stored bookmark with one click](recall-a-stored-bookmark-with-one-click.md)
- [Delete a bookmark you no longer need](delete-a-bookmark-you-no-longer-need.md)
