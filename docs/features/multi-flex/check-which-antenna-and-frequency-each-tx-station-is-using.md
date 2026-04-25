# Verificar qué antena y frecuencia utiliza cada estación TX

Abra el multiFLEX Dashboard para ver de un vistazo qué antena TX y frecuencia de transmisión está usando en ese momento cada estación conectada.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El multiFLEX Dashboard requiere una conexión activa con el radio.
- multiFLEX debe estar habilitado en el radio. Si no lo está, la tabla de estaciones aparecerá vacía.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el multiFLEX Dashboard.
2. Consulte la tabla **Stations table**. Cada fila corresponde a un cliente conectado. Las columnas son:

   | Columna | Qué muestra |
   |---|---|
   | LOCAL PTT | Una marca de verificación si esa estación tiene actualmente la autoridad PTT. |
   | STATION | El nombre del programa y de la estación para ese cliente. Su propia estación aparece resaltada en azul. |
   | TX ANT | La antena de transmisión que esa estación tiene seleccionada. Muestra `----` si aún no se ha reportado. |
   | TX FREQ (MHz) | La frecuencia de transmisión en MHz, con tres decimales. Muestra `----` si aún no se ha reportado. |

3. Haga clic en `Close` cuando haya terminado.

## Consejos

- La tabla se actualiza automáticamente cada vez que una estación cambia su antena o frecuencia de transmisión. No es necesario volver a abrir el diálogo.
- La fila de su propia estación se distingue por el texto en azul en la columna STATION, lo que facilita comparar su configuración con la de otras estaciones.
- Los valores `----` en `TX ANT` y `TX FREQ (MHz)` indican que el radio aún no ha reportado ese dato para la estación, no que la estación esté inactiva.

## Relacionados

- [Habilitar multiFLEX en el radio](enable-multiflex-on-the-radio.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
- [Conceder o revocar PTT local](grant-or-revoke-local-ptt.md)
