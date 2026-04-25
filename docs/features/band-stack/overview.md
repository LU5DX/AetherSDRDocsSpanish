# Descripción general del Band Stack

El Band Stack es una franja vertical de marcadores de frecuencia que aparece junto a cada panadapter. Úselo para guardar frecuencias a las que desee volver, recuperarlas con un solo clic y visualizar de un vistazo todo lo que tiene almacenado en las bandas.

## Cómo funciona

El panel Band Stack aparece automáticamente junto a cada panadapter cuando hay un radio conectado — no es necesario abrirlo ni habilitarlo. Los marcadores de cada radio se almacenan de forma independiente bajo la clave de configuración `BandStack_<serial>`, donde `<serial>` es el número de serie del FLEX-8600 conectado.

Los marcadores se muestran como botones con la frecuencia almacenada en MHz. El color de cada botón refleja el segmento del plan de bandas al que pertenece esa frecuencia, lo que facilita distinguir las bandas de HF de un vistazo. Si tiene más marcadores de los que caben en el panel, puede desplazarse por la lista.

Cuando la opción "Group by band" está activada, los marcadores se ordenan bajo encabezados de banda (por ejemplo, 40m o 20m) en lugar de mostrarse en el orden en que fueron añadidos. Al hacer clic derecho sobre un encabezado de banda en modo agrupado, aparece la opción de eliminar todos los marcadores de esa banda de una sola vez.

## Qué hace cada control

| Control | Descripción | Notas |
|---|---|---|
| Botones de marcador | Haga clic para sintonizar el panadapter en la frecuencia almacenada. Haga clic derecho y elija "Remove" para eliminar un marcador individual. | El color corresponde al segmento del plan de bandas para esa frecuencia. El tooltip muestra la frecuencia completa en MHz, el modo y la antena de RX. |
| + | Añade un nuevo marcador en la frecuencia actual del slice activo. | — |
| × | Elimina todos los marcadores. | El tooltip indica "Clear all bookmarks". |
| ⚙ (engranaje) | Abre el menú de opciones del Band Stack. | Consulte las opciones a continuación. |

### Opciones del menú de engranaje

| Opción | Descripción | Valores válidos |
|---|---|---|
| Group by band | Cuando está marcada, los marcadores se ordenan bajo encabezados de banda. Cuando está desmarcada, los marcadores aparecen en el orden de inserción. | On / Off |
| Auto-expiry | Elimina automáticamente los marcadores más antiguos que la antigüedad seleccionada. | Off, 5 min, 15 min, 30 min, 60 min |
| Auto-save dwell | Guarda automáticamente un marcador después de que el slice activo haya permanecido en una frecuencia durante la duración elegida. | Off, 10 sec, 30 sec, 60 sec |

## Consejos

- Combine Auto-save dwell con Auto-expiry para mantener un historial rotativo y de mantenimiento automático de las frecuencias visitadas, sin necesidad de añadir marcadores manualmente.
- Cuando "Group by band" está activo, haga clic derecho sobre un encabezado de banda para eliminar todos los marcadores de esa banda sin afectar los demás.

## Temas relacionados

- [Marcar la frecuencia actual](bookmark-the-current-frequency.md)
- [Recuperar un marcador almacenado con un solo clic](recall-a-stored-bookmark-with-one-click.md)
- [Eliminar un marcador que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
- [Explorar visualmente las frecuencias almacenadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
