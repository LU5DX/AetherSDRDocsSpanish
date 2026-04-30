# Consultar activaciones POTA

AetherSDR puede descargar periódicamente las activaciones actuales de Parks on the Air (POTA) desde `api.pota.app` y mostrarlas como spots en su panadapter. Esto le permite encontrar operadores POTA activos sin necesidad de un navegador web independiente o una fuente de cluster.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para configurar esta función.
- El acceso HTTP saliente a `api.pota.app` no debe estar bloqueado por un cortafuegos.

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Haga clic en la pestaña **POTA**.
3. Revise el indicador **Server:**, que muestra `api.pota.app (HTTP polling)`. Este punto final es fijo y no se puede cambiar.
4. Establezca **Poll Interval:** en el número de segundos entre cada consulta. Este valor se persiste como `PotaPollInterval`.
5. Haga clic en **Start** para comenzar la consulta. El indicador de estado cambia a **Polling** cuando está activo. Haga clic en **Stop** para detener la consulta en cualquier momento.
6. Para cambiar el color utilizado para los spots POTA en el panadapter, haga clic en **Spot Color:**. Seleccione un color del selector. Esto se persiste como `PotaSpotColor`.
7. Para comenzar la consulta automáticamente cada vez que AetherSDR se inicia, haga clic en **Auto-start on startup** para activarlo. Esto se persiste como `PotaAutoStart`.
8. Supervise las activaciones entrantes en la consola **POTA Activations** en la misma pestaña.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Indicador | Muestra el punto final de consulta fijo: `api.pota.app (HTTP polling)`. No configurable. |
| **Poll Interval:** | Spinbox | Segundos entre consultas de la API de POTA. Se persiste como `PotaPollInterval`. |
| **Start / Stop** | Botón de presión | Inicia o detiene la consulta de POTA. |
| **Auto-start on startup** | Botón de alternancia | Inicia automáticamente la consulta de POTA cuando se lanza AetherSDR. Se persiste como `PotaAutoStart`. |
| **POTA Activations** | Campo de texto | Consola de solo lectura que muestra la fuente de activación. |
| **Spot Color:** | Botón de presión | Abre un selector de color para spots POTA en el panadapter. Se persiste como `PotaSpotColor`. |

## Controles del Reportero FreeDV (pestaña FreeDV)

Los siguientes controles aparecen en el cuadro de grupo **Station Reporting** en la pestaña **FreeDV**. Solo están presentes en compilaciones compiladas con `HAVE_WEBSOCKETS`.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Casilla de verificación | Reporta su estación al mapa público FreeDV Reporter en `qso.freedv.org` siempre que el módem RADE esté activo. Si el campo de indicativo o el cuadrado de red están en blanco cuando marca esta casilla, aparece un diálogo de advertencia y la casilla se revierte a desmarcada. Se persiste como `FreeDvAutoReport`. En Windows, también requiere una compilación compilada con `HAVE_RADE`. |
| **Callsign:** | Campo de texto | Indicativo enviado al mapa FreeDV Reporter. Se vuelve de solo lectura cuando se marca **Use radio**. Se persiste como `FreeDvMyCallsign`. |
| **Use radio** | Casilla de verificación | Rellena previamente el campo **Callsign:** desde el indicativo configurado de la radio y bloquea el campo como de solo lectura. Se actualiza automáticamente si el indicativo cambia en Radio Setup. Se persiste como `FreeDvUseRadioCallsign`. Predeterminado: habilitado. |
| **Grid Square:** | Campo de texto | Cuadrado de red Maidenhead enviado al mapa FreeDV Reporter. Se vuelve de solo lectura cuando se marca **Use GPS**. Se persiste como `FreeDvMyGrid`. |
| **Use GPS** | Casilla de verificación | Rellena previamente el campo **Grid Square:** desde el módulo GPS de la radio y bloquea el campo como de solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. Se persiste como `FreeDvUseGpsGrid`. Predeterminado: habilitado. |
| **Station Msg:** | Campo de texto | Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público FreeDV Reporter. Se persiste como `FreeDvMyMessage`. |

### Habilitar el reporte del Reportero FreeDV

Antes de habilitar **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR resuelve su indicativo y cuadrado de red efectivos en este orden:

1. Si **Use radio** está marcado y la radio tiene un indicativo configurado no vacío, se utiliza ese indicativo. De lo contrario, se utiliza el texto ingresado en **Callsign:**.
2. Si **Use GPS** se muestra y está marcado y el módulo GPS de la radio proporciona un cuadrado de red no vacío, se utiliza ese cuadrado. De lo contrario, se utiliza el texto ingresado en **Grid Square:**.

Si el indicativo resuelto o el cuadrado de red están vacíos, AetherSDR muestra una advertencia y deja la casilla desmarcada. Rellene ambos campos antes de intentar de nuevo.

## Consejos

- Los spots POTA aparecen en la pestaña **Spot List** unificada junto con spots de otras fuentes. La columna **Source** los identifica.
- Al hacer doble clic en una fila de spot POTA en la lista de spots, su radio se sintoniza en esa frecuencia. Consulte [Tune to a spot by double-clicking the spot list](tune-to-a-spot-by-double-clicking-the-spot-list.md).
- Si los spots no son visibles en el panadapter, confirme que el botón maestro **Spots:** en la pestaña **Display** esté configurado en **Enabled** (`IsSpotsEnabled`).

## Solución de problemas

- **El estado permanece en Stopped después de hacer clic en Start** — La aplicación no puede alcanzar `api.pota.app`. Compruebe su conexión a Internet y confirme que ningún cortafuegos o proxy está bloqueando HTTP saliente.
- **No aparecen spots en el panadapter a pesar del estado Polling** — Verifique que **Spots:** en la pestaña **Display** esté **Enabled**. También compruebe que la banda actual no esté filtrada en las casillas de verificación **Bands:** de la pestaña **Spot List**.
- **La consola POTA Activations está vacía** — Puede que no haya activaciones POTA activas en este momento, o la consulta aún no se ha completado. Espere a que transcurra el siguiente intervalo de consulta.
- **La casilla FreeDV Reporter se desmarca inmediatamente** — El campo **Callsign:** o **Grid Square:** está vacío. Ingrese un indicativo válido y un cuadrado de red Maidenhead (o habilite **Use radio** / **Use GPS** si la radio los proporciona) y luego marque la casilla nuevamente.

## Relacionado

- [SpotHub overview](overview.md)
- [Tune to a spot by double-clicking the spot list](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Pick colors for each spot source](pick-colors-for-each-spot-source.md)
- [Tune spot density, position, font size and lifetime](tune-spot-density-position-font-size-and-lifetime.md)
- [Clear all spots from the panadapter](clear-all-spots-from-the-panadapter.md)
