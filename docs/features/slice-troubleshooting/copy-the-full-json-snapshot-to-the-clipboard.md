# Copiar el snapshot JSON completo al portapapeles

Copie el snapshot JSON sin procesar desde el diálogo Slice Troubleshooting al portapapeles para pegarlo en un informe de error, una publicación en el foro o un ticket de soporte.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo requiere una conexión de radio activa.
- Abra el diálogo Slice Troubleshooting mediante `Help > Slice Troubleshooting...`.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en `Refresh Snapshot` para asegurarse de que el snapshot refleja el estado actual del slice.
3. Haga clic en `Copy JSON`.
4. Revise la etiqueta de estado en la parte inferior del diálogo. Mostrará `Copied to clipboard` cuando la operación sea exitosa.
5. Pegue el contenido del portapapeles en el documento de destino.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `JSON (tab)` | Pestaña | Muestra el snapshot JSON completo de los slices y los canales DAX. |
| `Issue Summary (tab)` | Pestaña | Muestra una lista de viñetas en lenguaje sencillo con los problemas detectados. |
| `Refresh Snapshot` | Botón | Vuelve a leer el estado del slice en el snapshot. Haga clic antes de copiar para asegurarse de que los datos están actualizados. |
| `Copy JSON` | Botón | Copia el snapshot JSON completo al portapapeles. |
| `Copy Summary` | Botón | Copia el texto del resumen de problemas al portapapeles en lugar del JSON. |
| `Export JSON...` | Botón | Guarda el snapshot JSON en un archivo. |
| `Close` | Botón | Cierra el diálogo. |

## Consejos

- Si acaba de cambiar una configuración del slice (modo, antena, estado de silencio), haga clic en `Refresh Snapshot` antes de `Copy JSON`. El snapshot no se actualiza automáticamente cuando cambia el estado de la radio.
- Para adjuntar el snapshot como archivo en lugar de pegarlo directamente, use `Export JSON...`.

## Relacionado

- [Capturar un snapshot del slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar el snapshot a un archivo para adjuntarlo a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Leer una lista en lenguaje sencillo de los problemas de slice detectados](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar el snapshot después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
