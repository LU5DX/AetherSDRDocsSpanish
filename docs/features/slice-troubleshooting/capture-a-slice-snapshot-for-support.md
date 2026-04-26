# Capturar una instantánea de slice para soporte

El diálogo Slice Troubleshooting captura una instantánea JSON puntual de cada slice y canal DAX, y resume los problemas detectados en lenguaje sencillo. Úselo al reportar un error o solicitar soporte — puede copiar o exportar los datos para compartirlos con el equipo de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo requiere una conexión de radio activa.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo Slice Troubleshooting.
2. La instantánea se toma automáticamente al abrir el diálogo. Revise la pestaña **Issue Summary** para ver una lista con los problemas detectados (audio faltante, silenciamiento bloqueado, antena faltante y similares).
3. Para ver los datos sin procesar, haga clic en la pestaña **JSON**.
4. Si ha cambiado el estado del slice desde que abrió el diálogo, haga clic en `Refresh Snapshot` para volver a leer el estado actual.
5. Para compartir el texto del resumen, haga clic en `Copy Summary`. El texto se coloca en el portapapeles. La etiqueta de estado confirma "Copied to clipboard".
6. Para compartir el JSON completo, haga clic en `Copy JSON`. Péguelo en su ticket de soporte o correo electrónico.
7. Para guardar el JSON en un archivo (para adjuntarlo a un informe de error), haga clic en `Export JSON...` y elija una ubicación de guardado en el diálogo de archivos.
8. Haga clic en `Close` cuando haya terminado.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** | Pestaña | Lista en lenguaje sencillo con los problemas detectados. |
| **JSON** | Pestaña | Instantánea JSON completa de los slices y canales DAX. |
| `Refresh Snapshot` | Botón | Vuelve a leer el estado del slice en la instantánea. Úselo después de cambiar la configuración del slice. |
| `Copy Summary` | Botón | Copia el texto del resumen de problemas al portapapeles. |
| `Copy JSON` | Botón | Copia la instantánea JSON completa al portapapeles. |
| `Export JSON...` | Botón | Abre un diálogo de guardado y escribe el JSON en un archivo. |
| `Close` | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard"). |

## Consejos

- Tome la instantánea antes de cambiar cualquier cosa. Si reconfigura un slice para solucionar un problema, haga clic en `Refresh Snapshot` una segunda vez después del cambio para tener una instantánea antes y después que pueda comparar.
- `Export JSON...` produce un archivo que puede adjuntar directamente a un informe de error sin necesidad de pegar grandes cantidades de texto.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje sencillo de los problemas de slice detectados](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
