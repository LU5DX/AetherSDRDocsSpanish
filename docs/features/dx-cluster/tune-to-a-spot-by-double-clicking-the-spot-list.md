# Sintonizar una baliza haciendo doble clic en la lista de balizas

La lista de balizas (Spot List) en SpotHub muestra todas las balizas activas de cada fuente conectada en una única tabla ordenable. Al hacer doble clic en cualquier fila, el slice receptor activo se sintoniza a la frecuencia de esa baliza.

## Antes de comenzar

- Al menos una fuente de balizas debe estar activa y entregando balizas (clúster DX, RBN, WSJT-X, SpotCollector, POTA o FreeDV). Consulte [Conectarse a un clúster DX](../../getting-started/setup/connect-to-a-dx-cluster.md) si aún no ha configurado ninguna.
- La configuración `IsSpotsEnabled` debe estar activada si también desea ver las balizas en el panadapter, pero no es necesaria para usar la lista de balizas al sintonizar.
- Debe haber una radio conectada y al menos un slice receptor abierto.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Spot List**.
3. Opcionalmente, marque o desmarque las casillas **Bands:** para restringir la tabla a las bandas de su interés.
4. Haga clic en el encabezado de una columna (por ejemplo, **Freq (kHz)** o **Band**) para ordenar la tabla por esa columna.
5. Haga doble clic en cualquier fila de la tabla de balizas.

El slice receptor activo se sintoniza a la frecuencia que aparece en la columna **Freq (kHz)** de esa fila.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| Casillas **Bands:** | Controles de activación por banda. Ocultar una banda elimina esas filas de la vista de la tabla; no borra las balizas. | — |
| **Clear** | Vacía la lista de balizas de todas las fuentes de forma inmediata. | — |
| Tabla de balizas | Tabla ordenable con todas las balizas activas. Columnas: Time, Freq (kHz), DX Call, Mode, Comment, Spotter, Band, Source. Haga doble clic en una fila para sintonizar. | — |

## Consejos

- La tabla se puede ordenar por cualquier columna. Ordenar por **Band** y luego revisar **Freq (kHz)** es una forma rápida de encontrar actividad en una banda específica.
- Las balizas más recientes aparecen en la parte superior de la tabla sin ordenar; la baliza más reciente de un indicativo DX determinado se agrega al inicio cuando llega.
- La tabla tiene capacidad finita de balizas. Las balizas más antiguas se eliminan desde el final a medida que llegan nuevas. Use los filtros **Bands:** para reducir el desorden si la lista se llena rápidamente.
- Use el control deslizante **Spot Lifetime:** en la pestaña **Display** (`SpotsLifetime`) para controlar cuánto tiempo permanecen visibles las balizas en el panadapter después de haberse sintonizado a otra frecuencia.

## Resolución de problemas

- **La tabla está vacía** — No hay ninguna fuente de balizas conectada o en funcionamiento. Revise las pestañas **Cluster**, **RBN**, **WSJT-X**, **SpotCollector**, **POTA** o **FreeDV** y confirme que el indicador de estado muestre Connected, Listening o Polling.
- **El doble clic no hace nada** — No hay ninguna radio conectada. Conéctese primero a una FLEX-8600 mediante `Settings > Connect to Radio...`.
- **Las balizas de una banda no son visibles** — La casilla **Bands:** correspondiente está desmarcada. Vuelva a marcarla para restaurar esa banda en la tabla.

## Temas relacionados

- [Descripción general de SpotHub](overview.md)
- [Conectarse a un clúster DX](../../getting-started/setup/connect-to-a-dx-cluster.md)
- [Conectarse a la Red de Balizas Inversas (Reverse Beacon Network)](../../getting-started/setup/connect-to-the-reverse-beacon-network.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de las balizas](tune-spot-density-position-font-size-and-lifetime.md)
- [Borrar todas las balizas del panadapter](clear-all-spots-from-the-panadapter.md)
