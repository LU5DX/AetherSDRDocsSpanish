# Identifique cada cliente por programa y nombre de estación

Utilice el diálogo de Estaciones Conectadas para ver la identificación detallada (nombre del programa y nombre de estación opcional) de cada cliente conectado a su FLEX-8600. Esto le ayuda a reconocer qué cliente debe desconectar cuando multiFLEX está deshabilitado y hay otra sesión activa.

## Antes de comenzar

- Su radio debe estar conectada a AetherSDR.

## Pasos

1. Abra **Help > Connected Stations…**.

2. En la sección Radio, confirme el modelo, el apodo y el indicativo de la radio mostrados.

3. En la sección Connected Stations, revise cada entrada de botón de opción. Cada entrada muestra el nombre del programa del cliente y, si está configurado, el nombre de la estación, en el formato `ProgramName: StationName`.

   – Si el cliente no reporta un nombre de programa o estación, se muestra como `client 0x<HEX>`.

## Función de cada control

| Control | Descripción |
|---|---|
| Radio section | Bloque de solo lectura que muestra el modelo, el apodo y el indicativo de la radio conectada. |
| Station radio buttons | Uno por cada cliente conectado. La etiqueta muestra el nombre del programa, opcionalmente seguido de `: StationName`. |
| Disconnect Station | Desconecta el cliente seleccionado. Se habilita solo cuando se ha marcado un botón de opción. |
| Cancel | Cierra el diálogo sin desconectar. |
| Info label | Explica que multiFLEX está deshabilitado y que debe seleccionar una estación para desconectar antes de conectar AetherSDR. |

## Relacionado

- [Connected Stations overview](overview.md)
- [Disconnect another client to free a slot](../../getting-started/setup/disconnect-another-client-to-free-a-slot.md)
- [See all stations connected when multiFLEX is off](../../getting-started/setup/see-all-stations-connected-when-multiflex-is-off.md)
