# Sintonizar una señal haciendo doble clic en la lista de spots

La pestaña Spot List en SpotHub muestra una tabla unificada y ordenable con todos los spots en vivo de cada fuente conectada. Al hacer doble clic en una fila, el receptor activo se sintoniza a la frecuencia de ese spot.

## Antes de comenzar

- Al menos una fuente de spots debe estar activa y entregando spots (clúster DX, RBN, WSJT-X, SpotCollector, POTA o FreeDV). Consulte las páginas relacionadas a continuación para obtener instrucciones de configuración.
- La radio debe estar conectada a AetherSDR.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `Spot List`.
3. Opcionalmente, use las casillas `Bands:` para limitar qué bandas aparecen en la tabla. Desmarque las bandas que no desee ver.
4. Haga clic en el encabezado de una columna para ordenar la tabla — por ejemplo, haga clic en `Freq (kHz)` para ordenar por frecuencia o en `DX Call` para ordenar alfabéticamente.
5. Localice el spot que desea trabajar.
6. Haga doble clic en esa fila. AetherSDR sintoniza el receptor activo a la frecuencia que aparece en la columna `Freq (kHz)`.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Casillas `Bands:` | Activadores por banda. Desmarcar una banda oculta sus spots en la tabla. No afecta la visualización en el panadapter. | — |
| `Clear` | Vacía la lista de spots de inmediato. | — |
| Tabla de spots | Tabla ordenable con columnas: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source. Haga doble clic en cualquier fila para sintonizar. | — |

## Consejos

- Ordene por `Time` (descendente) para ver los spots recibidos más recientemente en la parte superior. Los spots nuevos se agregan al inicio, por lo que el orden predeterminado ya los coloca primero.
- Ordene por `Band` para comparar la actividad en distintas bandas antes de decidir dónde operar.
- Si espera ver spots pero la tabla está vacía, verifique que la banda en cuestión no esté filtrada por las casillas `Bands:`.

## Solución de problemas

- **Hacer doble clic en una fila no produce ningún efecto** — Verifique que la radio esté conectada. La acción de sintonía requiere una conexión de radio activa, aunque SpotHub en sí no la requiera.
- **La tabla está vacía a pesar de tener una fuente conectada** — Confirme que la fuente aparezca como Connected, Listening o Polling en su pestaña. También confirme que las casillas de la banda correspondiente estén marcadas.
- **La columna de banda de un spot aparece en blanco** — La frecuencia del spot cae fuera de los límites reconocidos de las bandas de radioaficionados. La fila sigue apareciendo y hacer doble clic en ella igualmente sintoniza.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Conectarse a un clúster DX](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectarse a la Reverse Beacon Network](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas hacia mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Consultar activaciones de POTA](poll-pota-activations.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
