# Verificar qué antena y frecuencia usa cada estación TX

El Panel multiFLEX muestra una tabla en tiempo real de todas las estaciones que comparten el radio FLEX, incluyendo la antena TX y la frecuencia de transmisión que cada estación está usando en ese momento. Úselo cuando necesite confirmar qué están haciendo otros operadores en el mismo radio antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Panel multiFLEX requiere una conexión activa con el radio.
- multiFLEX debe estar habilitado en el radio. Si el panel no muestra ninguna estación, consulte [Habilitar multiFLEX en el radio](enable-multiflex-on-the-radio.md).

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el Panel multiFLEX.
2. Lea la tabla Stations. Cada fila corresponde a un cliente conectado.
3. Busque la columna **TX ANT** para ver la antena que usa cada estación, y la columna **TX FREQ (MHz)** para ver su frecuencia de transmisión actual.
4. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Tabla Stations | Lista todos los clientes multiFLEX conectados. Columnas: **LOCAL PTT**, **STATION**, **TX ANT**, **TX FREQ (MHz)**. |
| Columna **LOCAL PTT** | Muestra una marca de verificación para la estación que tiene actualmente la autoridad PTT. |
| Columna **STATION** | Muestra el nombre del programa y el nombre de la estación para cada cliente. Su propia estación aparece resaltada en azul. |
| Columna **TX ANT** | Muestra la antena de transmisión seleccionada por cada estación. Muestra `----` si no hay datos de antena disponibles. |
| Columna **TX FREQ (MHz)** | Muestra la frecuencia de transmisión de cada estación en MHz, con tres decimales. Muestra `----` si no hay datos de frecuencia disponibles. |

## Sugerencias

- La tabla se actualiza automáticamente cuando las estaciones cambian de frecuencia o antena. No es necesario volver a abrir el diálogo para ver los valores actuales.
- La fila de su propia estación se muestra en un color diferenciado, lo que facilita ubicar su entrada entre varios clientes.

## Solución de problemas

- **TX ANT o TX FREQ muestra `----` para una estación** — El radio aún no ha reportado el estado del slice (receptor virtual) para ese cliente. Espere un momento y la tabla se actualizará automáticamente cuando lleguen los datos.
- **No aparecen filas en la tabla Stations** — Es posible que multiFLEX no esté habilitado. Haga clic en `Enable` en la parte superior del diálogo para habilitarlo, o consulte [Habilitar multiFLEX en el radio](enable-multiflex-on-the-radio.md).

## Relacionados

- [Habilitar multiFLEX en el radio](enable-multiflex-on-the-radio.md)
- [Otorgar o revocar PTT local](grant-or-revoke-local-ptt.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
