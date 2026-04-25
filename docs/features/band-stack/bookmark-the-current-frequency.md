# Guardar la frecuencia actual como marcador

Guarde la frecuencia del slice activo en el panel Band Stack para volver a ella con un solo clic.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel Band Stack solo es visible cuando hay una radio conectada.
- Sintonice el slice activo en la frecuencia que desea guardar.

## Pasos

1. Localice el panel Band Stack — la franja vertical estrecha de botones de colores ubicada junto al panadapter.
2. Haga clic en `+` en la parte inferior del panel Band Stack.

El nuevo marcador aparece inmediatamente como un botón codificado por color que muestra la frecuencia en MHz. El color del botón refleja el segmento del plan de banda correspondiente a esa frecuencia. Los marcadores se guardan automáticamente en `BandStack_<serial>`, donde `<serial>` es el número de serie de su radio.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| `+` | Agrega un marcador en la frecuencia actual del slice activo. | Un solo clic; no muestra diálogo de confirmación. |
| Botones de marcador | Haga clic para recuperar la frecuencia almacenada; haga clic derecho para eliminar. | El color coincide con el segmento del plan de banda. |
| ⚙ (botón de engranaje) | Abre el menú de opciones del Band Stack. | Consulte las opciones a continuación. |
| Botón × | Elimina todos los marcadores. | Información emergente: "Clear all bookmarks". |

### Opciones del menú de engranaje

| Opción | Valores | Comportamiento |
|---|---|---|
| Group by band | On / Off | Organiza los marcadores bajo encabezados de banda en lugar de por orden de inserción. |
| Auto-expiry | Off, 5 min, 15 min, 30 min, 60 min | Elimina automáticamente los marcadores más antiguos que la duración seleccionada. |
| Auto-save dwell | Off, 10 sec, 30 sec, 60 sec | Guarda automáticamente como marcador una frecuencia cuando el slice permanece en ella durante el tiempo elegido. |

## Consejos

- Combine **Auto-save dwell** con **Auto-expiry** para mantener un historial rotativo con autopoda de las frecuencias visitadas recientemente, sin necesidad de crear marcadores manualmente.
- Pase el cursor sobre un botón de marcador para ver la frecuencia completa en MHz, el modo y la antena RX almacenados en él.

## Relacionado

- [Descripción general del Band Stack](overview.md)
- [Recuperar un marcador almacenado con un solo clic](recall-a-stored-bookmark-with-one-click.md)
- [Eliminar un marcador que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
- [Explorar visualmente las frecuencias almacenadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
