# Identificar cada cliente por programa y nombre de estación

Utilice el cuadro de diálogo Estaciones Conectadas para ver la identificación detallada (nombre del programa y nombre de estación opcional) de cada cliente conectado a su FLEX-8600. Esto le ayuda a reconocer qué cliente desconectar cuando multiFLEX está deshabilitado y otra sesión está activa.

## Antes de comenzar

- Su radio debe estar conectada a AetherSDR.

## Pasos

1. Abra **Help > Connected Stations…**.

2. En la sección Radio, confirme el modelo, apodo e indicativo de la radio mostrada.

3. En la sección Connected Stations, revise cada entrada con botón de opción. Cada entrada muestra el nombre del programa del cliente y, si está configurado, el nombre de la estación, en el formato `ProgramName: StationName`.

   – Si el cliente no reporta un nombre de programa o estación, se utiliza la opción de respaldo `client 0x<HEX>`.

4. Para desconectar un cliente, seleccione su botón de opción y haga clic en **Disconnect Station**.

5. Haga clic en **Cancel** para cerrar el cuadro de diálogo sin desconectar.

## Función de cada control

| Control | Descripción |
|---|---|
| Radio section | Bloque de solo lectura que muestra el modelo, apodo e indicativo de la radio conectada. |
| Station radio buttons | Uno por cada cliente conectado. La etiqueta muestra el nombre del programa, opcionalmente seguido de `: StationName`. |
| Disconnect Station | Desconecta el cliente seleccionado. Solo se habilita cuando un botón de opción está marcado. |
| Cancel | Cierra el cuadro de diálogo sin desconectar. |
| Info label | Explica que multiFLEX está deshabilitado y que debe seleccionar una estación para desconectar antes de conectar AetherSDR. |

## Soporte de temas

El cuadro de diálogo aplica el contenedor de tema `dialog/connectedStations`, lo que garantiza un estilo coherente con otros cuadros de diálogo temáticos en AetherSDR.

## Relacionados

- [Connected Stations overview](overview.md)
- [Disconnect another client to free a slot](../../getting-started/setup/disconnect-another-client-to-free-a-slot.md)
- [See all stations connected when multiFLEX is off](../../getting-started/setup/see-all-stations-connected-when-multiflex-is-off.md)
