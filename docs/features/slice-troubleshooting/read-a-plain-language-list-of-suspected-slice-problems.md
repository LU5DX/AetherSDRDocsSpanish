# Leer una lista en lenguaje sencillo de los problemas detectados en un slice

El diálogo Slice Troubleshooting analiza el estado actual del slice (canal de recepción) y presenta los problemas detectados en lenguaje sencillo. Úselo cuando un slice se comporte de manera inesperada y desee un resumen rápido antes de revisar la configuración o contactar al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión activa con el radio.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`.
2. En el diálogo Slice Troubleshooting, haga clic en la pestaña `Issue Summary`.
3. Lea la lista de problemas detectados. Cada elemento describe un posible problema, como ausencia de audio, silencio (mute) bloqueado o antena no detectada.
4. Si la lista no refleja el estado actual del radio, haga clic en `Refresh Snapshot` para volver a leer el estado del slice y luego revise nuevamente la pestaña `Issue Summary`.
5. Para compartir el resumen, haga clic en `Copy Summary`. El texto se copia al portapapeles. La etiqueta de estado en la parte inferior del diálogo confirma el resultado.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `Issue Summary` | Pestaña | Muestra una lista en lenguaje sencillo de los problemas detectados. |
| `JSON` | Pestaña | Muestra la instantánea JSON completa de los slices y canales DAX. |
| `Refresh Snapshot` | Botón | Vuelve a leer el estado del slice en la instantánea. |
| `Copy Summary` | Botón | Copia el texto del resumen de problemas al portapapeles. |
| `Copy JSON` | Botón | Copia la instantánea JSON completa al portapapeles. |
| `Export JSON...` | Botón | Guarda la instantánea JSON en un archivo. |
| `Close` | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación, por ejemplo "Copied to clipboard". |

## Consejos

- El diálogo no consulta el radio de forma continua. Si cambia la configuración del slice después de abrir el diálogo, haga clic en `Refresh Snapshot` antes de volver a leer la pestaña `Issue Summary`.
- La pestaña `Issue Summary` es adecuada para pegar en reportes de problemas de GitHub. Para diagnóstico asistido por inteligencia artificial, utilice la pestaña `JSON`.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar una instantánea del slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un reporte de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
