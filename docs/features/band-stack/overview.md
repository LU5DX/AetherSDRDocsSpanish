# Resumen de la band stack

La band stack es una franja vertical de marcadores de frecuencia que se sitúa junto a cada panadapter. Úsela para guardar frecuencias a las que desee volver, recuperarlas con un solo clic y revisar visualmente lo que tiene almacenado en las bandas.

## Cómo funciona

El panel de la band stack aparece automáticamente junto a cada panadapter cuando hay una radio conectada; no hay nada que abrir ni activar. Los marcadores de cada radio se almacenan de forma independiente bajo la clave de configuración `BandStack_<serial>`, donde `<serial>` es el número de serie de la FLEX-8600 conectada.

Los marcadores se muestran como botones con la frecuencia almacenada en MHz. El color de cada botón refleja el segmento del plan de bandas en el que cae esa frecuencia, lo que facilita distinguir las bandas de HF de un vistazo. Puede desplazarse por la lista si tiene más marcadores de los que caben en la altura del panel.

Cuando la opción "Group by band" está activada, los marcadores se ordenan bajo encabezados de banda etiquetados (por ejemplo, 40m o 20m) en lugar de mostrarse en el orden en que los agregó. Al hacer clic derecho en un encabezado de banda cuando está agrupado, tiene la opción de borrar todos los marcadores de esa banda a la vez.

## Qué hace cada control

| Control | Descripción | Notas |
|---|---|---|
| Botones de marcador | Haga clic para sintonizar el panadapter a la frecuencia almacenada. Haga clic derecho para eliminar un marcador individual. | El color coincide con el segmento del plan de bandas para esa frecuencia. La información sobre herramientas muestra la frecuencia completa en MHz, el modo y la antena de RX. |
| + | Agrega un nuevo marcador en la frecuencia actual del slice activo. | — |
| × | Borra todos los marcadores. | La información sobre herramientas dice "Clear all bookmarks". |
| ⚙ (engranaje) | Abre el menú de opciones de la band stack. | Consulte las opciones a continuación. |

### Opciones del menú de engranaje

| Opción | Descripción | Valores válidos |
|---|---|---|
| Group by band | Cuando está marcada, los marcadores se ordenan bajo encabezados de banda. Cuando no está marcada, los marcadores aparecen en orden de inserción. | On / Off |
| Auto-expiry | Elimina automáticamente los marcadores más antiguos que la edad elegida. | Off, 5 min, 15 min, 30 min, 60 min |
| Auto-save dwell | Guarda automáticamente un marcador después de que el slice activo haya permanecido en una frecuencia durante la duración elegida. | Off, 10 sec, 30 sec, 60 sec |

## Consejos

- Combine Auto-save dwell con Auto-expiry para mantener un historial continuo de las frecuencias visitadas que se depura solo, sin necesidad de marcar manualmente.
- Cuando "Group by band" está activada, haga clic derecho en un encabezado de banda para borrar todos los marcadores de esa banda sin afectar a los demás.

## Relacionados

- [Bookmark the current frequency](bookmark-the-current-frequency.md)
- [Recall a stored bookmark with one click](recall-a-stored-bookmark-with-one-click.md)
- [Delete a bookmark you no longer need](delete-a-bookmark-you-no-longer-need.md)
- [Visually scan the stored frequencies for the active band](visually-scan-the-stored-frequencies-for-the-active-band.md)
