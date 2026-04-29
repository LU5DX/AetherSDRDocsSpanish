# Descripción general del Band Stack

El Band Stack es una columna vertical de marcadores de frecuencia que se muestra junto a cada panadapter. Úselo para guardar frecuencias a las que desee volver, recuperarlas con un solo clic y visualizar de forma rápida todo lo que tiene almacenado en las distintas bandas.

## Cómo funciona

El panel Band Stack aparece automáticamente junto a cada panadapter cuando hay una radio conectada — no es necesario abrirlo ni habilitarlo. Los marcadores de cada radio se almacenan de forma independiente bajo la clave de configuración `BandStack_<serial>`, donde `<serial>` es el número de serie del FLEX-8600 conectado.

Los marcadores se muestran como botones con la frecuencia almacenada en MHz. El color de cada botón refleja el segmento del plan de banda al que pertenece esa frecuencia, lo que facilita distinguir las bandas HF de un vistazo. Si tiene más marcadores de los que caben en el panel, puede desplazarse por la lista.

Cuando la opción "Group by band" está activada, los marcadores se ordenan bajo encabezados de banda etiquetados (por ejemplo, 40m o 20m), en lugar de mostrarse en el orden en que fueron añadidos. Al hacer clic derecho sobre un encabezado de banda en modo agrupado, aparece la opción de eliminar todos los marcadores de esa banda a la vez.

## Qué hace cada control

| Control | Descripción | Notas |
|---|---|---|
| Botones de marcador | Haga clic para sintonizar el panadapter en la frecuencia almacenada. Haga clic derecho y elija "Remove" para eliminar un marcador individual. | El color corresponde al segmento del plan de banda para esa frecuencia. El tooltip muestra la frecuencia completa en MHz, el modo y la antena de recepción. |
| + | Añade un nuevo marcador en la frecuencia actual del slice activo. | — |
| × | Elimina todos los marcadores. | El tooltip indica "Clear all bookmarks". |
| ⚙ (engranaje) | Abre el menú de opciones del band stack. | Consulte las opciones a continuación. |

### Opciones del menú de engranaje

| Opción | Descripción | Valores válidos |
|---|---|---|
| Group by band | Cuando está activada, los marcadores se ordenan bajo encabezados de banda. Cuando está desactivada, los marcadores aparecen en el orden en que fueron insertados. | On / Off |
| Auto-expiry | Elimina automáticamente los marcadores que superen la antigüedad seleccionada. | Off, 5 min, 15 min, 30 min, 60 min |
| Auto-save dwell | Guarda automáticamente un marcador después de que el slice activo permanezca en una frecuencia durante el tiempo seleccionado. | Off, 10 sec, 30 sec, 60 sec |

## Consejos

- Combine Auto-save dwell con Auto-expiry para mantener un historial rotativo y de depuración automática de las frecuencias visitadas, sin necesidad de crear marcadores manualmente.
- Cuando "Group by band" está activado, haga clic derecho sobre un encabezado de banda para eliminar todos los marcadores de esa banda sin afectar las demás.

## Relacionado

- [Marcar la frecuencia actual](bookmark-the-current-frequency.md)
- [Recuperar un marcador almacenado con un solo clic](recall-a-stored-bookmark-with-one-click.md)
- [Eliminar un marcador que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
- [Explorar visualmente las frecuencias almacenadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
