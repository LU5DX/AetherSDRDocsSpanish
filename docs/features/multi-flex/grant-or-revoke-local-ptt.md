# Otorgar o revocar PTT local

Use el panel multiFLEX Dashboard para reclamar la autoridad de PTT local para su estación o para ver qué estación la tiene actualmente. Esto es necesario cuando varios clientes comparten un único FLEX-8600 y solo uno puede transmitir a la vez.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El multiFLEX Dashboard requiere una conexión activa con la radio.
- multiFLEX debe estar habilitado en la radio. Si el botón Enable del panel muestra "Disabled", consulte [Habilitar multiFLEX en la radio](enable-multiflex-on-the-radio.md) antes de continuar.
- Deben estar conectadas al menos dos estaciones para que aparezcan los controles de PTT. Con solo una estación conectada, la sección de PTT está oculta.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el multiFLEX Dashboard.
2. Revise la tabla Stations. La columna LOCAL PTT muestra una marca de verificación junto a la estación que actualmente tiene el PTT.
3. Si su estación no tiene el PTT, aparece debajo de la tabla una etiqueta con el texto `Enable Local PTT for this station (<your station name>):`, junto con un botón Enable.
4. Haga clic en Enable para reclamar el PTT local para su estación.

Para liberar el PTT, otra estación debe reclamarlo desde su propio cliente. No es posible otorgar el PTT a otra estación desde su cliente. Si selecciona la fila de otra estación mientras usted tiene el PTT, el panel muestra un mensaje indicando que la otra estación debe reclamar el PTT desde su propio cliente.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Enable (multiFLEX) | Activa o desactiva multiFLEX en la radio. Muestra "Enabled" (verde) o "Disabled" (rojo) para reflejar el estado actual. |
| Tabla Stations | Lista todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). Su estación aparece resaltada en azul. Una marca de verificación verde en LOCAL PTT indica qué estación tiene la autoridad de PTT. |
| Enable (PTT) | Reclama el PTT local para su estación. Solo es visible cuando su estación no tiene actualmente el PTT y hay más de una estación conectada. |
| Close | Cierra el multiFLEX Dashboard. |

## Sugerencias

- La tabla Stations se actualiza automáticamente a medida que los clientes se conectan, desconectan o cambian de estado. No es necesario volver a abrir el diálogo para ver el estado actual del PTT.
- La fila de su estación aparece resaltada con un color distintivo para que pueda identificarla rápidamente en una tabla con muchas entradas.
- Si el botón Enable y la etiqueta de PTT están ausentes, es probable que solo haya una estación conectada o que su estación ya tenga el PTT.

## Solución de problemas

- **El botón Enable y la etiqueta de PTT no aparecen** — Su estación ya tiene el PTT o hay menos de dos estaciones conectadas actualmente. Revise la columna LOCAL PTT para confirmar qué estación lo tiene.
- **Los controles de PTT no aparecen en absoluto** — multiFLEX puede estar deshabilitado. Haga clic en el botón Enable en la parte superior del panel para habilitarlo y verifique que la radio reconozca el cambio (el botón se vuelve verde y muestra "Enabled").
- **No puede otorgar el PTT a otra estación** — Esto es por diseño. Cada estación debe reclamar el PTT desde su propio cliente. Informe al otro operador que abra su multiFLEX Dashboard y haga clic en Enable en la sección de PTT.

## Relacionados

- [Habilitar multiFLEX en la radio](enable-multiflex-on-the-radio.md)
- [Verificar qué antena y frecuencia usa cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
