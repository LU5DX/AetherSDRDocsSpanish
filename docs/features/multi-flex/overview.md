# Visión general del panel multiFLEX

El panel multiFLEX muestra cada estación cliente que está compartiendo actualmente su FLEX-8600 y le permite gestionar la autoridad de PTT entre esas estaciones. Úselo cuando opere en un entorno con múltiples operadores o múltiples programas de software y necesite ver quién está transmitiendo, en qué antena y a qué frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel multiFLEX no está disponible sin una conexión activa con la radio.
- El firmware de su FLEX-8600 debe ser compatible con la función multiFLEX de SmartSDR.

## Cómo funciona

Abra el panel desde `Settings > multiFLEX...`. El diálogo muestra el encabezado **multiFLEX Stations** y se actualiza automáticamente cuando un cliente se conecta o desconecta, o cuando el estado de los slices cambia en la radio.

En la parte superior del diálogo, el botón **Enabled** / **Disabled** refleja el estado actual de multiFLEX en la radio. Al hacer clic en él, se activa o desactiva multiFLEX y la etiqueta del botón se actualiza inmediatamente para reflejar el nuevo estado.

La **tabla de estaciones** enumera cada cliente multiFLEX conectado en cuatro columnas:

| Columna | Contenido |
|---|---|
| LOCAL PTT | Una marca de verificación (✔) aparece en verde cuando esa estación posee actualmente la autoridad de PTT local. |
| STATION | Muestra el nombre del programa cliente y el nombre de la estación en el formato *programa: estación*. Su propia estación se resalta en azul. |
| TX ANT | La antena de transmisión asignada al slice de TX de esa estación. Muestra `----` si no está disponible. |
| TX FREQ (MHz) | La frecuencia de transmisión del slice de TX de esa estación en MHz con tres decimales. Muestra `----` si no está disponible. |

Debajo de la tabla, la **etiqueta de PTT local** y el botón **Enable** (PTT) aparecen solo cuando hay más de un cliente conectado. Su contenido depende del estado actual de PTT:

- Si su estación no posee PTT, la etiqueta dice *Enable Local PTT for this station (nombre de estación):* y se muestra el botón **Enable**. Al hacer clic en **Enable** se solicita la autoridad de PTT local para su estación.
- Si su estación ya posee PTT y selecciona la fila de otra estación, la etiqueta le informa que la estación seleccionada debe solicitar el PTT desde su propio cliente. El botón **Enable** está oculto en este estado.
- Si solo hay un cliente conectado, tanto la etiqueta como el botón **Enable** están ocultos.

Al hacer clic en **Close** se cierra el diálogo.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enabled** / **Disabled** | Botón | Activa o desactiva multiFLEX en la radio. La etiqueta muestra el estado actual: **Enabled** (verde) o **Disabled** (rojo). |
| **Tabla de estaciones** | Lista | Muestra todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). Seleccionar una fila actualiza la sección de PTT debajo. |
| **Enable** (PTT) | Botón | Solicita la autoridad de PTT local para su estación. Visible solo cuando su estación no posee PTT actualmente y hay más de un cliente conectado. |
| Etiqueta de PTT local | Indicador | Muestra texto dependiente del contexto sobre el estado de PTT para la estación seleccionada. Oculto cuando solo hay un cliente conectado. |
| **Close** | Botón | Cierra el diálogo del panel multiFLEX. |

## Consejos

- La fila de su propia estación en la tabla de estaciones se resalta en azul, lo que facilita identificar su entrada entre múltiples clientes.
- Los datos de antena de TX y frecuencia de su propia estación se obtienen directamente de su slice de TX activo, por lo que reflejan el estado actual incluso si la información del cliente desde la radio aún no se ha actualizado.
- La tabla se actualiza automáticamente; no necesita cerrar y volver a abrir el diálogo para ver nuevos clientes.

## Relacionados

- [Enable multiFLEX on the radio](enable-multiflex-on-the-radio.md)
- [Grant or revoke local PTT](grant-or-revoke-local-ptt.md)
- [Check which antenna and frequency each TX station is using](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [See all stations connected to this FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
