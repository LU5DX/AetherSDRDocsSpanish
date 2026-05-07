# Ver todas las estaciones conectadas a esta FLEX

El panel multiFLEX (multiFLEX Dashboard) muestra cada cliente de SmartSDR que esté compartiendo su FLEX-8600 en ese momento. Úselo para comprobar qué estaciones están en línea, qué antena y frecuencia utiliza cada una y quién tiene el PTT local.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel multiFLEX Dashboard no está disponible cuando no hay ninguna radio conectada.
- multiFLEX debe estar habilitado en la radio. Si aún no lo está, consulte [Habilitar multiFLEX en la radio](../../features/multi-flex/enable-multiflex-on-the-radio.md).

## Pasos

1. Haga clic en `Settings > multiFLEX...`.
2. Se abre el diálogo **multiFLEX Dashboard**, que muestra la tabla de estaciones (Stations) con todos los clientes actualmente conectados.
3. Revise la tabla. Cada fila corresponde a una estación conectada.
4. Haga clic en `Close` cuando haya terminado.

## Qué hace cada control

| Control | Qué hace |
|---|---|
| Botón `Enabled` / `Disabled` | Muestra el estado actual de multiFLEX en la radio. Haga clic para activar o desactivar multiFLEX. |
| Tabla de estaciones (Stations) | Enumera todos los clientes multiFLEX conectados. Columnas: **LOCAL PTT**, **STATION**, **TX ANT**, **TX FREQ (MHz)**. Su propia estación aparece resaltada en azul. Una marca de verificación (✔) en la columna **LOCAL PTT** identifica qué estación tiene actualmente la autoridad de PTT. |
| `Enable` (PTT) | Aparece cuando hay más de una estación conectada y su estación no tiene el PTT en ese momento. Haga clic para reclamar la autoridad de PTT local para su estación. |
| Etiqueta Local PTT | Texto sobre el botón `Enable`. Si usted tiene el PTT, indica qué estación debe reclamarlo desde su propio cliente. Si usted no tiene el PTT, muestra el nombre de su estación y le solicita que lo reclame. |
| `Close` | Cierra el diálogo. |

## Consejos

- La columna STATION muestra el nombre del programa y el nombre de la estación en el formato `programa: estación`. Si el nombre de la estación coincide con el nombre del programa, solo se muestra el nombre del programa.
- TX ANT y TX FREQ (MHz) muestran `----` si la radio aún no ha informado esos datos para una estación determinada.
- La tabla se actualiza automáticamente a medida que las estaciones se conectan o desconectan. No es necesario volver a abrir el diálogo.
- Si solo hay una estación conectada, el botón `Enable` (PTT) y la etiqueta Local PTT están ocultos (no son necesarios cuando usted es el único cliente).

## Solución de problemas

- **`Settings > multiFLEX...` aparece atenuado o falta** — AetherSDR no está conectado a una radio. Conéctese a una radio primero y luego vuelva a abrir el menú.
- **La tabla de estaciones está vacía** — Es posible que multiFLEX esté deshabilitado. Haga clic en el botón `Disabled` para habilitarlo y luego compruebe si aparecen otras estaciones.
- **TX ANT y TX FREQ muestran `----` para todas las estaciones** — La radio aún no ha enviado el estado del slice para esos clientes. Espere un momento y la tabla se actualizará automáticamente.

## Relacionado

- [Descripción general del panel multiFLEX Dashboard](../../features/multi-flex/overview.md)
- [Habilitar multiFLEX en la radio](../../features/multi-flex/enable-multiflex-on-the-radio.md)
- [Conceder o revocar el PTT local](../../features/multi-flex/grant-or-revoke-local-ptt.md)
- [Comprobar qué antena y frecuencia usa cada estación transmisora](../../features/multi-flex/check-which-antenna-and-frequency-each-tx-station-is-using.md)
