# Activar multiFLEX en el radio

multiFLEX permite que varias estaciones compartan un único FLEX-8600 de forma simultánea. Esta página explica cómo activar o desactivar multiFLEX desde AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El multiFLEX Dashboard no está disponible sin una conexión activa al radio.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el multiFLEX Dashboard.
2. Haga clic en el botón de alternancia ubicado en la parte superior del cuadro de diálogo. Cuando multiFLEX está desactivado, el botón muestra "Disabled". Cuando está activado, muestra "Enabled".
3. Haga clic en Close para cerrar el cuadro de diálogo.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Alternancia Enable / Disable | Activa o desactiva multiFLEX en el radio. La etiqueta del botón refleja el estado actual: "Enabled" (verde) o "Disabled" (rojo). Al hacer clic, cambia al estado opuesto. |
| Tabla Stations | Lista todos los clientes multiFLEX conectados actualmente al radio. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). |
| Enable (PTT) | Alterna la autoridad PTT local para esta estación. Solo es visible cuando hay más de una estación conectada y esta estación no tiene el PTT en ese momento. |
| Close | Cierra el cuadro de diálogo multiFLEX Dashboard. |

## Sugerencias

- La tabla Stations aparece vacía hasta que al menos un cliente se conecta. Si usted es el único cliente, los controles LOCAL PTT y Enable (PTT) están ocultos.
- La entrada de su propia estación aparece resaltada en la tabla Stations, lo que facilita identificarla entre los demás clientes conectados.

## Solución de problemas

- **"multiFLEX..." aparece atenuado en el menú Settings** — AetherSDR no está conectado al radio. Establezca una conexión con el radio y luego regrese a `Settings > multiFLEX...`.
- **El botón muestra "Enabled" pero otras estaciones no pueden conectarse** — Las licencias de multiFLEX y la disponibilidad de ranuras son gestionadas por el firmware del radio, no por AetherSDR. Verifique que el firmware del FLEX-8600 sea la versión 4.1.5 y que las ranuras multiFLEX disponibles no se hayan agotado.

## Relacionado

- [Descripción general del multiFLEX Dashboard](overview.md)
- [Otorgar o revocar el PTT local](grant-or-revoke-local-ptt.md)
- [Consultar qué antena y frecuencia usa cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
