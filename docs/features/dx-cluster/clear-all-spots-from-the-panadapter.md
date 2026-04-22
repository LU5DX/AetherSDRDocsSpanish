# Borrar todos los spots del panadapter

Elimine de una sola acción todos los spots que AetherSDR está rastreando actualmente en el panadapter. Use esta función cuando la pantalla esté saturada tras un cambio de banda o tras activar o desactivar fuentes de spots.

## Antes de comenzar

- Al menos una fuente de spots (clúster DX, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe haber entregado spots para que haya algo que borrar.
- El diálogo SpotHub debe ser accesible desde el menú (no se requiere conexión a la radio).

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Haga clic en la pestaña `Spot List`.
3. Haga clic en `Clear All Spots`.

Todos los spots se eliminan de inmediato del panadapter y de la tabla de spots. Las fuentes conectadas continúan funcionando y agregarán nuevos spots a medida que lleguen.

## Consejos

- `Clear All Spots` elimina los spots de la lista de rastreo en tiempo real para todas las fuentes a la vez. No desconecta ninguna fuente ni modifica ningún ajuste de visualización.
- Si desea eliminar los spots solo de la vista de tabla sin afectar la superposición del panadapter, use el botón `Clear` en la pestaña `Spot List`. Ese botón vacía únicamente la visualización de la tabla.
- Para evitar que aparezcan nuevos spots en el panadapter sin desconectar sus fuentes, desactive `Spots:` en la pestaña `Display` (`IsSpotsEnabled`).

## Relacionados

- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Descripción general de SpotHub](overview.md)
