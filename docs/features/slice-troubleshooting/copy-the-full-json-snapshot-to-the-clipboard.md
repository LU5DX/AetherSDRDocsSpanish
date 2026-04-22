# Copiar el Snapshot JSON Completo al Portapapeles

Copie el snapshot JSON completo de su slice, panadapter y estado de medidores al portapapeles para pegarlo en una solicitud de soporte, un issue de GitHub o una sesión de resolución de problemas asistida por IA.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo Slice Troubleshooting requiere una conexión activa con la radio.
- Abra el diálogo antes de copiar. Si aún no lo ha abierto, continúe con los pasos siguientes.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo Slice Troubleshooting.
2. Haga clic en la pestaña `JSON` para verificar el contenido del snapshot.
3. Si los datos parecen desactualizados o ha cambiado el estado del slice desde que abrió el diálogo, haga clic en `Refresh Snapshot` para releer el estado actual.
4. Haga clic en `Copy JSON`.
5. Pegue el contenido del portapapeles en su ticket de soporte, mensaje de chat o documento.

La etiqueta de estado en la parte inferior del diálogo muestra `JSON copied to clipboard.` cuando la copia se realiza correctamente.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `JSON` (pestaña) | Pestaña | Muestra el snapshot JSON completo de los slices y canales DAX. |
| `Refresh Snapshot` | Botón | Relee el estado del slice en el snapshot. Úselo después de cambiar la configuración del slice para asegurarse de que el JSON esté actualizado. |
| `Copy JSON` | Botón | Copia el JSON completo al portapapeles. |
| `Export JSON...` | Botón | Guarda el JSON en un archivo en lugar del portapapeles. |
| `Copy Summary` | Botón | Copia el resumen del problema en lenguaje claro al portapapeles en lugar del JSON sin procesar. |
| `Close` | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación. |

## Consejos

- El diálogo no consulta la radio automáticamente. Si cambia una configuración del slice después de abrir el diálogo, haga clic en `Refresh Snapshot` antes de hacer clic en `Copy JSON` para asegurarse de que el snapshot refleje el estado actual.
- Si necesita adjuntar el JSON como archivo en lugar de pegarlo directamente, use `Export JSON...` en su lugar.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar un snapshot del slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar el snapshot a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Leer una lista en lenguaje claro de problemas sospechados en el slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar el snapshot después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
