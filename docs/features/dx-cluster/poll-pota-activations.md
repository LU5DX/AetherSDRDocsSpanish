# Consultar activaciones POTA

AetherSDR puede obtener periódicamente las activaciones actuales de Parks on the Air desde `api.pota.app` y mostrarlas como spots en el panadapter. Esto le permite ver los operadores POTA activos sin consultar manualmente el sitio web de POTA.

## Antes de comenzar

- AetherSDR debe tener una conexión a internet activa para alcanzar `api.pota.app`.
- Los spots deben estar habilitados. Abra `Settings > SpotHub...`, vaya a la pestaña **Display** y confirme que **Spots:** esté configurado en Enabled.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **POTA**.
3. Revise el indicador **Server:** — muestra `api.pota.app (HTTP polling)` y es fijo; no se requiere ingresar ningún servidor.
4. Configure **Poll Interval:** con el número de segundos entre consultas. Este valor se guarda como `PotaPollInterval`.
5. Haga clic en **Start** para iniciar las consultas. El indicador de estado cambia a **Polling**.
6. Observe la consola **POTA Activations** para ver los datos de activación entrantes.
7. Para cambiar el color usado para los spots POTA en el panadapter, haga clic en **Spot Color:** para abrir el selector de color. El color elegido se guarda como `PotaSpotColor`.
8. Para que las consultas POTA se inicien automáticamente cada vez que AetherSDR se ejecuta, habilite **Auto-start on startup**. Esto se guarda como `PotaAutoStart`.

## Qué hace cada control

| Control | Descripción | Configuración guardada |
|---|---|---|
| **Server:** | Indicador de solo lectura que muestra el endpoint fijo (`api.pota.app (HTTP polling)`). | — |
| **Poll Interval:** | Segundos entre consultas HTTP a la API de POTA. | `PotaPollInterval` |
| **Start / Stop** | Inicia o detiene las consultas POTA. El estado muestra **Polling** cuando está activo y **Stopped** cuando está inactivo. | — |
| **Auto-start on startup** | Inicia automáticamente las consultas POTA cuando AetherSDR se ejecuta. | `PotaAutoStart` |
| **POTA Activations** | Consola de solo lectura que muestra el feed de activaciones sin procesar a medida que llega. | — |
| **Spot Color:** | Abre un selector de color para el color usado al renderizar los spots POTA en el panadapter. | `PotaSpotColor` |

## Consejos

- Los spots POTA aparecen en la pestaña unificada **Spot List** junto con spots de otras fuentes. La columna **Source** los identifica.
- Hacer doble clic en una fila de la pestaña **Spot List** sintoniza su radio a la frecuencia de ese spot. Consulte [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md).
- Para filtrar llamadas CQ de POTA que llegan mediante decodificaciones FT8 de WSJT-X en lugar de consultas HTTP, consulte [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md).

## Solución de problemas

- **El estado permanece en Stopped después de hacer clic en Start** — Confirme que AetherSDR tiene acceso a internet saliente hacia `api.pota.app` en el puerto 443. Un firewall o proxy puede estar bloqueando la conexión.
- **No aparecen spots en el panadapter a pesar del estado Polling** — Verifique que la capa de spots principal esté habilitada: pestaña **Display**, **Spots:** debe estar en Enabled (`IsSpotsEnabled`). Confirme también que **Spot Lifetime:** en la pestaña **Display** esté configurado con un valor suficientemente alto para que los spots permanezcan visibles entre consultas.
- **Los spots aparecen pero con el color incorrecto** — Haga clic en **Spot Color:** en la pestaña **POTA** para reasignar el color. Si **Override Colors:** está habilitado en la pestaña **Display**, anula todos los colores por fuente de forma global.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Seleccionar colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
