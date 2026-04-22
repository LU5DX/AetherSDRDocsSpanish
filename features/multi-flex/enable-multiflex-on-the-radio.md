# Activar multiFLEX en el equipo

multiFLEX permite que varias estaciones compartan un único FLEX-8600 de forma simultánea. Use esta página para activar o desactivar multiFLEX desde AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El multiFLEX Dashboard no está disponible sin una conexión activa al equipo.
- Su FLEX-8600 de FlexRadio debe ser compatible con multiFLEX. Confirme que la licencia de su equipo incluye la función multiFLEX antes de continuar.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el multiFLEX Dashboard.
2. Haga clic en el botón etiquetado como `Disabled` (que aparece en rojo cuando multiFLEX está desactivado) para activar multiFLEX en el equipo.
3. El botón cambia a `Enabled` (que aparece en verde) para confirmar que multiFLEX está ahora activo en el equipo.
4. Para desactivar multiFLEX, haga clic en `Enabled`. El botón vuelve a `Disabled`.
5. Haga clic en `Close` cuando haya terminado.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| `Disabled` / `Enabled` | Activa o desactiva multiFLEX en el equipo. La etiqueta y el color reflejan el estado actual: verde (`Enabled`) o rojo (`Disabled`). |
| Tabla de estaciones | Muestra todos los clientes multiFLEX conectados. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). |
| `Enable` (PTT) | Activa o desactiva la autoridad PTT local para esta estación. Solo es visible cuando otro cliente está conectado y tiene el PTT activo. |
| `Close` | Cierra el multiFLEX Dashboard. |

## Consejos

- La tabla de estaciones se actualiza automáticamente a medida que los clientes se conectan o desconectan. No es necesario volver a abrir el cuadro de diálogo para ver los cambios.
- La entrada correspondiente a su propia estación aparece resaltada en la tabla, lo que facilita su identificación entre varios clientes conectados.

## Relacionado

- [Descripción general del multiFLEX Dashboard](overview.md)
- [Conceder o revocar el PTT local](grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia usa cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
