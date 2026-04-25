# Descripción general del panel multiFLEX

El panel multiFLEX muestra todos los clientes SmartSDR que comparten actualmente su FLEX-8600 y permite gestionar la autoridad de PTT entre estaciones. Úselo cuando más de un operador o aplicación esté conectado al mismo radio y necesite ver quién está transmitiendo, en qué antena y en qué frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El panel requiere una conexión de radio activa.
- multiFLEX debe ser compatible con el firmware de su radio (versión 4.1.5 o posterior).

## Cómo funciona

Abra el panel con `Settings > multiFLEX...`. El título del diálogo es **multiFLEX Dashboard** y su elemento central es la tabla **Stations table**, que se actualiza automáticamente cada vez que los clientes se conectan, desconectan o cambian de estado.

Cada fila de la tabla **Stations table** representa un cliente SmartSDR conectado. La tabla tiene cuatro columnas:

| Columna | Qué muestra |
|---|---|
| LOCAL PTT | Una marca de verificación (✔) si esa estación posee actualmente la autoridad de PTT local. |
| STATION | El nombre del programa y el nombre de estación del cliente. Su propia estación aparece resaltada en azul. |
| TX ANT | La antena de transmisión que usa ese cliente. Muestra `----` si no está disponible. |
| TX FREQ (MHz) | La frecuencia de transmisión en MHz con tres decimales. Muestra `----` si no está disponible. |

La etiqueta **Local PTT label** situada encima del botón PTT muestra texto de estado según el contexto. Si su estación no posee PTT, muestra algo como `Enable Local PTT for this station (<your station name>):`. Si otra estación posee PTT, identifica a esa estación e indica que deben reclamar PTT desde su propio cliente.

Cuando solo hay un cliente conectado, la etiqueta PTT y el botón PTT están ocultos, ya que solo son relevantes en un escenario de múltiples estaciones.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Enable | Activa o desactiva multiFLEX en el radio. Cuando multiFLEX está activo, la etiqueta del botón cambia a **Enabled** (verde); cuando está inactivo, muestra **Disabled** (rojo). Haga clic para alternar el estado actual. |
| Stations table | Lista todos los clientes multiFLEX conectados con su estado de LOCAL PTT, nombre de estación, antena TX y frecuencia TX. Se actualiza automáticamente ante cualquier cambio de cliente. |
| Enable (PTT) | Aparece cuando su estación no posee actualmente PTT local y hay más de un cliente conectado. Haga clic para reclamar la autoridad de PTT local para su estación. La etiqueta del botón es **Enable**. |
| Close | Cierra el diálogo. |

## Sugerencias

- La fila de su propia estación aparece resaltada con un color distintivo en la columna STATION, lo que facilita identificarse entre varios clientes.
- Si usted posee PTT y otra estación necesita transmitir, ese operador debe reclamar PTT desde su propio cliente; no es posible otorgárselo desde este diálogo.
- Las columnas TX ANT y TX FREQ obtienen los datos del estado del slice del radio. Si un cliente se conectó antes de recibir el estado de su slice, estos campos pueden mostrar brevemente `----` hasta que el panel se actualice.

## Temas relacionados

- [Activar multiFLEX en el radio](enable-multiflex-on-the-radio.md)
- [Otorgar o revocar PTT local](grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia usa cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
