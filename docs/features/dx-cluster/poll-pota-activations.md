# Consultar activaciones POTA

AetherSDR puede obtener periódicamente las activaciones activas de Parks on the Air (POTA) desde `api.pota.app` y mostrarlas como spots en su panadapter. Esto le permite encontrar operadores POTA activos sin necesidad de un navegador web independiente ni de un feed de cluster.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para configurar esta función.
- El acceso HTTP saliente hacia `api.pota.app` no debe estar bloqueado por un firewall.

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Haga clic en la pestaña **POTA**.
3. Revise el indicador **Server:**, que muestra `api.pota.app (HTTP polling)`. Este endpoint es fijo y no puede modificarse.
4. Establezca **Poll Interval:** con el número de segundos entre cada consulta. Este valor se guarda como `PotaPollInterval`.
5. Haga clic en **Start** para iniciar las consultas. El indicador de estado cambia a **Polling** cuando está activo. Haga clic en **Stop** para detener las consultas en cualquier momento.
6. Para cambiar el color usado para los spots POTA en el panadapter, haga clic en **Spot Color:**. Seleccione un color en el selector. Este valor se guarda como `PotaSpotColor`.
7. Para iniciar las consultas automáticamente cada vez que AetherSDR se inicia, haga clic en **Auto-start on startup** para activarlo. Este valor se guarda como `PotaAutoStart`.
8. Supervise las activaciones entrantes en la consola **POTA Activations** de la misma pestaña.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Server:** | Indicador | Muestra el endpoint de consulta fijo: `api.pota.app (HTTP polling)`. No es configurable. | — |
| **Poll Interval:** | Spinbox | Segundos entre consultas a la API de POTA. | `PotaPollInterval` |
| **Start / Stop** | Botón | Inicia o detiene las consultas POTA. | — |
| **Auto-start on startup** | Botón de alternancia | Inicia automáticamente las consultas POTA cuando AetherSDR se lanza. | `PotaAutoStart` |
| **POTA Activations** | Campo de texto | Consola de solo lectura que muestra el feed de activaciones. | — |
| **Spot Color:** | Botón | Abre un selector de color para los spots POTA en el panadapter. | `PotaSpotColor` |

## Consejos

- Los spots POTA aparecen en la pestaña unificada **Spot List** junto con spots de otras fuentes. La columna **Source** los identifica.
- Hacer doble clic en una fila de spot POTA en la Spot List sintoniza su radio en esa frecuencia. Consulte [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md).
- Si los spots no son visibles en el panadapter, confirme que el interruptor principal **Spots:** en la pestaña **Display** esté configurado en **Enabled** (`IsSpotsEnabled`).

## Solución de problemas

- **El estado permanece en Stopped después de hacer clic en Start** — La aplicación no puede alcanzar `api.pota.app`. Verifique su conexión a internet y confirme que ningún firewall o proxy esté bloqueando el tráfico HTTP saliente.
- **No aparecen spots en el panadapter a pesar del estado Polling** — Verifique que **Spots:** en la pestaña **Display** esté en **Enabled**. Compruebe también que la banda actual no esté filtrada en las casillas **Bands:** de la pestaña **Spot List**.
- **La consola POTA Activations está vacía** — Es posible que no haya activaciones POTA activas en este momento, o que la consulta aún no haya completado. Espere a que transcurra el siguiente intervalo de consulta.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
