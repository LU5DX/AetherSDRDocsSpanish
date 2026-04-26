# Descripción general del panel multiFLEX

El panel multiFLEX muestra todos los clientes que comparten actualmente su FLEX-8600, y le permite habilitar multiFLEX en la radio, monitorear el estado de transmisión de cada estación y administrar la autoridad PTT local. Ábralo cuando necesite ver quién más está conectado o para reclamar PTT para su estación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel multiFLEX requiere una conexión de radio activa.
- El firmware de su FLEX-8600 debe ser compatible con multiFLEX (firmware 4.1.5, protocolo SmartSDR v1.4.0.0).

## Cómo funciona

Abra el panel desde `Settings > multiFLEX...`. El cuadro de diálogo tiene el título **multiFLEX Dashboard** y muestra el encabezado **multiFLEX Stations**.

Cuando solo hay un cliente conectado, los controles PTT locales están ocultos: la gestión de PTT solo es relevante cuando dos o más estaciones comparten la radio. La tabla y la sección PTT se actualizan automáticamente cuando otro cliente se conecta, se desconecta o cambia su estado de transmisión.

El **estado de habilitación de multiFLEX** se activa o desactiva con el botón en la parte superior del cuadro de diálogo. La etiqueta del botón refleja el estado actual: muestra **Enabled** (verde) cuando multiFLEX está activo en la radio, y **Disabled** (rojo) cuando no lo está. Al hacer clic en el botón, el estado cambia de inmediato.

El **PTT local** se gestiona por estación. Solo una estación puede tener la autoridad PTT a la vez. Si su estación no tiene actualmente el PTT, el panel muestra la etiqueta "Enable Local PTT for this station (*nombre de estación*):" junto al botón **Enable**. Si su estación ya tiene el PTT y selecciona la fila de otra estación en la tabla, el panel muestra un mensaje que indica que la otra estación debe reclamar el PTT desde su propio cliente; no es posible otorgárselo desde aquí.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Enabled** / **Disabled** | Botón | Habilita o deshabilita multiFLEX en la radio. La etiqueta y el color reflejan el estado actual. |
| Tabla de estaciones | Lista | Enumera todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). Su propia estación aparece resaltada. Una marca de verificación (✔) en LOCAL PTT indica la estación que actualmente tiene la autoridad PTT. |
| Etiqueta PTT local | Indicador | Muestra texto contextual: una invitación para reclamar el PTT para su estación o un mensaje de que otra estación seleccionada debe reclamar el PTT por su cuenta. Se oculta cuando solo hay un cliente conectado. |
| **Enable** (PTT) | Botón | Solicita la autoridad PTT local para esta estación. Visible solo cuando su estación no tiene actualmente el PTT y hay al menos otro cliente conectado. |
| **Close** | Botón | Cierra el cuadro de diálogo. |

### Columnas de la tabla de estaciones

| Columna | Contenido |
|---|---|
| LOCAL PTT | Marca de verificación si esta estación tiene actualmente la autoridad PTT. |
| STATION | Nombre del programa y nombre de la estación, con el formato *programa: estación*. Su propia estación se muestra en azul. |
| TX ANT | La antena de transmisión asignada al slice TX de esta estación. Muestra `----` si no está disponible. |
| TX FREQ (MHz) | La frecuencia de transmisión en MHz con tres decimales. Muestra `----` si no está disponible. |

## Consejos

- Si selecciona una fila en la tabla de estaciones mientras su estación tiene el PTT, se mostrará un mensaje indicando que esa estación debe reclamar el PTT desde su propio cliente. No se requiere ninguna acción de su parte ni es posible realizarla desde este cuadro de diálogo en esa situación.
- La tabla se actualiza automáticamente cuando otros clientes se conectan o desconectan. No es necesario volver a abrir el cuadro de diálogo.

## Temas relacionados

- [Habilitar multiFLEX en la radio](enable-multiflex-on-the-radio.md)
- [Otorgar o revocar el PTT local](grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia usa cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
