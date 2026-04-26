# Habilitar multiFLEX en el radio

multiFLEX permite que varias estaciones compartan un único FLEX-8600 de forma simultánea. Esta página explica cómo habilitar o deshabilitar multiFLEX desde AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El multiFLEX Dashboard no está disponible sin una conexión activa al radio.
- Se requiere acceso de operador al FLEX-8600. Habilitar multiFLEX es una configuración global del radio que afecta a todas las estaciones conectadas.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el multiFLEX Dashboard.
2. En la parte superior del diálogo, localice el botón de habilitación/deshabilitación. Cuando multiFLEX está desactivado, el botón muestra "Disabled". Cuando está activado, muestra "Enabled".
3. Haga clic en el botón para activar o desactivar multiFLEX. La etiqueta y el color del botón se actualizan de inmediato para reflejar el nuevo estado.
4. Haga clic en `Close` para cerrar el diálogo.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Botón Enable / Disable | Activa o desactiva multiFLEX en el radio. Muestra "Enabled" (verde) cuando está activo y "Disabled" (rojo) cuando está inactivo. |
| Tabla Stations | Lista todos los clientes multiFLEX conectados en ese momento. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). |
| Enable (PTT) | Activa o desactiva la autoridad PTT local para esta estación. Aparece únicamente cuando hay más de una estación conectada y esta estación no tiene el PTT en ese momento. |
| Close | Cierra el multiFLEX Dashboard. |

## Consejos

- Cuando solo hay una estación conectada, los controles de PTT están ocultos. Aparecen automáticamente en cuanto se conecta una segunda estación.
- Su propia estación aparece resaltada en la tabla Stations para que pueda identificarla entre los demás clientes conectados.
- Al hacer clic en el botón de habilitación/deshabilitación, el cambio surte efecto de inmediato en el radio. No es necesario desconectarse y volver a conectarse.

## Temas relacionados

- [Descripción general del multiFLEX Dashboard](overview.md)
- [Otorgar o revocar el PTT local](grant-or-revoke-local-ptt.md)
- [Verificar la antena y la frecuencia de cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
