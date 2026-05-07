# Resumen de la Pila de Bandas

La Pila de Bandas (Band Stack) es una franja vertical de marcadores de frecuencia que se sitúa junto a cada panadapter. Sirve para guardar frecuencias a las que desea volver, recuperarlas con un solo clic e inspeccionar visualmente lo que tiene almacenado en las bandas.

## Cómo funciona

El panel de la Pila de Bandas aparece automáticamente junto a cada panadapter cuando hay una radio conectada; no hay nada que abrir o activar. Los marcadores de cada radio se almacenan de forma independiente bajo la clave de configuración `BandStack_<serial>`, donde `<serial>` es el número de serie de la FLEX-8600 conectada.

Los marcadores se muestran como botones que indican la frecuencia almacenada en MHz. El color de cada botón refleja el segmento del plan de bandas en el que se encuentra esa frecuencia, lo que facilita distinguir las bandas de HF de un vistazo. Puede desplazar la lista si tiene más marcadores de los que caben en la altura del panel.

Cuando la opción "Agrupar por banda" está activada, los marcadores se ordenan bajo encabezados de banda con etiquetas (por ejemplo, 40m o 20m), en lugar de mostrarse en el orden en que los agregó. Al hacer clic derecho en un encabezado de banda cuando está agrupado, tiene la opción de borrar todos los marcadores de esa banda de una sola vez.

## Para qué sirve cada control

| Control | Descripción | Notas |
|---|---|---|
| Botones de marcador | Haga clic para sintonizar el panadapter a la frecuencia almacenada. Haga clic derecho y elija "Remove" para eliminar un marcador individual. | El color coincide con el segmento del plan de bandas para esa frecuencia. La información sobre herramientas (tooltip) muestra la frecuencia completa en MHz, el modo y la antena de RX. |
| + | Agrega un nuevo marcador en la frecuencia actual del slice activo. | — |
| × | Borra todos los marcadores. | La información sobre herramientas muestra "Clear all bookmarks". |
| ⚙ (engranaje) | Abre el menú de opciones de la pila de bandas. | Consulte las opciones a continuación. |

### Opciones del menú de engranaje

| Opción | Descripción | Valores válidos |
|---|---|---|
| Group by band | Cuando está marcada, los marcadores se ordenan bajo encabezados de banda. Cuando no está marcada, los marcadores aparecen en el orden de inserción. | On / Off |
| Auto-expiry | Elimina automáticamente los marcadores más antiguos que la antigüedad seleccionada. | Off, 5 min, 15 min, 30 min, 60 min |
| Auto-save dwell | Guarda automáticamente un marcador después de que el slice activo haya permanecido en una frecuencia durante la duración seleccionada. | Off, 10 sec, 30 sec, 60 sec |

## Consejos

- Combine Auto-save dwell con Auto-expiry para mantener un historial móvil autopodado de las frecuencias que ha visitado, sin necesidad de marcar manualmente.
- Cuando "Group by band" está activada, haga clic derecho en un encabezado de banda para borrar todos los marcadores de esa banda sin afectar a los demás.

## Temas relacionados

- [Bookmark the current frequency](bookmark-the-current-frequency.md)
- [Recall a stored bookmark with one click](recall-a-stored-bookmark-with-one-click.md)
- [Delete a bookmark you no longer need](delete-a-bookmark-you-no-longer-need.md)
- [Visually scan the stored frequencies for the active band](visually-scan-the-stored-frequencies-for-the-active-band.md)
