# Marcar la frecuencia actual como favorita

Guarde la frecuencia del slice activo en el Band Stack para poder volver a ella más tarde con un solo clic.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El panel Band Stack solo es visible cuando hay una conexión de radio activa.
- Sintonice el slice activo en la frecuencia que desea marcar como favorita.

## Pasos

1. Ubique el panel Band Stack — la franja vertical estrecha junto al panadapter.
2. Haga clic en `+` en la parte inferior del panel Band Stack.

Aparece un nuevo botón de favorito en la lista, etiquetado con la frecuencia en MHz y con un color que corresponde al segmento del plan de banda para esa frecuencia. El favorito se guarda inmediatamente en `BandStack_<serial>`, donde `<serial>` es el número de serie de su radio.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| `+` | Agrega un favorito en la frecuencia actual del slice activo. | Se guarda en `BandStack_<serial>`. |
| Botones de favorito | Haga clic para recuperar la frecuencia almacenada; haga clic derecho para eliminar. | El color refleja el segmento del plan de banda para esa frecuencia. El tooltip muestra la frecuencia completa en MHz, el modo y la antena RX. |
| ⚙ | Abre las opciones del band stack. | Las opciones incluyen "Group by band" y los intervalos de expiración automática: Off, 5 min, 15 min, 30 min, 60 min. |
| × | Elimina todos los favoritos. | El tooltip muestra "Clear all bookmarks". |

## Consejos

- Si "Group by band" está habilitado (mediante el menú ⚙), el nuevo favorito aparece bajo el encabezado de su banda en lugar de al final de una lista plana.
- El tooltip del botón de favorito muestra la frecuencia completa con seis decimales, el modo y la antena RX — coloque el cursor sobre un botón para confirmar lo que fue capturado.

## Solución de problemas

- **El botón `+` no es visible** — El panel Band Stack solo aparece cuando hay un radio conectado. Verifique la conexión mediante `Settings > Connect to Radio...`.
- **El favorito aparece en una posición inesperada** — "Group by band" está activado. El menú ⚙ indica si el agrupamiento está activo; desactívelo para restaurar el orden de inserción.

## Relacionados

- [Descripción general del Band Stack](overview.md)
- [Recuperar un favorito almacenado con un solo clic](recall-a-stored-bookmark-with-one-click.md)
- [Eliminar un favorito que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
- [Explorar visualmente las frecuencias almacenadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
