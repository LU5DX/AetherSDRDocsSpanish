# Verificar qué antena y frecuencia usa cada estación TX

El panel multiFLEX muestra la antena TX y la frecuencia TX de cada estación que comparte el FLEX-8600 en ese momento. Utilícelo cuando necesite confirmar que otros operadores en la radio no están en conflicto con la frecuencia de operación o la antena que usted tiene previsto usar.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- multiFLEX debe estar habilitado en la radio. Si la tabla Stations está vacía o la función no está activa, consulte [Habilitar multiFLEX en la radio](enable-multiflex-on-the-radio.md).

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el panel multiFLEX.
2. Observe la tabla Stations. Cada fila corresponde a una estación conectada.
3. Lea la columna **TX ANT** para ver la antena en la que transmite esa estación.
4. Lea la columna **TX FREQ (MHz)** para ver la frecuencia de transmisión de esa estación en MHz, expresada con tres decimales.
5. Haga clic en Close cuando termine.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Tabla Stations | Muestra todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). |
| Columna LOCAL PTT | Muestra una marca de verificación en la estación que actualmente tiene la autoridad PTT. |
| Columna STATION | Muestra el nombre del programa y el nombre de la estación de cada cliente. Su propia estación aparece resaltada en azul. |
| Columna TX ANT | Muestra la antena asignada al slice TX de esa estación. Muestra `----` si aún no hay datos disponibles. |
| Columna TX FREQ (MHz) | Muestra la frecuencia de transmisión en MHz con tres decimales. Muestra `----` si aún no hay datos disponibles. |
| Close | Cierra el cuadro de diálogo. |

## Sugerencias

- La tabla se actualiza automáticamente cuando cambia el estado de cualquier cliente. No es necesario volver a abrir el cuadro de diálogo para ver los valores actualizados.
- La fila de su propia estación se distingue por el texto en azul en la columna STATION.
- Los valores de TX ANT y TX FREQ provienen del estado del slice de la radio. Si una estación acaba de conectarse, esas columnas pueden mostrar `----` brevemente hasta que la radio informe los datos del slice.

## Relacionados

- [Habilitar multiFLEX en la radio](enable-multiflex-on-the-radio.md)
- [Otorgar o revocar PTT local](grant-or-revoke-local-ptt.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
