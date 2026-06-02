# Recupere un marcador guardado con un solo clic

El panel Band Stack le permite saltar el panadapter directamente a cualquier frecuencia guardada haciendo clic en su botón de marcador. Úselo cuando desee volver a una frecuencia que haya marcado anteriormente sin tener que escribirla de nuevo.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel Band Stack solo es visible cuando hay una radio conectada.
- Debe existir al menos un marcador en el panel. Si el panel está vacío, agregue un marcador primero.

## Pasos

1. Localice el panel Band Stack (la estrecha franja vertical junto al panadapter en la ventana principal).
2. Encuentre el botón de marcador que muestra la frecuencia deseada. Cada botón muestra la frecuencia en MHz (por ejemplo, `14.225`). Pase el cursor sobre un botón para ver un tooltip con la frecuencia completa, el modo y la antena.
3. Haga clic en el botón de marcador. El panadapter sintoniza inmediatamente la frecuencia guardada.

## Función de cada control

| Control | Comportamiento | Ajuste persistente |
|---|---|---|
| Botones de marcador | Haga clic para sintonizar el panadapter en la frecuencia guardada; clic derecho para eliminar. El color refleja el segmento del plan de bandas para esa frecuencia. | `BandStack_<serial>` |
| `+` | Agrega un nuevo marcador en la frecuencia actual del slice activo. | `BandStack_<serial>` |

## Consejos

- El color de cada botón de marcador proviene del segmento del plan de bandas para esa frecuencia, por lo que puede identificar la banda de un vistazo sin leer la etiqueta.

## Solución de problemas

- **El panel Band Stack no es visible**: el panel solo aparece cuando hay una radio conectada. Verifique su conexión a través de `Settings > Connect to Radio...`.
- **No aparecen botones de marcador**: aún no se han guardado marcadores para esta radio. Haga clic en `+` para guardar la frecuencia actual, o consulte [Bookmark the current frequency](bookmark-the-current-frequency.md).

## Relacionados

- [Band Stack overview](overview.md)
- [Bookmark the current frequency](bookmark-the-current-frequency.md)
- [Delete a bookmark you no longer need](delete-a-bookmark-you-no-longer-need.md)
- [Visually scan the stored frequencies for the active band](visually-scan-the-stored-frequencies-for-the-active-band.md)
