# Sintonizar una escucha haciendo doble clic en la lista de escuchas

La pestaña Spot List de SpotHub muestra todas las escuchas activas de todas las fuentes habilitadas en una única tabla ordenable. Al hacer doble clic en una fila, el VFO activo se sintoniza a la frecuencia de esa escucha.

## Antes de comenzar

- Al menos una fuente de escuchas (DX Cluster, RBN, WSJT-X, SpotCollector, POTA o FreeDV) debe estar conectada y recibiendo escuchas.
- El equipo debe estar conectado a AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña "Spot List".
3. Opcionalmente, utilice las casillas "Bands:" para filtrar la tabla por banda. Desmarque las bandas que no desee ver.
4. Haga clic en el encabezado de una columna para ordenar la tabla por esa columna. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source.
5. Haga doble clic en cualquier fila de la tabla de escuchas. AetherSDR sintoniza el VFO activo a la frecuencia que aparece en esa fila.

## Función de cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Bands: | Casillas de verificación por banda. Desmarque una banda para ocultar sus escuchas en la tabla. | — |
| Clear | Elimina todas las escuchas que se muestran actualmente en la tabla. | — |
| Spot table | Tabla ordenable con todas las escuchas activas. Haga doble clic en una fila para sintonizar. Columnas: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source. | — |

## Consejos

- Ordene por "Freq (kHz)" para encontrar escuchas cercanas a su frecuencia actual.
- Ordene por "Band" para agrupar todas las escuchas de una banda determinada antes de hacer doble clic.
- Las escuchas se agregan de más reciente a más antigua; la tabla conserva como máximo las escuchas más recientes de todas las fuentes.
- Ocultar bandas con las casillas "Bands:" afecta únicamente a la vista Spot List, no a la superposición del panadapter.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Conectarse a un clúster DX](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectarse a la Reverse Beacon Network](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas propias](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Consultar activaciones POTA](poll-pota-activations.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de las escuchas](tune-spot-density-position-font-size-and-lifetime.md)
