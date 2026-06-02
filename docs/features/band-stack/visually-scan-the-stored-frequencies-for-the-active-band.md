# Examinar visualmente las frecuencias almacenadas para la banda activa

El panel Band Stack muestra todas las frecuencias marcadas como una tira vertical de botones codificados por color junto al panadapter. Un vistazo le permite ver de inmediato qué frecuencias tiene almacenadas, en qué segmentos de banda se encuentran y cuántos marcadores existen, sin necesidad de sintonizar ninguna de ellas.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel Band Stack solo es visible cuando hay una radio conectada.
- Debe existir al menos un marcador guardado. Si el panel está vacío, consulte [Bookmark the current frequency](bookmark-the-current-frequency.md).

## Pasos

1. Observe la estrecha tira vertical inmediatamente al lado del panadapter. Este es el panel Band Stack.
2. Lea las etiquetas de frecuencia en los botones de marcador. Cada botón muestra la frecuencia almacenada en MHz con tres decimales (por ejemplo, `14.225`).
3. Pase el cursor sobre cualquier botón de marcador para ver su detalle completo: frecuencia con seis decimales, modo y antena RX, mostrados en una información emergente.
4. Para agrupar los marcadores por banda y facilitar el examen, haga clic en el botón ⚙ en la parte inferior del panel y luego haga clic en **Group by band**. El panel se redibuja con encabezados de nombre de banda que separan cada grupo. Los marcadores que no pertenecen a una banda definida aparecen bajo un encabezado **Other**.
5. Para volver a la visualización por orden de inserción, haga clic en ⚙ nuevamente y desmarque **Group by band**.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de marcador | Muestran una frecuencia almacenada; haga clic para recordarla, haga clic derecho para abrir un menú con **Remove**. | El color del botón refleja el segmento del plan de banda para esa frecuencia. La información emergente muestra frecuencia completa, modo y antena RX. |
| + | Añade un nuevo marcador en la frecuencia actual del slice activo. | — |
| × | Solicita la eliminación de todos los marcadores. | La información emergente dice "Clear all bookmarks". |
| ⚙ | Abre el menú de opciones de band stack. | Consulte las opciones a continuación. |
| **Group by band** (menú ⚙) | Activa o desactiva la visualización agrupada frente a la visualización por orden de inserción. Cuando está marcado, aparecen encabezados de nombre de banda y los marcadores se ordenan por banda. | Predeterminado: desmarcado. |
| **Auto-expiry** (menú ⚙) | Elimina automáticamente los marcadores más antiguos que la edad seleccionada: Off, 5 min, 15 min, 30 min o 60 min. | Predeterminado: Off. |
| **Auto-save dwell** (menú ⚙) | Guarda automáticamente un marcador después de que el VFO permanezca en una frecuencia durante el tiempo seleccionado: Off, 10 sec, 30 sec o 60 sec. | Predeterminado: Off. Combínelo con Auto-expiry para obtener un historial continuo que se autopod. |

Los datos de los marcadores se guardan en `BandStack_<serial>`, donde `<serial>` es el número de serie de su radio.

## Apariencia

El panel Band Stack utiliza el tema activo de la aplicación para sus colores y estilo. Los colores de fondo, los colores de texto, los colores de la barra de desplazamiento y los bordes de los botones respetan el tema actual. No quedan colores fijos; todos los elementos visuales cambian al cambiar de tema.

## Consejos

- Los colores de los botones provienen del plan de banda activo. Los botones para frecuencias en diferentes segmentos (CW, phone, digital) aparecen en colores distintos, lo que permite ver la distribución de segmentos de un vistazo sin leer cada etiqueta.
- Cuando **Group by band** está activado, puede hacer clic derecho en un encabezado de nombre de banda para borrar todos los marcadores de esa banda únicamente, usando el elemento de menú **Clear \<band name\>**.
- Si la lista de marcadores es larga, el panel se desplaza verticalmente. La barra de desplazamiento aparece en el borde derecho del panel; los botones +, × y ⚙ permanecen fijos en la parte inferior.

## Relacionados

- [Band Stack overview](overview.md)
- [Bookmark the current frequency](bookmark-the-current-frequency.md)
- [Recall a stored bookmark with one click](recall-a-stored-bookmark-with-one-click.md)
- [Delete a bookmark you no longer need](delete-a-bookmark-you-no-longer-need.md)
