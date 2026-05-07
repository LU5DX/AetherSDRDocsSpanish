# Activar activaciones POTA

AetherSDR puede obtener periódicamente las activaciones actuales de Parks on the Air (POTA) desde `api.pota.app` y mostrarlas como spots en su panadapter. Esto le permite encontrar operadores POTA activos sin necesidad de un navegador web separado o una fuente de cluster.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. No se requiere una conexión de radio para configurar esta función.
- El acceso HTTP saliente a `api.pota.app` no debe estar bloqueado por un cortafuegos.

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Haga clic en la pestaña **POTA**.
3. Revise el indicador **Server:**, que muestra `api.pota.app (HTTP polling)`. Este endpoint es fijo y no se puede cambiar.
4. Establezca **Poll Interval:** en el número de segundos entre cada consulta. Este valor se guarda como `PotaPollInterval`.
5. Haga clic en **Start** para comenzar la consulta. El indicador de estado cambia a **Polling** cuando está activo. Haga clic en **Stop** para detener la consulta en cualquier momento.
6. Para cambiar el color utilizado para los spots POTA en el panadapter, haga clic en **Spot Color:**. Seleccione un color del selector. Esto se guarda como `PotaSpotColor`.
7. Para iniciar la consulta automáticamente cada vez que AetherSDR se inicie, haga clic en **Auto-start on startup** para que esté activo. Esto se guarda como `PotaAutoStart`.
8. Monitoree las activaciones entrantes en la consola **POTA Activations** en la misma pestaña.

## Función de cada control

| Control                      | Tipo           | Comportamiento                                                                                                                                                                          |
|------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Server:**                  | Indicador      | Muestra el endpoint de consulta fijo: `api.pota.app (HTTP polling)`. No configurable.                                                                                                  |
| **Poll Interval:**           | Spinbox        | Segundos entre consultas a la API de POTA. Se guarda como `PotaPollInterval`.                                                                                                           |
| **Start / Stop**             | Botón          | Inicia o detiene la consulta POTA.                                                                                                                                                     |
| **Auto-start on startup**    | Botón de alternancia | Inicia automáticamente la consulta POTA cuando AetherSDR se inicia. Se guarda como `PotaAutoStart`.                                                                                    |
| **POTA Activations**         | Campo de texto | Consola de solo lectura que muestra el flujo de activaciones.                                                                                                                           |
| **Spot Color:**              | Botón          | Abre un selector de color para los spots POTA en el panadapter. Se guarda como `PotaSpotColor`.                                                                                        |
| Total Spots:                 | Indicador      | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se actualiza cuando se agregan o eliminan spots. Se restablece a 0 al presionar **Clear All Spots**. |
| **Spot Lines:**              | Botón de alternancia | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Activado por defecto. Desactívelo durante concursos para reducir el desorden visual. Se guarda como `IsSpotsLinesEnabled`. Nuevo en v0.9.7. |
## Controles del Reporter FreeDV (pestaña FreeDV)

Los siguientes controles aparecen en el cuadro **Station Reporting** en la pestaña **FreeDV**. Solo están presentes en compilaciones compiladas con `HAVE_WEBSOCKETS`.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Casilla de verificación | Reporta su estación al mapa público FreeDV Reporter en `qso.freedv.org` siempre que el módem RADE esté activo. Si el campo de indicativo o de cuadrícula está vacío al marcar esta casilla, aparece un diálogo de advertencia y la casilla se desmarca. Se guarda como `FreeDvAutoReport`. En Windows, también requiere una compilación con `HAVE_RADE`. |
| **Callsign:** | Campo de texto | Indicativo enviado al mapa FreeDV Reporter. Se vuelve de solo lectura cuando **Use radio** está marcado. Se guarda como `FreeDvMyCallsign`. |
| **Use radio** | Casilla de verificación | Rellena previamente el campo **Callsign:** con el indicativo configurado en la radio y lo bloquea como solo lectura. Se actualiza automáticamente si el indicativo cambia en Radio Setup. Se guarda como `FreeDvUseRadioCallsign`. Predeterminado: activado. |
| **Grid Square:** | Campo de texto | Cuadrícula Maidenhead enviada al mapa FreeDV Reporter. Se vuelve de solo lectura cuando **Use GPS** está marcado. Se guarda como `FreeDvMyGrid`. |
| **Use GPS** | Casilla de verificación | Rellena previamente el campo **Grid Square:** con la cuadrícula del módulo GPS de la radio y lo bloquea como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. Se guarda como `FreeDvUseGpsGrid`. Predeterminado: activado. |
| **Station Msg:** | Campo de texto | Mensaje de texto libre opcional que se muestra junto a su indicativo en el mapa público FreeDV Reporter. Se guarda como `FreeDvMyMessage`. |

