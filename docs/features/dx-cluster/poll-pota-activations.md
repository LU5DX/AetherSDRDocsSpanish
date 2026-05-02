# Consultar activaciones de POTA

AetherSDR puede obtener periódicamente las activaciones actuales de Parks on the Air (POTA) desde `api.pota.app` y mostrarlas como spots en su panadapter. Esto permite encontrar operadores de POTA activos sin necesidad de un navegador web independiente ni un feed de clúster.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión de radio para configurar esta función.
- El acceso HTTP saliente a `api.pota.app` no debe estar bloqueado por un cortafuegos.

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Haga clic en la pestaña **POTA**.
3. Revise el indicador **Server:**, que muestra `api.pota.app (HTTP polling)`. Este endpoint es fijo y no se puede cambiar.
4. Establezca **Poll Interval:** con el número de segundos entre cada consulta. Este valor se persiste como `PotaPollInterval`.
5. Haga clic en **Start** para iniciar la consulta. El indicador de estado cambia a **Polling** cuando está activo. Haga clic en **Stop** para detener la consulta en cualquier momento.
6. Para cambiar el color usado para los spots de POTA en el panadapter, haga clic en **Spot Color:**. Seleccione un color en el selector. Este valor se persiste como `PotaSpotColor`.
7. Para iniciar la consulta automáticamente cada vez que AetherSDR se inicia, haga clic en **Auto-start on startup** para activarlo. Este valor se persiste como `PotaAutoStart`.
8. Supervise las activaciones entrantes en la consola **POTA Activations** de la misma pestaña.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Indicador | Muestra el endpoint de consulta fijo: `api.pota.app (HTTP polling)`. No es configurable. |
| **Poll Interval:** | Spinbox | Segundos entre consultas a la API de POTA. Se persiste como `PotaPollInterval`. |
| **Start / Stop** | Botón | Inicia o detiene la consulta de POTA. |
| **Auto-start on startup** | Botón de alternancia | Inicia automáticamente la consulta de POTA al lanzar AetherSDR. Se persiste como `PotaAutoStart`. |
| **POTA Activations** | Campo de texto | Consola de solo lectura que muestra el feed de activaciones. |
| **Spot Color:** | Botón | Abre un selector de color para los spots de POTA en el panadapter. Se persiste como `PotaSpotColor`. |

## Controles de FreeDV Reporter (pestaña FreeDV)

Los siguientes controles aparecen en el grupo **Station Reporting** de la pestaña **FreeDV**. Solo están presentes en compilaciones generadas con `HAVE_WEBSOCKETS`.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Casilla de verificación | Reporta su estación al mapa público de FreeDV Reporter en `qso.freedv.org` cuando el módem RADE está activo. Si el campo de indicativo o cuadrícula está vacío al marcar esta casilla, aparece un diálogo de advertencia y la casilla vuelve a desmarcarse. Se persiste como `FreeDvAutoReport`. En Windows, también requiere una compilación con `HAVE_RADE`. |
| **Callsign:** | Campo de texto | Indicativo enviado al mapa de FreeDV Reporter. Se vuelve de solo lectura cuando **Use radio** está marcado. Se persiste como `FreeDvMyCallsign`. |
| **Use radio** | Casilla de verificación | Rellena previamente el campo **Callsign:** con el indicativo configurado en la radio y bloquea el campo como solo lectura. Se actualiza automáticamente si el indicativo cambia en Radio Setup. Se persiste como `FreeDvUseRadioCallsign`. Valor predeterminado: activado. |
| **Grid Square:** | Campo de texto | Cuadrícula Maidenhead enviada al mapa de FreeDV Reporter. Se vuelve de solo lectura cuando **Use GPS** está marcado. Se persiste como `FreeDvMyGrid`. |
| **Use GPS** | Casilla de verificación | Rellena previamente el campo **Grid Square:** con el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que disponen de hardware GPS. Se persiste como `FreeDvUseGpsGrid`. Valor predeterminado: activado. |
| **Station Msg:** | Campo de texto | Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público de FreeDV Reporter. Se persiste como `FreeDvMyMessage`. |

### Activar el reporte en FreeDV Reporter

Antes de activar **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR resuelve su indicativo y cuadrícula efectivos en este orden:

1. Si **Use radio** está marcado y la radio tiene un indicativo no vacío configurado, se utiliza ese indicativo. De lo contrario, se utiliza el texto ingresado en **Callsign:**.
2. Si **Use GPS** se muestra y está marcado, y el módulo GPS de la radio proporciona una cuadrícula no vacía, se utiliza esa cuadrícula. De lo contrario, se utiliza el texto ingresado en **Grid Square:**.

Si el indicativo o la cuadrícula resueltos están vacíos, AetherSDR muestra una advertencia y deja la casilla desmarcada. Complete ambos campos antes de intentarlo de nuevo.

## Cambio en el valor predeterminado de Auto Mode

A partir de la v0.9.5.1, el botón de alternancia **Auto Mode:** en la pestaña **Display** tiene como valor predeterminado **Enabled**. El ajuste se persiste como `SpotAutoSwitchMode`. Si anteriormente dejó este valor en su predeterminado, estará activo tras una instalación nueva. Las instalaciones existentes conservan el último valor guardado.

## Consejos

- Los spots de POTA aparecen en la pestaña unificada **Spot List** junto con spots de otras fuentes. La columna **Source** los identifica.
- Hacer doble clic en una fila de spot de POTA en la Spot List sintoniza su radio a esa frecuencia. Consulte [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md).
- Si los spots no son visibles en el panadapter, confirme que el control principal **Spots:** en la pestaña **Display** esté configurado como **Enabled** (`IsSpotsEnabled`).

## Solución de problemas

- **El estado permanece en Stopped después de hacer clic en Start** — La aplicación no puede alcanzar `api.pota.app`. Verifique su conexión a internet y confirme que ningún cortafuegos o proxy esté bloqueando el HTTP saliente.
- **No aparecen spots en el panadapter a pesar del estado Polling** — Verifique que **Spots:** en la pestaña **Display** esté **Enabled**. Compruebe también que la banda actual no esté filtrada en las casillas **Bands:** de la pestaña **Spot List**.
- **La consola POTA Activations está vacía** — Es posible que no haya activaciones de POTA activas en este momento, o que la consulta aún no se haya completado. Espere a que transcurra el siguiente intervalo de consulta.
- **La casilla de FreeDV Reporter se desmarca inmediatamente** — El campo **Callsign:** o **Grid Square:** está vacío. Ingrese un indicativo válido y una cuadrícula Maidenhead válida (o active **Use radio** / **Use GPS** si la radio los suministra) y marque la casilla nuevamente.

## Relacionados

- [Descripción general de SpotHub](overview.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
