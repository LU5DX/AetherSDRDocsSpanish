# Copiar el snapshot JSON completo al portapapeles

El diálogo Slice Troubleshooting captura un snapshot JSON de cada slice (canal de recepción/transmisión), panadapter (visualizador panorámico), transverter y canal DAX. Esta página explica cómo copiar ese snapshot al portapapeles para pegarlo en un ticket de soporte, una publicación en un foro o un reporte de error.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo requiere una conexión activa con la radio.
- Si el estado del slice ha cambiado desde la última vez que abrió el diálogo, haga clic en "Refresh Snapshot" antes de copiar para asegurarse de que los datos estén actualizados.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña `JSON`.
3. Haga clic en `Copy JSON`.
4. Confirme que la etiqueta de estado muestre `Copied to clipboard`.
5. Pegue el contenido en la aplicación de destino.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `JSON` (pestaña) | Pestaña | Muestra el snapshot JSON completo de los slices y canales DAX. |
| `Issue Summary` (pestaña) | Pestaña | Muestra una lista con viñetas, en lenguaje simple, de los problemas detectados. |
| `Refresh Snapshot` | Botón | Vuelve a leer el estado actual del slice en el snapshot. Haga clic aquí después de realizar cualquier cambio en el slice antes de copiar. |
| `Copy JSON` | Botón | Copia el snapshot JSON completo al portapapeles. |
| `Copy Summary` | Botón | Copia el texto del resumen de problemas al portapapeles en lugar del JSON. |
| `Export JSON...` | Botón | Guarda el snapshot JSON en un archivo. |
| `Close` | Botón | Cierra el diálogo. |

## Consejos

- Si desea solo un resumen de problemas en lenguaje simple en lugar del JSON completo, use `Copy Summary` en la pestaña `Issue Summary`.
- Para obtener el snapshot más preciso, realice primero cualquier cambio en la configuración del slice, luego haga clic en `Refresh Snapshot` y después en `Copy JSON`.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar un snapshot de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar el snapshot a un archivo para adjuntar a un reporte de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar el snapshot después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje simple de posibles problemas de slice](read-a-plain-language-list-of-suspected-slice-problems.md)
