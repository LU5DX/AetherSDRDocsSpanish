# Descripción general del panel multiFLEX

El panel multiFLEX muestra todos los clientes SmartSDR que comparten actualmente su radio Flex y le permite gestionar la autoridad PTT entre ellos. Úselo cuando más de un operador o aplicación esté conectado a la misma radio y necesite ver quién tiene el control de transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel requiere una conexión de radio activa.
- multiFLEX debe ser compatible con el firmware de su radio (radio Flex, firmware 4.1.5).

## Cómo funciona

Abra el panel desde `Settings > multiFLEX...`. El título del diálogo es "multiFLEX Dashboard".

Al abrir el diálogo, AetherSDR consulta a la radio la lista actual de clientes conectados y rellena la tabla Stations automáticamente. La tabla se actualiza cada vez que un cliente se conecta, se desconecta o cambia su estado PTT — no es necesario recargarla manualmente.

Cada fila de la tabla Stations representa un cliente SmartSDR conectado. Su propia estación aparece resaltada en azul. Una marca de verificación (✔) en la columna LOCAL PTT identifica la estación que actualmente tiene la autoridad PTT.

Cuando otro cliente tiene PTT y hay más de un cliente conectado, la etiqueta "Enable Local PTT for this station" y el botón Enable (PTT) aparecen debajo de la tabla. Cuando usted es el único cliente conectado, la autoridad PTT le corresponde implícitamente y esos controles se ocultan.

El botón alternante Enable / Disabled en la parte superior del diálogo refleja el estado actual de multiFLEX en la radio. Al hacer clic, activa o desactiva multiFLEX a nivel de radio y actualiza el diálogo de inmediato.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Enable / Disabled | Botón | Activa o desactiva multiFLEX en la radio. La etiqueta muestra "Enabled" (verde) cuando está activo y "Disabled" (rojo) cuando está inactivo. Haga clic para alternar. |
| Tabla Stations | Tabla | Lista cada cliente multiFLEX conectado. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). Su estación aparece en azul. Un ✔ en LOCAL PTT marca la estación con autoridad de transmisión. |
| Etiqueta Local PTT | Etiqueta | Muestra "Enable Local PTT for this station (nombre de estación):" cuando otro cliente tiene PTT. Se oculta cuando usted tiene PTT o es el único cliente. |
| Enable (PTT) | Botón | Alterna la autoridad PTT local para esta estación. Solo es visible cuando otro cliente tiene PTT y hay más de un cliente conectado. |
| Close | Botón | Cierra el diálogo. |

### Columnas de la tabla Stations

| Columna | Contenido |
|---|---|
| LOCAL PTT | Marca de verificación (✔) si esta estación tiene actualmente PTT local. Vacío en caso contrario. |
| STATION | Nombre del programa cliente y nombre de la estación, con el formato "program: station". Su estación aparece resaltada en azul. |
| TX ANT | La antena de transmisión asignada al slice TX de esta estación. Muestra `----` si no está disponible. |
| TX FREQ (MHz) | La frecuencia de transmisión del slice TX de esta estación en MHz, con tres decimales. Muestra `----` si no está disponible. |

## Consejos

- La tabla Stations se actualiza automáticamente cuando los clientes se unen o abandonan la sesión. No es necesario cerrar y volver a abrir el diálogo para ver los cambios.
- TX ANT y TX FREQ reflejan el slice TX asignado a cada cliente. Si un cliente no tiene un slice TX activo, ambas columnas muestran `----`.
- El botón Enable (PTT) solo aparece cuando otra estación tiene PTT. Si usted es el único cliente conectado, PTT se concede implícitamente y el botón no se muestra.

## Relacionado

- [Activar multiFLEX en la radio](enable-multiflex-on-the-radio.md)
- [Conceder o revocar PTT local](grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia usa cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
