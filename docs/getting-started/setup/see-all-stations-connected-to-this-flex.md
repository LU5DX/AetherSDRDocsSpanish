# Ver todas las estaciones conectadas a este FLEX

El multiFLEX Dashboard muestra todos los clientes que comparten actualmente su radio Flex y lo que cada uno está haciendo. Úselo para confirmar quién está conectado, qué antena utiliza cada uno y en qué frecuencia está transmitiendo.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El multiFLEX Dashboard requiere una conexión activa con el radio.
- multiFLEX debe estar habilitado en el radio. Si el panel no muestra estaciones, verifique que multiFLEX esté activo (consulte [Habilitar multiFLEX en el radio](../../features/multi-flex/enable-multiflex-on-the-radio.md)).

## Pasos

1. Haga clic en `Settings > multiFLEX...`.
2. El **multiFLEX Dashboard** se abre y llena inmediatamente la **Stations table** con todos los clientes conectados.
3. Lea la tabla. Cada fila corresponde a un cliente. Las columnas son **LOCAL PTT**, **STATION**, **TX ANT** y **TX FREQ (MHz)**. Su propia estación aparece resaltada en azul.
4. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Botón `Enabled` / `Disabled` | Activa o desactiva multiFLEX en el radio. La etiqueta del botón refleja el estado actual. |
| **Stations table** | Lista todos los clientes multiFLEX conectados. Columnas: **LOCAL PTT** (marca de verificación si esa estación tiene PTT activo), **STATION** (programa y nombre de la estación), **TX ANT** (antena de transmisión), **TX FREQ (MHz)** (frecuencia de transmisión). Muestra `----` cuando un valor no está disponible. |
| `Enable` (PTT) | Solicita autoridad PTT local para su estación. Aparece solo cuando hay otro cliente conectado y su estación no tiene PTT en ese momento. |
| `Close` | Cierra el cuadro de diálogo. |

## Consejos

- La tabla se actualiza automáticamente cuando los clientes se conectan, se desconectan o cambian de estado. No es necesario volver a abrir el cuadro de diálogo para ver los cambios.
- La fila de su propia estación se muestra en un color diferenciado para que pueda localizarla rápidamente en una lista con muchas entradas.
- El botón `Enable` (PTT) está oculto cuando su estación ya tiene PTT activo o cuando usted es el único cliente conectado.

## Relacionados

- [Descripción general del multiFLEX Dashboard](../../features/multi-flex/overview.md)
- [Habilitar multiFLEX en el radio](../../features/multi-flex/enable-multiflex-on-the-radio.md)
- [Conceder o revocar PTT local](../../features/multi-flex/grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia usa cada estación TX](../../features/multi-flex/check-which-antenna-and-frequency-each-tx-station-is-using.md)
