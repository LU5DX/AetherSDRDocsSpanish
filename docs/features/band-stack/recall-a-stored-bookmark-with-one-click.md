# Recuperar un marcador guardado con un solo clic

El panel Band Stack le permite saltar el panadapter directamente a cualquier frecuencia guardada haciendo clic en su botón de marcador. Úselo cuando desee volver a una frecuencia que marcó anteriormente sin necesidad de escribirla de nuevo.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel Band Stack solo es visible cuando hay una radio conectada.
- Debe existir al menos un marcador en el panel. Si el panel está vacío, agregue un marcador primero.

## Pasos

1. Localice el panel Band Stack — la franja vertical estrecha junto al panadapter en la ventana principal.
2. Encuentre el botón de marcador que muestra la frecuencia deseada. Cada botón muestra la frecuencia en MHz (por ejemplo, `14.225`). Pase el cursor sobre un botón para ver un tooltip con la frecuencia completa, el modo y la antena.
3. Haga clic en el botón de marcador. El panadapter sintoniza la frecuencia guardada de inmediato.

## Qué hace cada control

| Control | Comportamiento | Ajuste persistente |
|---|---|---|
| Botones de marcador | Haga clic para sintonizar el panadapter a la frecuencia guardada. El color refleja el segmento del plan de banda para esa frecuencia. | `BandStack_<serial>` |
| `+` | Agrega un nuevo marcador en la frecuencia actual del slice activo. | `BandStack_<serial>` |
| × | Borra todos los marcadores. | `BandStack_<serial>` |
| ⚙ | Abre las opciones del band stack: Group by band, Auto-expiry (Off, 5 min, 15 min, 30 min, 60 min), Auto-save dwell (Off, 10 sec, 30 sec, 60 sec). | `BandStack_<serial>` |

## Consejos

- Si tiene muchos marcadores, active **Group by band** mediante el menú ⚙. Los marcadores se ordenan entonces bajo encabezados de banda, lo que facilita encontrar una frecuencia específica a simple vista.
- El color de cada botón de marcador proviene del segmento del plan de banda para esa frecuencia, por lo que puede identificar la banda de un vistazo sin leer la etiqueta.

## Solución de problemas

- **El panel Band Stack no es visible** — el panel aparece solo cuando hay una radio conectada. Verifique su conexión mediante `Settings > Connect to Radio...`.
- **No aparecen botones de marcador** — aún no se han guardado marcadores para esta radio. Haga clic en `+` para guardar la frecuencia actual, o consulte [Marcar la frecuencia actual](bookmark-the-current-frequency.md).

## Relacionados

- [Descripción general del Band Stack](overview.md)
- [Marcar la frecuencia actual](bookmark-the-current-frequency.md)
- [Eliminar un marcador que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
- [Explorar visualmente las frecuencias guardadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
