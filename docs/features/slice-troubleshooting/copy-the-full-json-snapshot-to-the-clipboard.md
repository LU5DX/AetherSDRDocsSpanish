# Copiar el snapshot JSON completo al portapapeles

Copie el snapshot JSON completo de su slice, DAX y estado del radio al portapapeles para pegarlo en un hilo de soporte, reporte de error o sesión de diagnóstico asistida por IA.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión de radio activa.
- Abra el diálogo Slice Troubleshooting mediante `Help > Slice Troubleshooting...`.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña **JSON** para confirmar que el snapshot contiene datos.
3. Si los datos parecen desactualizados, haga clic en **Refresh Snapshot** para releer el estado actual del slice.
4. Haga clic en **Copy JSON**.
5. La etiqueta de estado en la parte inferior del diálogo muestra `Copied to clipboard` cuando la operación se completa con éxito.
6. Pegue el contenido del portapapeles en su hilo de soporte, chat o documento.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** (pestaña) | Pestaña | Lista de viñetas en lenguaje sencillo con los problemas detectados. |
| **JSON** (pestaña) | Pestaña | Snapshot JSON completo de los slices y canales DAX. |
| **Refresh Snapshot** | Botón | Relee el estado del slice en el snapshot. |
| **Copy Summary** | Botón | Copia el texto del resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia el snapshot JSON completo al portapapeles. |
| **Export JSON...** | Botón | Guarda el JSON en un archivo en lugar del portapapeles. |
| **Close** | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación. |

## Consejos

- Si desea compartir tanto un resumen en lenguaje sencillo como el JSON sin procesar, use primero **Copy Summary** y luego **Copy JSON** por separado — cada botón sobreescribe el portapapeles.
- Para guardar el JSON como archivo adjunto en lugar de pegarlo directamente, use **Export JSON...** en su lugar.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar un snapshot de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar el snapshot a un archivo para adjuntar a un reporte de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Leer una lista en lenguaje sencillo de problemas detectados en el slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar el snapshot después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
