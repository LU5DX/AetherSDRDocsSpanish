# Sintonizar una señal haciendo doble clic en la lista de spots

La pestaña Spot List en SpotHub muestra una tabla unificada y ordenable con todos los spots en vivo de cada fuente activa. Al hacer doble clic en una fila, el slice activo de su radio se sintoniza a la frecuencia de ese spot.

## Antes de comenzar

- Al menos una fuente de spots debe estar conectada y enviando spots (clúster DX, RBN, WSJT-X, SpotCollector, POTA o FreeDV).
- Su radio debe estar conectada a AetherSDR.
- `IsSpotsEnabled` debe estar activado si también desea ver los spots en el panadapter, pero no es obligatorio para la lista de spots en sí.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Spot List**.
3. Opcionalmente, use las casillas de verificación **Bands:** para ocultar las bandas que no le interesan. Desmarcar una banda elimina esas filas de la tabla.
4. Opcionalmente, haga clic en el encabezado de cualquier columna para ordenar la tabla. Las columnas son: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source.
5. Haga doble clic en la fila del spot que desea. El slice activo se sintoniza a esa frecuencia.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Casillas de verificación **Bands:** | Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m). Desmarcar una banda oculta sus spots de la tabla. | — |
| **Clear** | Vacía la lista de spots actual. | — |
| Tabla de spots | Tabla ordenable con todos los spots en vivo. Haga doble clic en una fila para sintonizar. Columnas: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source. | — |

## Consejos

- Haga clic en el encabezado de la columna **Freq (kHz)** para ordenar por frecuencia, lo que facilita encontrar spots cercanos a su frecuencia de operación actual.
- Haga clic en el encabezado de la columna **Band** para agrupar todos los spots de la misma banda.
- Los nuevos spots se agregan al inicio de la tabla. Si la lista crece demasiado, haga clic en **Clear** para eliminar todas las entradas actuales sin desconectar ninguna fuente.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Conectarse a un clúster DX](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectarse a la Red de Balizas Inversa](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
