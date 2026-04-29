# Eliminar todos los spots del panadapter

Elimine de una sola acción todos los spots que se muestran actualmente en el panadapter. Use esta función cuando la pantalla esté saturada y desee comenzar de cero sin desconectar ninguna fuente de spots.

## Antes de comenzar

- Al menos una fuente de spots (clúster DX, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe haber entregado spots; de lo contrario, no hay nada que eliminar.
- Los spots continúan llegando desde cualquier fuente conectada o en ejecución inmediatamente después de la limpieza, por lo que las fuentes permanecen activas.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `Display`.
3. Haga clic en `Clear All Spots`.

Todos los spots se eliminan al instante del panadapter y de la lista de spots. Las fuentes conectadas no se desconectan y continuarán entregando nuevos spots.

## Consejos

- Para eliminar spots banda por banda en lugar de todos a la vez, use la pestaña `Spot List`. Marque o desmarque bandas individuales en `Bands:` para ocultar los spots de una banda específica sin descartarlos de forma permanente.
- Para limpiar únicamente la tabla de la lista de spots, vaya a la pestaña `Spot List` y haga clic en `Clear`. Esto vacía la visualización de la tabla, pero el efecto sobre la superposición del panadapter sigue los mismos datos de spots en tiempo real.
- Si los spots reaparecen de inmediato y desea una pantalla limpia por más tiempo, reduzca el valor de `Spot Lifetime:` en la pestaña `Display` (`SpotsLifetime`), o desconecte la fuente correspondiente antes de limpiar.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
