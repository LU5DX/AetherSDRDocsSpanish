# Comprobar qué antena y frecuencia utiliza cada estación TX

El panel multiFLEX Dashboard muestra la antena TX y la frecuencia TX de cada estación que esté compartiendo el FLEX-8600. Utilícelo cuando necesite confirmar que otros operadores en la radio no están interfiriendo con la frecuencia o antena en la que desea operar.

## Antes de empezar

- AetherSDR debe estar conectado a la radio.
- multiFLEX debe estar habilitado en la radio. Si la tabla de estaciones está vacía o la función no está activa, consulte [Habilitar multiFLEX en la radio](enable-multiflex-on-the-radio.md).

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el panel multiFLEX Dashboard.
2. Observe la tabla de estaciones. Cada fila corresponde a una estación conectada.
3. Lea la columna **TX ANT** para conocer la antena en la que está transmitiendo esa estación.
4. Lea la columna **TX FREQ (MHz)** para conocer la frecuencia de transmisión de esa estación en MHz, mostrada con tres decimales.
5. Haga clic en Close cuando haya terminado.

## Función de cada control

| Control | Descripción |
|---|---|
| Stations table | Enumera todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz) y botón Disconnect. |
| Columna LOCAL PTT | Muestra una marca de verificación para la estación que tiene la autoridad PTT actual. |
| Columna STATION | Muestra el nombre del programa y el nombre de la estación de cada cliente. Su propia estación aparece resaltada en azul. Si el nombre de la estación es igual al nombre del programa, solo se muestra el nombre del programa. Si ambos están vacíos, muestra `client 0x{HANDLE}`. |
| Columna TX ANT | Muestra la antena asignada al slice TX de esa estación. Muestra `----` si aún no hay datos disponibles. |
| Columna TX FREQ (MHz) | Muestra la frecuencia de transmisión en MHz con tres decimales. Muestra `----` si aún no hay datos disponibles. |
| Botón Disconnect | Desconecta al cliente correspondiente de multiFLEX. El botón se vuelve amarillo después de hacer clic para indicar que la desconexión está pendiente y luego vuelve a la normalidad cuando la radio confirma la desconexión. Este botón está deshabilitado para su propia estación. |
| Enable | Habilita o deshabilita multiFLEX en la radio. |
| Enable (PTT) | Alterna la autoridad PTT local para esta estación. |
| Close | Cierra el cuadro de diálogo. |

## Consejos

- La tabla se actualiza automáticamente cuando cambia el estado de algún cliente. No es necesario volver a abrir el cuadro de diálogo para ver los valores actualizados.
- La fila de su propia estación se distingue por el texto azul en la columna STATION.
- Los valores de TX ANT y TX FREQ provienen del estado del slice de la radio. Si una estación acaba de conectarse, esas columnas pueden mostrar `----` brevemente hasta que la radio informe los datos del slice.
- El cuadro de diálogo recuerda su tamaño y posición entre sesiones.
- Después de hacer clic en el botón Disconnect para un cliente, el botón se vuelve amarillo hasta que la radio confirme la desconexión. Si el cliente permanece en la tabla, el botón vuelve a la normalidad, lo que permite reintentar si es necesario.

## Relacionados

- [Habilitar multiFLEX en la radio](enable-multiflex-on-the-radio.md)
- [Conceder o revocar PTT local](grant-or-revoke-local-ptt.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
