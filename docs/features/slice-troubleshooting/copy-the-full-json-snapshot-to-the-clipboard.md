# Copiar el instantáneo JSON completo al portapapeles

Copie el instantáneo JSON sin procesar de todos los slices y canales DAX al portapapeles para pegarlo en un ticket de soporte, una publicación en el foro o un reporte de error.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo Slice Troubleshooting requiere una conexión de radio activa.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña `JSON` para confirmar que el instantáneo contiene los datos que desea compartir.
3. Si los datos parecen desactualizados, haga clic en `Refresh Snapshot` para releer el estado actual del slice.
4. Haga clic en `Copy JSON`.
5. La etiqueta de estado del diálogo se actualiza para confirmar la copia (por ejemplo, "Copied to clipboard").
6. Pegue el contenido del portapapeles en su ticket de soporte o publicación en el foro.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Pestaña `Issue Summary` | Pestaña | Cambia la vista a una lista con viñetas en lenguaje simple de los problemas detectados. |
| Pestaña `JSON` | Pestaña | Cambia la vista al instantáneo JSON completo de los slices y canales DAX. |
| `Refresh Snapshot` | Botón | Relee el estado del slice y actualiza el instantáneo. Haga clic aquí después de cambiar la configuración del slice antes de copiar. |
| `Copy Summary` | Botón | Copia el resumen de problemas en lenguaje simple al portapapeles, no el JSON completo. |
| `Copy JSON` | Botón | Copia el instantáneo JSON completo al portapapeles. |
| `Export JSON...` | Botón | Guarda el instantáneo JSON en un archivo en lugar del portapapeles. |
| `Close` | Botón | Cierra el diálogo. |

## Consejos

- Haga clic en `Refresh Snapshot` antes de `Copy JSON` si ha cambiado el estado del slice desde que abrió el diálogo. El instantáneo no se actualiza automáticamente.
- Para adjuntar el JSON como archivo en lugar de pegarlo directamente, use `Export JSON...` en su lugar.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar un instantáneo de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar el instantáneo a un archivo para adjuntar a un reporte de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Leer una lista en lenguaje simple de los problemas de slice detectados](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar el instantáneo después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
