# Verificar qué antena y frecuencia está usando cada estación transmisora

El panel multiFLEX Dashboard muestra la antena TX y la frecuencia TX de cada estación que comparte actualmente el FLEX-8600. Utilícelo cuando necesite confirmar que otros operadores en la radio no están interfiriendo con su frecuencia de operación o antena prevista.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- multiFLEX debe estar habilitado en la radio. Si la tabla de estaciones está vacía o la función no está activa, consulte [Enable multiFLEX on the radio](enable-multiflex-on-the-radio.md).

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el panel multiFLEX Dashboard.
2. Observe la tabla Stations. Cada fila representa una estación conectada.
3. Lea la columna **TX ANT** para conocer la antena en la que esa estación está transmitiendo.
4. Lea la columna **TX FREQ (MHz)** para conocer la frecuencia de transmisión de esa estación en MHz, mostrada con tres decimales.
5. Haga clic en Close cuando termine.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Stations table | Enumera todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). |
| LOCAL PTT column | Muestra una marca de verificación en la estación que actualmente tiene autoridad de PTT. |
| STATION column | Muestra el nombre del programa y el nombre de la estación para cada cliente. Su propia estación aparece resaltada en azul. |
| TX ANT column | Muestra la antena asignada al slice TX de esa estación. Muestra `----` si aún no hay datos disponibles. |
| TX FREQ (MHz) column | Muestra la frecuencia de transmisión en MHz con tres decimales. Muestra `----` si aún no hay datos disponibles. |
| Close | Cierra el cuadro de diálogo. |

## Consejos

- La tabla se actualiza automáticamente cuando cambia el estado de algún cliente. No necesita volver a abrir el cuadro de diálogo para ver los valores actualizados.
- La fila de su propia estación se distingue por el texto azul en la columna STATION.
- Los valores de TX ANT y TX FREQ provienen del estado del slice de la radio. Si una estación acaba de conectarse, esas columnas pueden mostrar brevemente `----` hasta que la radio informe los datos del slice.

## Relacionado

- [Enable multiFLEX on the radio](enable-multiflex-on-the-radio.md)
- [Grant or revoke local PTT](grant-or-revoke-local-ptt.md)
- [See all stations connected to this FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
