# Verificar qué antena y frecuencia usa cada estación transmisora

El panel multiFLEX muestra la antena y frecuencia de transmisión de cada estación que comparte el FLEX-8600. Úselo cuando necesite confirmar que otros operadores en la radio no interfieren con su frecuencia o antena de operación prevista.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- multiFLEX debe estar habilitado en la radio. Si la tabla de estaciones está vacía o la función no está activa, consulte [Habilitar multiFLEX en la radio](enable-multiflex-on-the-radio.md).

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el panel multiFLEX.
2. Observe la tabla de estaciones. Cada fila representa una estación conectada.
3. Lea la columna **TX ANT** para ver la antena que está usando esa estación para transmitir.
4. Lea la columna **TX FREQ (MHz)** para ver la frecuencia de transmisión de esa estación en MHz, mostrada con tres decimales.
5. Haga clic en Close cuando termine.

## Descripción de cada control

| Control | Descripción |
|---|---|
| Stations table | Lista todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). |
| Columna LOCAL PTT | Muestra una marca de verificación para la estación que tiene autoridad de PTT actualmente. |
| Columna STATION | Muestra el nombre del programa y el nombre de la estación para cada cliente. Su propia estación aparece resaltada en azul. |
| Columna TX ANT | Muestra la antena asignada al slice de TX de esa estación. Muestra `----` si aún no hay datos disponibles. |
| Columna TX FREQ (MHz) | Muestra la frecuencia de transmisión en MHz con tres decimales. Muestra `----` si aún no hay datos disponibles. |
| Enable | Habilita o deshabilita multiFLEX en la radio. |
| Enable (PTT) | Activa o desactiva la autoridad local de PTT para esta estación. |
| Close | Cierra el cuadro de diálogo. |

## Consejos

- La tabla se actualiza automáticamente cuando cambia el estado de algún cliente. No es necesario volver a abrir el cuadro de diálogo para ver los valores actualizados.
- Su propia estación se distingue por el texto azul en la columna STATION.
- Los valores de TX ANT y TX FREQ provienen del estado del slice de la radio. Si una estación acaba de conectarse, esas columnas pueden mostrar `----` brevemente hasta que la radio reporte los datos del slice.
- El cuadro de diálogo recuerda su tamaño y posición entre sesiones.

## Relacionados

- [Habilitar multiFLEX en la radio](enable-multiflex-on-the-radio.md)
- [Conceder o revocar PTT local](grant-or-revoke-local-ptt.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
