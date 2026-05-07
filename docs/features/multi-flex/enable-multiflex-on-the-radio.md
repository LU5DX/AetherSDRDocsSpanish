# Activar multiFLEX en la radio

Use el Panel multiFLEX para activar o desactivar multiFLEX en la FLEX-8600 conectada. Al habilitar multiFLEX, varias estaciones cliente pueden compartir la radio simultáneamente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El Panel multiFLEX requiere una conexión activa con la radio.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el Panel multiFLEX.
2. Haga clic en el botón de alternancia en el centro del diálogo. Cuando multiFLEX está deshabilitado, el botón muestra **Disabled**. Cuando está habilitado, muestra **Enabled**.
3. Haga clic en **Close** para cerrar el diálogo.

## Funcionamiento de cada control

| Control | Comportamiento |
|---|---|
| Botón **Enabled** / **Disabled** | Activa o desactiva multiFLEX en la radio. La etiqueta y el color del botón reflejan el estado actual: **Enabled** (verde) o **Disabled** (rojo). |
| Tabla de estaciones | Enumera cada cliente multiFLEX conectado actualmente a la radio. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). |
| **Enable** (PTT) | Activa la autoridad PTT local para esta estación. Solo se muestra cuando hay más de un cliente conectado y esta estación no posee el PTT actualmente. |
| **Close** | Cierra el diálogo del Panel multiFLEX. |

## Consejos

- La entrada de su estación en la tabla de estaciones se resalta en azul. Las demás estaciones conectadas aparecen en el color predeterminado.
- Cuando solo hay un cliente conectado, los controles LOCAL PTT se ocultan automáticamente.

## Relacionado

- [Descripción general del Panel multiFLEX](overview.md)
- [Conceder o revocar PTT local](grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia usa cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a esta FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
