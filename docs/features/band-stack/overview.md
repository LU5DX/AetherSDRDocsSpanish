# Resumen de la Banda (Band Stack)

La Banda (Band Stack) es una franja vertical de marcadores de frecuencia que se sitúa junto a cada panorámica (panadapter). Úsela para guardar frecuencias a las que desee regresar, recuperarlas con un solo clic e inspeccionar visualmente lo que tiene almacenado en todas las bandas.

## Cómo funciona

El panel de la Banda (Band Stack) aparece automáticamente al lado de cada panorámica cuando una radio está conectada; no hay nada que abrir o habilitar. Los marcadores de cada radio se almacenan de forma independiente bajo la clave de configuración `BandStack_<serial>`, donde `<serial>` es el número de serie del FLEX-8600 conectado.

Los marcadores se muestran como botones que indican la frecuencia almacenada en MHz. El color de cada botón refleja el segmento del plan de banda en el que se encuentra esa frecuencia, lo que facilita distinguir las bandas de HF de un vistazo. Puede desplazar la lista si tiene más marcadores de los que caben en la altura del panel.

Cuando la opción "Group by band" está activada, los marcadores se ordenan bajo encabezados de banda etiquetados (por ejemplo, 40m o 20m) en lugar de mostrarse en el orden en que los agregó. Al hacer clic derecho en un encabezado de banda cuando están agrupados, tiene la opción de borrar todos los marcadores de esa banda a la vez.

## Funciones de cada control

| Control | Descripción | Notas |
|---|---|---|
| Botones de marcador | Haga clic para sintonizar la panorámica a la frecuencia almacenada. Haga clic derecho para eliminar un marcador individual. | El color coincide con el segmento del plan de banda para esa frecuencia. La información sobre herramientas muestra la frecuencia completa en MHz, el modo y la antena RX. |
| + | Agrega un nuevo marcador en la frecuencia actual del segmento activo (slice). | — |
| × | Borra todos los marcadores. | La información sobre herramientas indica "Clear all bookmarks". |
| ⚙ (engranaje) | Abre el menú de opciones de la banda (Band Stack). | Consulte las opciones a continuación. |

### Opciones del menú de engranaje

| Opción | Descripción | Valores válidos |
|---|---|---|
| Group by band | Cuando está marcada, los marcadores se ordenan bajo encabezados de banda. Cuando no está marcada, los marcadores aparecen en el orden de inserción. | On / Off |
| Auto-expiry | Elimina automáticamente los marcadores más antiguos que la antigüedad elegida. | Off, 5 min, 15 min, 30 min, 60 min |
| Auto-save dwell | Guarda automáticamente un marcador después de que el segmento activo (slice) haya permanecido en una frecuencia durante la duración elegida. | Off, 10 sec, 30 sec, 60 sec |

## Consejos

- Combine Auto-save dwell con Auto-expiry para mantener un historial rodante autogestionado de las frecuencias que ha visitado, sin necesidad de marcarlas manualmente.
- Cuando "Group by band" está activado, haga clic derecho en un encabezado de banda para borrar todos los marcadores de esa banda sin afectar a los demás.

## Relacionado

- [Marcar la frecuencia actual (Bookmark the current frequency)](bookmark-the-current-frequency.md)
- [Recuperar un marcador almacenado con un solo clic (Recall a stored bookmark with one click)](recall-a-stored-bookmark-with-one-click.md)
- [Eliminar un marcador que ya no necesita (Delete a bookmark you no longer need)](delete-a-bookmark-you-no-longer-need.md)
- [Examinar visualmente las frecuencias almacenadas de la banda activa (Visually scan the stored frequencies for the active band)](visually-scan-the-stored-frequencies-for-the-active-band.md)
