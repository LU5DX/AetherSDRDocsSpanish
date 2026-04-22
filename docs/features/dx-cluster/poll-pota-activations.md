# Consultar activaciones POTA

AetherSDR puede obtener periódicamente las activaciones activas de Parks on the Air (POTA) desde `api.pota.app` y mostrarlas como spots en su panadapter. Use esta función para encontrar operadores de parques activos sin necesidad de ejecutar una aplicación separada.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para configurar el sondeo POTA.
- Su equipo debe tener acceso HTTP saliente a `api.pota.app`.
- Confirme que la superposición de spots esté habilitada (`IsSpotsEnabled` configurado en Enabled) para que los spots aparezcan en el panadapter.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **POTA**.
3. Revise el indicador **Server:** — muestra `api.pota.app (HTTP polling)` y no es editable.
4. Configure **Poll Interval:** con el número de segundos entre consultas. Este valor se guarda como `PotaPollInterval`.
5. Haga clic en **Start**. El indicador de estado cambia a **Polling**.
6. Observe la consola **POTA Activations** para ver los datos de activación entrantes.
7. Para cambiar el color de los spots POTA en el panadapter, haga clic en **Spot Color:** y elija un color. La selección se guarda como `PotaSpotColor`.
8. Para que el sondeo inicie automáticamente cada vez que AetherSDR se ejecute, haga clic en **Auto-start on startup** para activarlo. Esto se guarda como `PotaAutoStart`.
9. Para detener el sondeo, haga clic en **Stop**.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **Server:** | Indicador de solo lectura que muestra el endpoint fijo de POTA. | `api.pota.app (HTTP polling)` | — |
| **Poll Interval:** | Segundos entre consultas sucesivas a la API de POTA. | — | `PotaPollInterval` |
| **Start / Stop** | Inicia o detiene el sondeo POTA. El estado cambia entre **Polling** y **Stopped**. | — | — |
| **Auto-start on startup** | Inicia el sondeo automáticamente cuando AetherSDR se ejecuta. | — | `PotaAutoStart` |
| **POTA Activations** | Consola de solo lectura que muestra el feed de activaciones sin procesar recibido desde la API. | — | — |
| **Spot Color:** | Abre un selector de color para definir el color de los spots POTA en el panadapter. | — | `PotaSpotColor` |

## Consejos

- La consola **POTA Activations** carga las últimas 500 líneas del registro de sesión cuando se abre el diálogo SpotHub, por lo que las activaciones recientes son visibles de inmediato sin esperar la siguiente consulta.
- Haga doble clic en cualquier spot POTA en la pestaña **Spot List** para sintonizar directamente la frecuencia de esa activación.

## Solución de problemas

- **El estado permanece en Stopped después de hacer clic en Start** — Verifique que su equipo tenga conexión a internet activa y que el HTTP saliente hacia `api.pota.app` no esté bloqueado por un cortafuegos.
- **No aparecen spots en el panadapter** — Confirme que la superposición maestra de spots esté habilitada: abra la pestaña **Display** en SpotHub y verifique que **Spots:** esté configurado en Enabled (`IsSpotsEnabled`).

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
