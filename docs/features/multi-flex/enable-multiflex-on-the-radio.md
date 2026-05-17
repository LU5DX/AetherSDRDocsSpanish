# Habilitar multiFLEX en la radio

Use el Panel multiFLEX para activar o desactivar multiFLEX en la FLEX-8600 conectada. Habilitar multiFLEX permite que múltiples estaciones cliente compartan la radio simultáneamente. El diálogo recuerda su posición y tamaño entre sesiones.

## Antes de empezar

- AetherSDR debe estar conectado a una radio FLEX-8600. El Panel multiFLEX requiere una conexión activa con la radio.

## Pasos

1. Haga clic en `Settings > multiFLEX...` para abrir el Panel multiFLEX.
2. Haga clic en el botón **Enable** para activar o desactivar multiFLEX en la radio. Cuando multiFLEX está deshabilitado, el botón muestra **Enable**. Cuando está habilitado, muestra **Disable**.
3. Haga clic en **Close** para cerrar el diálogo.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Botón **Enable** | Activa o desactiva multiFLEX en la radio. La etiqueta del botón refleja el estado actual: **Disable** cuando multiFLEX está activo, **Enable** cuando está desactivado. |
| Tabla de estaciones | Enumera cada cliente multiFLEX conectado actualmente a la radio. Columnas: LOCAL PTT, STATION, TX ANT, TX FREQ (MHz). |
| **Enable** (PTT) | Activa o desactiva la autoridad PTT local para esta estación. Solo se muestra cuando hay más de un cliente conectado y esta estación no posee el PTT actualmente. |
| **Close** | Cierra el diálogo del Panel multiFLEX. |

## Consejos

- La entrada de su estación en la tabla de estaciones se resalta en azul. Las demás estaciones conectadas aparecen en el color predeterminado.
- Cuando solo hay un cliente conectado, los controles LOCAL PTT se ocultan automáticamente.
- El diálogo restaura automáticamente su posición y tamaño anteriores al reabrirse dentro de la misma sesión.

## Relacionados

- [Resumen del Panel multiFLEX](overview.md)
- [Conceder o revocar PTT local](grant-or-revoke-local-ptt.md)
- [Verificar qué antena y frecuencia está usando cada estación TX](check-which-antenna-and-frequency-each-tx-station-is-using.md)
- [Ver todas las estaciones conectadas a esta FLEX](../../getting-started/setup/see-all-stations-connected-to-this-flex.md)
