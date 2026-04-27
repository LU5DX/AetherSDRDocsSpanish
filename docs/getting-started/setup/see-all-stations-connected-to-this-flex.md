# Ver todas las estaciones conectadas a este FLEX

El panel multiFLEX Dashboard muestra todos los clientes SmartSDR que comparten actualmente su FLEX-8600. Úselo para verificar qué estaciones están en línea, qué antena y frecuencia usa cada una, y quién tiene el control local de PTT.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel multiFLEX Dashboard no está disponible cuando no hay ninguna radio conectada.
- multiFLEX debe estar habilitado en la radio. Si aún no está habilitado, consulte [Habilitar multiFLEX en la radio](../../features/multi-flex/enable-multiflex-on-the-radio.md).

## Pasos

1. Haga clic en `Settings > multiFLEX...`.
2. Se abre el diálogo **multiFLEX Dashboard**, que muestra la tabla Stations con todos los clientes conectados en ese momento.
3. Revise la tabla. Cada fila corresponde a una estación conectada.
4. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control | Función |
|---|---|
| Botón `Enabled` / `Disabled` | Muestra el estado actual de multiFLEX en la radio. Haga clic para activar o desactivar multiFLEX. |
| Tabla Stations | Lista todos los clientes multiFLEX conectados. Columnas: **LOCAL PTT**, **STATION**, **TX ANT**, **TX FREQ (MHz)**. Su propia estación aparece resaltada en azul. Una marca de verificación (✔) en la columna **LOCAL PTT** identifica qué estación tiene actualmente la autoridad PTT. |
| `Enable` (PTT) | Aparece cuando hay más de una estación conectada y su estación no tiene el control PTT en ese momento. Haga clic para reclamar la autoridad PTT local para su estación. |
| Etiqueta Local PTT | Texto que aparece encima del botón `Enable`. Cuando usted tiene el control PTT, identifica la estación que debe reclamar el PTT desde su propio cliente. Cuando usted no tiene el control PTT, muestra el nombre de su estación y le indica que lo reclame. |
| `Close` | Cierra el diálogo. |

## Consejos

- La columna STATION muestra el nombre del programa y el nombre de la estación con el formato `program: station`. Si el nombre de la estación coincide con el nombre del programa, solo se muestra el nombre del programa.
- TX ANT y TX FREQ (MHz) muestran `----` si la radio aún no ha reportado esos datos para una estación determinada.
- La tabla se actualiza automáticamente a medida que las estaciones se conectan o desconectan. No es necesario volver a abrir el diálogo.
- Si solo hay una estación conectada, el botón `Enable` (PTT) y la etiqueta Local PTT están ocultos — no son necesarios cuando usted es el único cliente.

## Solución de problemas

- **`Settings > multiFLEX...` aparece en gris o no está disponible** — AetherSDR no está conectado a una radio. Conéctese a una radio primero y luego vuelva a abrir el menú.
- **La tabla Stations está vacía** — Es posible que multiFLEX esté deshabilitado. Haga clic en el botón `Disabled` para habilitarlo y luego verifique si aparecen otras estaciones.
- **TX ANT y TX FREQ muestran `----` para todas las estaciones** — La radio aún no ha enviado el estado del slice (canal de recepción) para esos clientes. Espere un momento y la tabla se actualizará automáticamente.

## Relacionados

- [Descripción general del panel multiFLEX Dashboard](../../features/multi-flex/overview.md)
- [Habilitar multiFLEX en la radio](../../features/multi-flex/enable-multiflex-on-the-radio.md)
- [Otorgar o revocar el control PTT local](../../features/multi-flex/grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia usa cada estación TX](../../features/multi-flex/check-which-antenna-and-frequency-each-tx-station-is-using.md)
