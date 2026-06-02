# Marcar la frecuencia actual

Guarde la frecuencia del segmento activo en el panel de Band Stack para poder volver a ella con un solo clic.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel de Band Stack solo es visible cuando hay una radio conectada.
- Sintonice el segmento activo a la frecuencia que desea guardar.

## Pasos

1. Localice el panel de Band Stack, la estrecha franja vertical de botones de colores que se encuentra junto al panadapter.
2. Haga clic en `+` en la parte inferior del panel de Band Stack.

El nuevo marcador aparece inmediatamente como un botón con código de colores que muestra la frecuencia en MHz. El color del botón refleja el segmento del plan de bandas para esa frecuencia. Los marcadores se guardan automáticamente en `BandStack_<serial>`, donde `<serial>` es el número de serie de su radio.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| `+` | Agrega un marcador en la frecuencia actual del segmento activo. | Un solo clic; no aparece un cuadro de diálogo de confirmación. |
| Botones de marcador | Haga clic para recuperar la frecuencia almacenada; haga clic derecho para eliminar. | El color coincide con el segmento del plan de bandas. |
| ⚙ (botón de engranaje) | Abre el menú de opciones de Band Stack. | Consulte las opciones a continuación. |
| Botón × | Borra todos los marcadores. | Información sobre herramientas: "Clear all bookmarks". |

### Opciones del menú de engranaje

| Opción | Valores | Comportamiento |
|---|---|---|
| Group by band | On / Off | Organiza los marcadores bajo encabezados de banda en lugar de por orden de inserción. |
| Auto-expiry | Off, 5 min, 15 min, 30 min, 60 min | Elimina automáticamente los marcadores más antiguos que la edad seleccionada. |
| Auto-save dwell | Off, 10 sec, 30 sec, 60 sec | Marca automáticamente una frecuencia después de que el segmento permanezca en ella durante el tiempo elegido. |

## Consejos

- Combine **Auto-save dwell** con **Auto-expiry** para mantener un historial rotativo y autopodado de las frecuencias visitadas recientemente sin necesidad de marcarlas manualmente.
- Pase el cursor sobre un botón de marcador para ver la frecuencia completa en MHz, el modo y la antena de RX almacenados con él.

## Relacionados

- [Band Stack overview](overview.md)
- [Recall a stored bookmark with one click](recall-a-stored-bookmark-with-one-click.md)
- [Delete a bookmark you no longer need](delete-a-bookmark-you-no-longer-need.md)
- [Visually scan the stored frequencies for the active band](visually-scan-the-stored-frequencies-for-the-active-band.md)
