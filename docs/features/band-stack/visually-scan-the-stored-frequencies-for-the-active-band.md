# Examine visualmente las frecuencias almacenadas para la banda activa

El panel Band Stack muestra todas sus frecuencias marcadas como una franja vertical de botones codificados por color junto al panadapter. Una mirada le permite ver de un vistazo qué frecuencias tiene almacenadas, en qué segmentos de banda se encuentran y cuántos marcadores existen, sin necesidad de sintonizar ninguno de ellos.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel Band Stack solo es visible cuando hay una radio conectada.
- Debe existir al menos un marcador guardado. Si el panel está vacío, consulte [Marque la frecuencia actual](bookmark-the-current-frequency.md).

## Pasos

1. Observe la franja vertical estrecha inmediatamente al lado del panadapter. Este es el panel Band Stack.
2. Lea las etiquetas de frecuencia en los botones de marcador. Cada botón muestra la frecuencia almacenada en MHz con tres decimales (por ejemplo, `14.225`).
3. Pase el cursor sobre cualquier botón de marcador para ver su detalle completo: frecuencia con seis decimales, modo y antena de RX, mostrados en una información sobre herramientas (tooltip).
4. Para agrupar los marcadores por banda y facilitar el escaneo, haga clic en el botón ⚙ en la parte inferior del panel y luego haga clic en **Group by band**. El panel se redibuja con encabezados de nombre de banda que separan cada grupo. Los marcadores que no pertenecen a ninguna banda definida aparecen bajo un encabezado **Other**.
5. Para volver a la visualización en orden de inserción, haga clic en ⚙ nuevamente y haga clic en **Group by band** para desmarcarlo.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de marcador | Muestran una frecuencia almacenada; haga clic para sintonizar, clic derecho para eliminar. | El color del botón refleja el segmento del plan de bandas para esa frecuencia. La información sobre herramientas muestra la frecuencia completa, el modo y la antena de RX. |
| + | Agrega un nuevo marcador en la frecuencia actual del slice activo. | — |
| × | Solicita la eliminación de todos los marcadores. | La información sobre herramientas indica "Clear all bookmarks". |
| ⚙ | Abre el menú de opciones del band stack. | Consulte las opciones a continuación. |
| **Group by band** (menú ⚙) | Alterna entre visualización agrupada y en orden de inserción. Cuando está marcado, aparecen encabezados con nombres de banda y los marcadores se ordenan por banda. | Predeterminado: desmarcado. |
| **Auto-expiry** (menú ⚙) | Elimina automáticamente los marcadores más antiguos que la edad seleccionada: Off, 5 min, 15 min, 30 min o 60 min. | Predeterminado: Off. |
| **Auto-save dwell** (menú ⚙) | Guarda automáticamente un marcador después de que el VFO permanezca en una frecuencia durante el tiempo seleccionado: Off, 10 sec, 30 sec o 60 sec. | Predeterminado: Off. Combine con Auto-expiry para obtener un historial rotativo autolimpiante. |

Los datos de los marcadores se conservan por radio. Los marcadores almacenados están limitados al ámbito de configuración de la radio activa, que incluye el número de serie de la radio, por lo que los marcadores de diferentes radios nunca se mezclan, incluso si usa la misma instalación de AetherSDR con varias unidades FLEX-8600.

## Apariencia

El panel Band Stack utiliza el tema de aplicación activo para sus colores y estilo. Los colores de fondo, los colores de texto, los colores de la barra de desplazamiento y los bordes de los botones respetan el tema actual. No quedan colores fijos; todos los elementos visuales cambian al alternar entre temas.

## Consejos

- Los colores de los botones provienen del plan de bandas activo. Los botones para frecuencias en diferentes segmentos (CW, phone, digital) aparecen en diferentes colores, lo que hace visible la distribución de segmentos de un vistazo sin leer cada etiqueta.
- Cuando **Group by band** está activado, puede hacer clic derecho en un encabezado de nombre de banda para eliminar solo los marcadores de esa banda, usando el elemento de menú **Clear \<band name\>**.
- Si la lista de marcadores es larga, el panel se desplaza verticalmente. La barra de desplazamiento aparece en el borde derecho del panel; los botones + , × y ⚙ permanecen fijos en la parte inferior.

## Relacionados

- [Descripción general de Band Stack](overview.md)
- [Marque la frecuencia actual](bookmark-the-current-frequency.md)
- [Recupere un marcador almacenado con un clic](recall-a-stored-bookmark-with-one-click.md)
- [Elimine un marcador que ya no necesite](delete-a-bookmark-you-no-longer-need.md)
