# Habilitar multiFLEX en la radio

Use el multiFLEX Dashboard para activar o desactivar multiFLEX en el FLEX-8600 conectado. Habilitar multiFLEX permite que varias estaciones cliente compartan la radio simultáneamente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El multiFLEX Dashboard requiere una conexión de radio activa.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el multiFLEX Dashboard.
2. Haga clic en el botón de alternancia ubicado en el centro del diálogo. Cuando multiFLEX está deshabilitado, el botón muestra **Disabled**. Cuando está habilitado, muestra **Enabled**.
3. Haga clic en **Close** para cerrar el diálogo.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Botón **Enabled** / **Disabled** | Activa o desactiva multiFLEX en la radio. La etiqueta y el color del botón reflejan el estado actual: **Enabled** (verde) o **Disabled** (rojo). |
| Tabla Stations | Lista todos los clientes multiFLEX conectados actualmente a la radio. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). |
| **Enable** (PTT) | Alterna la autoridad PTT local para esta estación. Solo se muestra cuando hay más de un cliente conectado y esta estación no tiene PTT en ese momento. |
| **Close** | Cierra el diálogo del multiFLEX Dashboard. |

## Consejos

- La entrada de su estación en la tabla Stations aparece resaltada en azul. Las demás estaciones conectadas se muestran con el color predeterminado.
- Cuando solo hay un cliente conectado, los controles de LOCAL PTT se ocultan automáticamente.

## Relacionado

- [Descripción general del multiFLEX Dashboard](overview.md)
- [Otorgar o revocar PTT local](grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia utiliza cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a este FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
