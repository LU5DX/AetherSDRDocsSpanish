# Conceder o revocar el PTT local

Cuando varias estaciones comparten un radio Flex mediante multiFLEX, solo una estación tiene autoridad de PTT local a la vez. Esta página explica cómo reclamar el PTT local para su estación y cómo identificar qué estación lo tiene en ese momento.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El multiFLEX Dashboard requiere una conexión activa con el radio.
- multiFLEX debe estar habilitado en el radio. Si el botón Enable en el panel muestra "Disabled", consulte primero [Habilitar multiFLEX en el radio](enable-multiflex-on-the-radio.md).
- Al menos otro cliente multiFLEX debe estar conectado. El botón Enable (PTT) solo aparece cuando hay otra estación presente y su estación no tiene el PTT en ese momento.

## Pasos

1. Abra `Settings > multiFLEX...`.
2. En la tabla Stations, localice la columna LOCAL PTT. Una marca de verificación (✔) en esa columna identifica la estación que actualmente tiene la autoridad de PTT.
3. Si otra estación tiene el PTT y necesita reclamarlo para su estación, haga clic en `Enable` en la fila PTT debajo de la tabla. La etiqueta sobre ese botón muestra el nombre de la otra estación para confirmación.
4. Verifique nuevamente la columna LOCAL PTT. La marca de verificación debe aparecer ahora en la fila de su estación.
5. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Enable (multiFLEX) | Activa o desactiva multiFLEX en el radio. La etiqueta del botón refleja el estado actual: "Enabled" o "Disabled". |
| Stations table | Muestra todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). El nombre de su estación aparece resaltado. |
| Local PTT label | Texto sobre el botón Enable (PTT). Muestra el nombre de la otra estación que tiene el PTT en ese momento. Solo es visible cuando otra estación tiene el PTT y su estación no lo tiene. |
| Enable (PTT) | Solicita la autoridad de PTT local para su estación. Solo es visible cuando otro cliente tiene el PTT. |
| Close | Cierra el multiFLEX Dashboard. |

## Sugerencias

- La columna LOCAL PTT usa una marca de verificación para indicar qué estación tiene el PTT. Si usted es la única estación conectada, el PTT es automáticamente suyo y el botón Enable (PTT) no aparece.
- La columna STATION muestra las entradas con el formato `program: station`. La entrada de su estación aparece resaltada en un color distinto.
- TX ANT y TX FREQ (MHz) se actualizan automáticamente a medida que cambia el estado de las estaciones. Si no hay datos disponibles para una columna, muestra `----`.

## Solución de problemas

- **El botón Enable (PTT) no es visible** — Su estación ya tiene el PTT, o solo hay una estación conectada. El botón solo aparece cuando otro cliente tiene la autoridad de PTT. Verifique la columna LOCAL PTT para confirmarlo.
- **La tabla Stations está vacía** — Es posible que el radio aún no haya reportado el estado de los clientes. Cierre y vuelva a abrir `Settings > multiFLEX...` para forzar una actualización, o verifique que la conexión con el radio esté activa.
- **TX ANT y TX FREQ muestran `----` para su estación** — Es posible que la información de su slice de TX aún no se haya recibido. Verifique que tenga un slice activo con TX habilitado.

## Relacionados

- [Descripción general del multiFLEX Dashboard](overview.md)
- [Habilitar multiFLEX en el radio](enable-multiflex-on-the-radio.md)
- [Verificar qué antena y frecuencia usa cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
