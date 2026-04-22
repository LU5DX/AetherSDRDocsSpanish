# Consultar activaciones POTA

AetherSDR puede obtener periódicamente las activaciones actuales de Parks on the Air (POTA) desde `api.pota.app` y mostrarlas como spots en el panadapter. Esto permite ver los operadores POTA activos en todas las bandas sin necesidad de un navegador o aplicación independiente.

## Antes de comenzar

- AetherSDR debe tener una conexión a internet activa para alcanzar `api.pota.app`.
- La visualización de spots en el panadapter requiere que `IsSpotsEnabled` esté activado. Verifique que en `Settings > SpotHub...` > pestaña Display > **Spots:** esté configurado como **Enabled**.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **POTA**.
3. Revise el indicador **Server:** — muestra `api.pota.app (HTTP polling)` y no puede modificarse.
4. Configure **Poll Interval:** con el número de segundos entre consultas (almacenado como `PotaPollInterval`).
5. Haga clic en **Start**. El indicador de estado cambia a **Polling**.
6. Observe la consola **POTA Activations** para ver los datos de activación entrantes. Los spots aparecen en el panadapter una vez recibidos.
7. Para elegir un color de spot, haga clic en **Spot Color:** y seleccione un color en el cuadro de diálogo (almacenado como `PotaSpotColor`).
8. Para iniciar la consulta automáticamente cada vez que AetherSDR se inicie, haga clic en **Auto-start on startup** para activarlo (almacenado como `PotaAutoStart`).

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Indicador de solo lectura que muestra el punto de acceso fijo `api.pota.app (HTTP polling)`. | — |
| **Poll Interval:** | Segundos entre consultas HTTP a `api.pota.app`. | `PotaPollInterval` |
| **Start / Stop** | Inicia o detiene la consulta POTA. El estado muestra **Polling** cuando está activo y **Stopped** cuando está inactivo. | — |
| **Auto-start on startup** | Cuando está activo, la consulta comienza automáticamente al iniciar. | `PotaAutoStart` |
| **POTA Activations** | Consola de solo lectura que muestra el flujo de activaciones sin procesar recibido en cada consulta. | — |
| **Spot Color:** | Abre un selector de color para los spots POTA en el panadapter. | `PotaSpotColor` |

## Consejos

- Si desea sintonizar directamente una activación POTA, cambie a la pestaña **Spot List** y haga doble clic en la fila. Consulte [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md).
- Los spots POTA respetan la configuración global de visualización de spots (duración, posición, tamaño de fuente, apilamiento). Ajuste esos parámetros en la pestaña **Display** o consulte [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md).

## Solución de problemas

- **El estado permanece en Stopped después de hacer clic en Start** — Verifique que su sistema tenga una conexión a internet funcional y pueda alcanzar `api.pota.app` en el puerto 443.
- **No aparecen spots en el panadapter a pesar del estado Polling** — Compruebe que **Spots:** en la pestaña **Display** esté configurado como **Enabled** (`IsSpotsEnabled`). Confirme también que ninguna estación POTA activa quede fuera del rango visible actualmente en el panadapter.
- **Los spots desaparecen rápidamente** — El control deslizante global **Spot Lifetime:** en la pestaña **Display** determina cuánto tiempo permanece visible cada spot. Auméntelo para mantener los spots POTA en pantalla por más tiempo (`SpotsLifetime`).

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Seleccionar colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
