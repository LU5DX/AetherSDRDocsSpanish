# Marcar la frecuencia actual

Guarde la frecuencia del slice activo en el panel Band Stack para poder volver a ella con un solo clic.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel Band Stack solo es visible cuando hay una radio conectada.
- Sintonice el slice activo a la frecuencia que desea guardar.

## Pasos

1. Localice el panel Band Stack: la estrecha franja vertical de botones de colores que se encuentra junto al panadapter.
2. Haga clic en `+` en la parte inferior del panel Band Stack.

El nuevo marcador aparece inmediatamente como un botón codificado por colores que muestra la frecuencia en MHz. El color del botón refleja el segmento del plan de bandas para esa frecuencia. Los marcadores se guardan automáticamente por radio y ámbito de configuración, por lo que diferentes configuraciones conservan sus propios conjuntos de marcadores.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| `+` | Agrega un marcador en la frecuencia actual del slice activo. | Un solo clic; sin diálogo de confirmación. |
| Botones de marcador | Haga clic para recuperar la frecuencia almacenada; haga clic derecho para eliminar. | El color coincide con el segmento del plan de bandas. |
| ⚙ (botón de engranaje) | Abre el menú de opciones de Band Stack. | Consulte las opciones a continuación. |
| Botón × | Borra todos los marcadores. | Información sobre herramientas: "Clear all bookmarks". |

### Opciones del menú de engranaje

| Opción | Valores | Comportamiento |
|---|---|---|
| Group by band | On / Off | Organiza los marcadores bajo encabezados de banda en lugar del orden de inserción. |
| Auto-expiry | Off, 5 min, 15 min, 30 min, 60 min | Elimina automáticamente los marcadores más antiguos que la edad seleccionada. |
| Auto-save dwell | Off, 10 sec, 30 sec, 60 sec | Marca automáticamente una frecuencia después de que el slice permanezca en ella durante la duración elegida. |

## Consejos

- Combine **Auto-save dwell** con **Auto-expiry** para mantener un historial continuo autopodado de frecuencias visitadas recientemente sin necesidad de marcar manualmente.
- Pase el cursor sobre un botón de marcador para ver la frecuencia completa en MHz, el modo y la antena RX almacenados con él.

## Relacionados

- [Descripción general de Band Stack](overview.md)
- [Recupere un marcador almacenado con un solo clic](recall-a-stored-bookmark-with-one-click.md)
- [Elimine un marcador que ya no necesite](delete-a-bookmark-you-no-longer-need.md)
- [Examine visualmente las frecuencias almacenadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
