# Explorar visualmente las frecuencias almacenadas para la banda activa

El panel Band Stack muestra todas sus frecuencias marcadas como una franja vertical de botones con código de colores junto al panadapter. Un vistazo rápido le permite ver qué frecuencias tiene almacenadas, en qué segmentos de banda se encuentran y cuántos marcadores existen, sin necesidad de sintonizar ninguno de ellos.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel Band Stack solo es visible cuando hay una radio conectada.
- Debe existir al menos un marcador guardado. Si el panel está vacío, consulte [Marcar la frecuencia actual](bookmark-the-current-frequency.md).

## Pasos

1. Observe la estrecha franja vertical ubicada inmediatamente junto al panadapter. Ese es el panel Band Stack.
2. Lea las etiquetas de frecuencia en los botones de marcador. Cada botón muestra la frecuencia almacenada en MHz con tres decimales (por ejemplo, `14.225`).
3. Coloque el cursor sobre cualquier botón de marcador para ver sus detalles completos: frecuencia con seis decimales, modo y antena RX, mostrados en un tooltip.
4. Para agrupar los marcadores por banda y facilitar la exploración, haga clic en el botón ⚙ en la parte inferior del panel y luego haga clic en **Group by band**. El panel se redibuja con encabezados de nombre de banda que separan cada grupo. Los marcadores que no corresponden a ninguna banda definida aparecen bajo un encabezado **Other**.
5. Para volver al orden de inserción, haga clic en ⚙ nuevamente y haga clic en **Group by band** para desmarcarlo.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de marcador | Muestran una frecuencia almacenada; haga clic para recuperarla, haga clic derecho para abrir un menú con **Remove**. | El color del botón refleja el segmento del plan de banda correspondiente a esa frecuencia. El tooltip muestra la frecuencia completa, el modo y la antena RX. |
| + | Agrega un nuevo marcador en la frecuencia actual del slice activo. | — |
| × | Solicita la eliminación de todos los marcadores. | El tooltip indica "Clear all bookmarks". |
| ⚙ | Abre el menú de opciones del band stack. | Consulte las opciones a continuación. |
| **Group by band** (menú ⚙) | Alterna entre la visualización agrupada y la visualización en orden de inserción. Cuando está marcado, aparecen encabezados de nombre de banda y los marcadores se ordenan por banda. | Valor predeterminado: desmarcado. |
| **Auto-expiry** (menú ⚙) | Elimina automáticamente los marcadores más antiguos que la antigüedad elegida: Off, 5 min, 15 min, 30 min o 60 min. | Valor predeterminado: Off. |
| **Auto-save dwell** (menú ⚙) | Guarda automáticamente un marcador después de que el VFO permanece en una frecuencia durante el tiempo elegido: Off, 10 sec, 30 sec o 60 sec. | Valor predeterminado: Off. Combínelo con Auto-expiry para obtener un historial rotativo con eliminación automática. |

Los datos de los marcadores se guardan en `BandStack_<serial>`, donde `<serial>` es el número de serie de su radio.

## Consejos

- Los colores de los botones provienen del plan de banda activo. Los botones correspondientes a frecuencias en distintos segmentos (CW, telefonía, digital) aparecen en colores diferentes, lo que hace visible la distribución por segmento de un vistazo, sin necesidad de leer cada etiqueta.
- Cuando **Group by band** está activado, puede hacer clic derecho en un encabezado de nombre de banda para eliminar todos los marcadores de esa banda únicamente, usando el elemento de menú **Clear \<band name\>**.
- Si la lista de marcadores es larga, el panel se desplaza verticalmente. La barra de desplazamiento aparece en el borde derecho del panel; los botones +, × y ⚙ permanecen fijos en la parte inferior.

## Relacionado

- [Descripción general del Band Stack](overview.md)
- [Marcar la frecuencia actual](bookmark-the-current-frequency.md)
- [Recuperar un marcador almacenado con un solo clic](recall-a-stored-bookmark-with-one-click.md)
- [Eliminar un marcador que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
