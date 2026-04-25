# Sintonizar una señal haciendo doble clic en la lista de spots

La pestaña Spot List de SpotHub muestra todos los spots activos de todas las fuentes conectadas en una sola tabla ordenable. Al hacer doble clic en una fila, el VFO activo se sintoniza a la frecuencia de ese spot.

## Antes de comenzar

- Al menos una fuente de spots (DX Cluster, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe estar conectada y recibiendo spots.
- La radio debe estar conectada a AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña "Spot List".
3. Opcionalmente, use las casillas "Bands:" para filtrar la tabla por banda. Desmarque las bandas que no desee ver.
4. Haga clic en un encabezado de columna para ordenar la tabla por esa columna. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source.
5. Haga doble clic en cualquier fila de la tabla de spots. AetherSDR sintoniza el VFO activo a la frecuencia mostrada en esa fila.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Bands: | Casillas de verificación por banda. Desmarque una banda para ocultar sus spots de la tabla. | — |
| Clear | Elimina todos los spots que se muestran actualmente en la tabla. | — |
| Spot table | Tabla ordenable de todos los spots activos. Haga doble clic en una fila para sintonizar. Columnas: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source. | — |

## Consejos

- Ordene por "Freq (kHz)" para encontrar spots cercanos a su frecuencia actual.
- Ordene por "Band" para agrupar todos los spots de una banda determinada antes de hacer doble clic.
- Los spots se agregan del más reciente al más antiguo; la tabla conserva un máximo de los spots más recientes de todas las fuentes.
- Ocultar bandas con las casillas "Bands:" afecta únicamente la vista Spot List, no la superposición del panadapter.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Conectarse a un clúster DX](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectarse a la Reverse Beacon Network](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Consultar activaciones de POTA](poll-pota-activations.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
