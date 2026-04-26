# Leer una lista en lenguaje sencillo de posibles problemas en el slice

El diálogo Slice Troubleshooting analiza el estado actual del slice (canal de recepción) y muestra un resumen en lenguaje sencillo de los problemas detectados — como audio ausente, silenciamiento bloqueado o antena no disponible — para que pueda identificar rápidamente qué ocurre sin necesidad de leer datos sin procesar.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión activa con el radio.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña **Issue Summary**.
3. Lea la lista de puntos con los problemas detectados.
4. Si ha modificado la configuración del slice desde que abrió el diálogo, haga clic en **Refresh Snapshot** para volver a leer el estado actual antes de revisar el resumen nuevamente.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** | Pestaña | Muestra una lista de puntos en lenguaje sencillo con los problemas detectados. |
| **JSON** | Pestaña | Muestra el snapshot JSON completo de los slices y canales DAX. |
| **Refresh Snapshot** | Botón | Vuelve a leer el estado del slice en el snapshot. |
| **Copy Summary** | Botón | Copia el texto del resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia el snapshot JSON completo al portapapeles. |
| **Export JSON...** | Botón | Guarda el snapshot JSON en un archivo. |
| **Close** | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard"). |

## Sugerencias

- Si la pestaña **Issue Summary** no muestra problemas pero el audio sigue sin estar disponible, haga clic en **Refresh Snapshot** y vuelva a verificar. El snapshot refleja el estado en el momento en que fue capturado por última vez, no de forma continua.
- Use **Copy Summary** para pegar la lista de problemas directamente en un mensaje de soporte o en una publicación de un foro.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Actualizar el snapshot tras cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Capturar un snapshot del slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Copiar el snapshot JSON completo al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar el snapshot a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
