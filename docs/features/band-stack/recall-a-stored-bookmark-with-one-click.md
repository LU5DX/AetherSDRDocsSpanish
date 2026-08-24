# Recupere un marcador guardado con un solo clic

El panel Band Stack le permite llevar el panadapter directamente a cualquier frecuencia guardada haciendo clic en su botón de marcador. Úselo cuando quiera volver a una frecuencia que marcó anteriormente sin tener que escribirla de nuevo.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel Band Stack solo es visible cuando hay una radio conectada.
- Ya debe existir al menos un marcador en el panel. Si el panel está vacío, agregue un marcador primero.

## Pasos

1. Localice el panel Band Stack: la franja vertical estrecha junto al panadapter en la ventana principal.
2. Encuentre el botón de marcador que muestra la frecuencia deseada. Cada botón muestra la frecuencia en MHz (por ejemplo, `14.225`). Pase el cursor sobre un botón para ver una información emergente con la frecuencia completa, el modo y la antena.
3. Haga clic en el botón de marcador. El panadapter se sintoniza inmediatamente a la frecuencia guardada.

## Qué hace cada control

| Control | Comportamiento | Ajuste persistente |
|---|---|---|
| Botones de marcador | Haga clic para sintonizar el panadapter a la frecuencia guardada; haga clic derecho para eliminar. El color refleja el segmento del band plan para esa frecuencia. | `BandStack_<serial>` |
| `+` | Agrega un nuevo marcador en la frecuencia actual del slice activo. | `BandStack_<serial>` |

## Consejos

- El color de cada botón de marcador proviene del segmento del band plan para esa frecuencia, por lo que puede identificar la banda de un vistazo sin leer la etiqueta.

## Solución de problemas

- **El panel Band Stack no es visible** — el panel solo aparece cuando hay una radio conectada. Verifique su conexión a través de `Settings > Connect to Radio...`.
- **No aparecen botones de marcador** — aún no se han guardado marcadores para esta radio. Haga clic en `+` para guardar la frecuencia actual, o consulte [Marque la frecuencia actual](bookmark-the-current-frequency.md).

## Relacionado

- [Descripción general de Band Stack](overview.md)
- [Marque la frecuencia actual](bookmark-the-current-frequency.md)
- [Elimine un marcador que ya no necesite](delete-a-bookmark-you-no-longer-need.md)
- [Examine visualmente las frecuencias guardadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