### Habilitar el reporte FreeDV Reporter

Antes de habilitar **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR resuelve su indicativo y cuadrícula efectivos en este orden:

1. Si **Use radio** está marcado y la radio tiene un indicativo no vacío configurado, se usa ese indicativo. De lo contrario, se usa el texto ingresado en **Callsign:**.
2. Si **Use GPS** se muestra y está marcado y el módulo GPS de la radio proporciona una cuadrícula no vacía, se usa esa cuadrícula. De lo contrario, se usa el texto ingresado en **Grid Square:**.

Si el indicativo o la cuadrícula resueltos están vacíos, AetherSDR muestra una advertencia y deja la casilla sin marcar. Complete ambos campos antes de intentarlo nuevamente.

## Cambio en el valor predeterminado de Auto Mode

A partir de v0.9.5.1, la alternancia **Auto Mode:** en la pestaña **Display** tiene como valor predeterminado **Enabled**. La configuración se guarda como `SpotAutoSwitchMode`. Si anteriormente dejó esto en su valor predeterminado, ahora estará activo después de una instalación nueva. Las instalaciones existentes conservan el valor que se guardó por última vez.

## Sintonizar un spot haciendo doble clic en la lista de spots

A partir de v0.9.7, hacer doble clic en una fila de la pestaña **Spot List** sintoniza su radio a la frecuencia del spot y también envía una sugerencia de modo derivada del comentario del spot. AetherSDR cambiará el slice activo a CW, SSB o al modo digital apropiado para coincidir con el spot, en lugar de solo cambiar la frecuencia. Si el comentario del spot no contiene un token de modo reconocible, el modo del slice no se modifica.

## Consejos

- Los spots POTA aparecen en la pestaña unificada **Spot List** junto con spots de otras fuentes. La columna **Source** los identifica.
- Hacer doble clic en una fila de spot POTA en Spot List sintoniza su radio a esa frecuencia y cambia el modo del slice para que coincida con el spot cuando sea posible. Consulte [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md).
- Si los spots no son visibles en el panadapter, confirme que la alternancia maestra **Spots:** en la pestaña **Display** esté configurada en **Enabled** (`IsSpotsEnabled`).
- Para reducir el desorden del panadapter durante un concurso, establezca **Spot Lines:** en **Disabled** en la pestaña **Display**. Esto oculta las líneas verticales mientras mantiene visibles las etiquetas de los spots.

## Solución de problemas

- **El estado permanece en Stopped después de hacer clic en Start** — La aplicación no puede alcanzar `api.pota.app`. Verifique su conexión a Internet y confirme que ningún cortafuegos o proxy esté bloqueando el HTTP saliente.
- **No aparecen spots en el panadapter a pesar del estado Polling** — Verifique que **Spots:** en la pestaña **Display** esté **Enabled**. También compruebe que la banda actual no esté filtrada en las casillas de verificación **Bands:** de la pestaña **Spot List**.
- **La consola POTA Activations está vacía** — Puede que no haya activaciones POTA activas en este momento, o que la consulta aún no se haya completado. Espere hasta que transcurra el siguiente intervalo de consulta.
- **La casilla FreeDV Reporter se desmarca inmediatamente** — El campo **Callsign:** o **Grid Square:** está vacío. Ingrese un indicativo y una cuadrícula Maidenhead válidos (o active **Use radio** / **Use GPS** si la radio los proporciona), luego vuelva a marcar la casilla.
- **Auto Mode: tiene como valor predeterminado Enabled en instalaciones nuevas** — A partir de v0.9.5.1, **Auto Mode:** tiene como valor predeterminado **Enabled**. Si prefiere que al hacer clic en un spot no se cambie automáticamente el modo del slice, establezca **Auto Mode:** en **Disabled** en la pestaña **Display** y la preferencia se guardará.
- **Hacer doble clic en un spot cambia al modo incorrecto** — El modo se infiere del texto del comentario del spot. Si el comentario no contiene un token de modo estándar, el modo del slice no se modifica. Edite la configuración del filtro en la pestaña de origen correspondiente para mejorar la calidad del comentario, o cambie el modo manualmente después de sintonizar.

## Relacionado

- [Descripción general de SpotHub](overview.md)
- [Sintonizar un spot haciendo doble clic en la lista de spots](tune-to-a-spot-by-double-clicking-the-spot-list.md)
- [Elegir colores para cada fuente de spot](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y vida útil de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Borrar todos los spots del panadapter](clear-all-spots-from-the-panadapter.md)
<!-- docmesh:llm version=v0.9.7 date=2026-05-03 -->
