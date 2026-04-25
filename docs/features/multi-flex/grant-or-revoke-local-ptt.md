# Otorgar o revocar PTT local

Use el multiFLEX Dashboard para reclamar la autoridad de PTT local para su estación o para ver qué estación la tiene en ese momento. Esto es necesario cuando varios clientes comparten el mismo FLEX-8600 y solo uno puede transmitir a la vez.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El multiFLEX Dashboard requiere una conexión activa con el radio.
- multiFLEX debe estar habilitado en el radio. Si no lo está, consulte [Habilitar multiFLEX en el radio](enable-multiflex-on-the-radio.md).
- Deben estar conectadas al menos dos estaciones para que aparezcan los controles de PTT.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el multiFLEX Dashboard.
2. Observe la tabla **Stations table**. La columna LOCAL PTT muestra una marca de verificación junto a la estación que actualmente tiene el PTT.
3. Si su estación no tiene el PTT, aparece una etiqueta con el texto `Enable Local PTT for this station (<your station name>):` debajo de la tabla, seguida del botón Enable.
4. Haga clic en `Enable` para reclamar el PTT local para su estación.
5. La marca de verificación en la columna LOCAL PTT se mueve a la fila de su estación, confirmando el cambio.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Enable (multiFLEX toggle) | Habilita o deshabilita multiFLEX en el radio. Se muestra como **Enabled** o **Disabled** según el estado actual. |
| Stations table | Lista todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). Su estación aparece resaltada en azul. |
| Local PTT label | Muestra qué estación tiene actualmente el PTT, o le solicita reclamarlo para su estación. Se oculta cuando solo hay una estación conectada. |
| Enable (PTT) | Reclama la autoridad de PTT local para su estación. Solo se muestra cuando su estación no tiene el PTT en ese momento. |
| Close | Cierra el multiFLEX Dashboard. |

## Consejos

- Los controles de PTT (la etiqueta y el botón Enable) se ocultan cuando solo hay una estación conectada. Aparecen automáticamente una vez que se une una segunda estación.
- Si su estación ya tiene el PTT y selecciona la fila de otra estación en la tabla, la etiqueta indicará que esa otra estación debe reclamar el PTT desde su propio cliente. No es posible transferir la autoridad de PTT a otro operador desde su lado.
- La fila de su estación siempre se muestra en azul en la columna STATION, lo que facilita identificar su entrada entre varios clientes.

## Solución de problemas

- **El botón Enable no es visible** — Su estación ya tiene el PTT, o solo hay una estación conectada en este momento. Verifique la columna LOCAL PTT para localizar la marca de verificación. Si usted es la única estación conectada, no se necesita ninguna negociación de PTT.
- **La marca de verificación no se mueve después de hacer clic en Enable** — Confirme que la conexión con el radio está activa y que multiFLEX está habilitado. El botón Enable en la parte superior del diálogo debe mostrar **Enabled**.
- **La etiqueta Local PTT y el botón Enable están ambos ocultos** — Solo hay un cliente conectado al radio. Los controles aparecen únicamente cuando hay dos o más clientes presentes.

## Relacionado

- [Habilitar multiFLEX en el radio](enable-multiflex-on-the-radio.md)
- [Verificar qué antena y frecuencia usa cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
