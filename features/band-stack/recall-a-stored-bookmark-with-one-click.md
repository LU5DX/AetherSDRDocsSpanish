# Recuperar un marcador guardado con un solo clic

El panel Band Stack muestra sus marcadores de frecuencia guardados junto a cada panadapter. Al hacer clic en un marcador, el panadapter sintoniza inmediatamente esa frecuencia y restaura el modo, filtro, antena y demás configuraciones del slice almacenadas.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel Band Stack solo es visible cuando hay una radio conectada.
- Debe existir al menos un marcador. Si el panel está vacío, guarde primero un marcador usando el botón `+`.

## Pasos

1. Ubique el panel Band Stack: la franja vertical estrecha de botones de colores que aparece inmediatamente junto al panadapter.
2. Encuentre el botón de marcador que muestra la frecuencia deseada. Cada botón muestra la frecuencia en MHz (por ejemplo, `14.225`). Pase el cursor sobre un botón para ver un tooltip con la frecuencia completa, el modo y la antena.
3. Haga clic en el botón de marcador. El panadapter sintoniza la frecuencia almacenada y se restauran las configuraciones del slice asociadas.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Botones de marcador | Haga clic para recuperar la frecuencia, el modo, el filtro, la antena, el AGC, el audio y la configuración de reducción de ruido almacenados. El color refleja el segmento del plan de bandas para esa frecuencia. Haga clic derecho para eliminar. | `BandStack_<serial>` |
| `+` | Agrega un nuevo marcador en la frecuencia actual del slice activo. | `BandStack_<serial>` |

## Consejos

- El color del botón indica el segmento del plan de bandas para la frecuencia almacenada. Use el color para agrupar visualmente los marcadores antes de hacer clic.
- Si tiene más marcadores de los que caben en el panel visible, desplace el panel verticalmente para mostrar los botones adicionales.

## Solución de problemas

- **El panel Band Stack no es visible** — El panel solo aparece cuando hay una radio conectada. Verifique su conexión mediante `Settings > Connect to Radio...`.
- **No aparecen botones de marcador** — Aún no se han guardado marcadores para esta radio. Use `+` para agregar el primero.

## Relacionados

- [Descripción general del Band Stack](overview.md)
- [Guardar un marcador en la frecuencia actual](bookmark-the-current-frequency.md)
- [Eliminar un marcador que ya no necesita](delete-a-bookmark-you-no-longer-need.md)
- [Explorar visualmente las frecuencias almacenadas para la banda activa](visually-scan-the-stored-frequencies-for-the-active-band.md)
