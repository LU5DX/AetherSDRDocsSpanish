# Descripción general del panel multiFLEX

El panel multiFLEX muestra todas las estaciones cliente que comparten actualmente su FLEX-8600 y le permite gestionar la autoridad PTT entre esas estaciones. Úselo cuando opere en un entorno de múltiples operadores o múltiples programas y necesite ver quién está transmitiendo, en qué antena y en qué frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel multiFLEX no está disponible sin una conexión activa al radio.
- El firmware de su FLEX-8600 debe ser compatible con la función multiFLEX de SmartSDR.

## Cómo funciona

Abra el panel desde `Settings > multiFLEX...`. El diálogo muestra el encabezado **multiFLEX Stations** y se actualiza automáticamente cada vez que un cliente se conecta o desconecta, o cuando el estado de un slice cambia en el radio.

En la parte superior del diálogo, el botón **Enabled** / **Disabled** refleja el estado actual de multiFLEX en el radio. Al hacer clic en él se activa o desactiva multiFLEX, y la etiqueta del botón se actualiza de inmediato para reflejar el nuevo estado.

La **tabla Stations** lista todos los clientes multiFLEX conectados en cuatro columnas:

| Columna | Contenido |
|---|---|
| LOCAL PTT | Aparece una marca de verificación (✔) en verde cuando esa estación tiene actualmente la autoridad PTT local. |
| STATION | Muestra el nombre del programa cliente y el nombre de la estación en la forma *programa: estación*. Su propia estación aparece resaltada en azul. |
| TX ANT | La antena de transmisión asignada al slice TX de esa estación. Muestra `----` si no está disponible. |
| TX FREQ (MHz) | La frecuencia de transmisión del slice TX de esa estación en MHz con tres decimales. Muestra `----` si no está disponible. |

Debajo de la tabla, la **etiqueta Local PTT** y el botón **Enable** (PTT) aparecen únicamente cuando hay más de un cliente conectado. Su contenido depende del estado PTT actual:

- Si su estación no tiene PTT, la etiqueta muestra *Enable Local PTT for this station (nombre de estación):* y se muestra el botón **Enable**. Al hacer clic en **Enable** se solicita la autoridad PTT local para su estación.
- Si su estación ya tiene PTT y selecciona la fila de otra estación, la etiqueta le informa que la estación seleccionada debe reclamar PTT desde su propio cliente. El botón **Enable** se oculta en este estado.
- Si solo hay un cliente conectado, tanto la etiqueta como el botón **Enable** se ocultan.

Haga clic en **Close** para cerrar el diálogo.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enabled** / **Disabled** | Botón | Activa o desactiva multiFLEX en el radio. La etiqueta muestra el estado actual: **Enabled** (verde) o **Disabled** (rojo). |
| **Tabla Stations** | Lista | Muestra todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). Al seleccionar una fila se actualiza la sección PTT inferior. |
| **Enable** (PTT) | Botón | Solicita la autoridad PTT local para su estación. Visible solo cuando su estación no tiene PTT actualmente y hay más de un cliente conectado. |
| Etiqueta Local PTT | Indicador | Muestra texto contextual sobre el estado PTT de la estación seleccionada. Se oculta cuando solo hay un cliente conectado. |
| **Close** | Botón | Cierra el diálogo del panel multiFLEX. |

## Consejos

- La fila de su propia estación en la tabla Stations aparece resaltada en azul, lo que facilita identificar su entrada entre múltiples clientes.
- Los datos de antena TX y frecuencia de su propia estación se obtienen directamente de su slice TX activo, por lo que reflejan el estado actual aunque la información del cliente proveniente del radio aún no se haya actualizado.
- La tabla se actualiza automáticamente; no es necesario cerrar y volver a abrir el diálogo para ver nuevos clientes.

## Temas relacionados

- [Activar multiFLEX en el radio](enable-multiflex-on-the-radio.md)
- [Conceder o revocar PTT local](grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia usa cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
