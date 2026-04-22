# Verificar la antena y frecuencia de transmisión de cada estación TX

El panel multiFLEX Dashboard muestra la antena de transmisión y la frecuencia de cada estación que comparte el radio en ese momento. Use esta página para confirmar lo que hace cada cliente conectado antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El multiFLEX Dashboard requiere una conexión activa con el radio.
- multiFLEX debe estar habilitado en el radio. Si el panel no muestra estaciones, consulte [Habilitar multiFLEX en el radio](enable-multiflex-on-the-radio.md).

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el multiFLEX Dashboard.
2. Lea la tabla Stations. Cada fila corresponde a un cliente conectado.
3. Localice la columna **TX ANT** para ver la antena de transmisión que usa cada estación.
4. Localice la columna **TX FREQ (MHz)** para ver la frecuencia de transmisión de cada estación, expresada en MHz con tres decimales.
5. Haga clic en `Close` cuando termine.

## Descripción de cada control

| Control | Descripción |
|---|---|
| Tabla Stations | Lista todos los clientes multiFLEX conectados al radio en ese momento. Columnas: **LOCAL PTT**, **STATION**, **TX ANT**, **TX FREQ (MHz)**. |
| LOCAL PTT | Una marca de verificación (✔) indica que la estación tiene actualmente la autoridad de PTT local. |
| STATION | El nombre del programa y el nombre de estación del cliente. Su propia estación aparece resaltada en azul. |
| TX ANT | La antena de transmisión que usa el slice TX de la estación. Muestra `----` si no hay datos disponibles. |
| TX FREQ (MHz) | La frecuencia de transmisión del slice TX de la estación, en MHz. Muestra `----` si no hay datos disponibles. |

## Sugerencias

- La tabla se actualiza automáticamente cada vez que un cliente se conecta, se desconecta o cambia su slice TX. No es necesario cerrar y volver a abrir el diálogo para ver los valores actuales.
- La fila de su propia estación aparece resaltada en un color distintivo, lo que facilita identificarse entre varios clientes.

## Solución de problemas

- **TX ANT o TX FREQ (MHz) muestra `----` para una estación** — El radio aún no ha reportado datos del slice TX para ese cliente. Espere un momento a que la tabla se actualice, o pida al otro operador que confirme que tiene un slice TX activo.
- **No aparece ninguna fila en la tabla Stations** — Es posible que multiFLEX no esté habilitado, o que no haya otros clientes conectados. Verifique que el botón Enable muestre "Enabled" y compruebe la conexión de red con el radio.

## Relacionado

- [Habilitar multiFLEX en el radio](enable-multiflex-on-the-radio.md)
- [Otorgar o revocar PTT local](grant-or-revoke-local-ptt.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
