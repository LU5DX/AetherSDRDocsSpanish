# Actualizar el snapshot después de cambiar el estado de un slice

Después de realizar un cambio en un slice — como quitarle el silencio, cambiar su antena o habilitar el audio DAX — el diálogo Slice Troubleshooting no se actualiza automáticamente. Use `Refresh Snapshot` para volver a leer el estado actual del slice y que el Issue Summary y el JSON reflejen sus cambios.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Slice Troubleshooting requiere una conexión activa con la radio.
- Abra el diálogo mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Realice el cambio en el slice que desea verificar (por ejemplo, quitar el silencio a un slice o reasignar su antena).
2. En el diálogo Slice Troubleshooting, haga clic en `Refresh Snapshot`.
3. Revise el contenido actualizado en la pestaña `Issue Summary` o en la pestaña `JSON`.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `Refresh Snapshot` | Botón | Vuelve a leer el estado del slice en el snapshot. Ambas pestañas se actualizan de inmediato. |
| `Issue Summary` (pestaña) | Pestaña | Lista con viñetas en lenguaje sencillo de los problemas detectados según el snapshot actual. |
| `JSON` (pestaña) | Pestaña | Snapshot JSON completo de los slices y canales DAX según el snapshot actual. |
| `Copy Summary` | Botón | Copia el resumen de problemas al portapapeles. |
| `Copy JSON` | Botón | Copia el JSON completo al portapapeles. |
| `Export JSON...` | Botón | Guarda el JSON en un archivo. |
| `Close` | Botón | Cierra el diálogo. |

## Consejos

- Haga clic en `Refresh Snapshot` después de cada cambio de estado del slice que desee evaluar. El diálogo no consulta los cambios por sí solo.
- Después de actualizar, use `Copy JSON` o `Export JSON...` para capturar el snapshot actualizado antes de compartirlo con el equipo de soporte.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar un snapshot de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje sencillo de posibles problemas de slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar el snapshot JSON completo al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar el snapshot a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
