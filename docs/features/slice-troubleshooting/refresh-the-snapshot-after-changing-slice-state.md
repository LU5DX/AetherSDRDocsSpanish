# Actualizar la instantánea después de cambiar el estado del slice

Después de modificar la configuración del slice — como ajustar el enrutamiento de audio, activar o desactivar el silencio, o cambiar de antena — el diálogo Slice Troubleshooting no se actualiza automáticamente. Use **Refresh Snapshot** para volver a leer el estado actual del slice y que el Issue Summary y el JSON reflejen los cambios realizados.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Slice Troubleshooting requiere una conexión de radio activa.
- Abra el diálogo mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Realice el cambio de estado del slice que desea capturar (por ejemplo, quitar el silencio a un slice, reasignar una antena o ajustar un canal DAX).
2. En el diálogo Slice Troubleshooting, haga clic en **Refresh Snapshot**.
3. El diálogo vuelve a leer el estado de todos los slices, panadapters, transvertidores y canales DAX.
4. Revise los resultados actualizados en la pestaña **Issue Summary** o en la pestaña **JSON**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Refresh Snapshot** | Botón | Vuelve a leer el estado del slice en la instantánea. Úselo después de cualquier cambio de configuración del slice. |
| **Issue Summary** (pestaña) | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados según la instantánea actual. |
| **JSON** (pestaña) | Pestaña | Muestra la instantánea JSON completa de los slices y canales DAX según la instantánea actual. |
| **Copy Summary** | Botón | Copia el resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia el JSON completo al portapapeles. |
| **Export JSON...** | Botón | Guarda el JSON en un archivo. |
| **Close** | Botón | Cierra el diálogo. |

## Consejos

- Después de hacer clic en **Refresh Snapshot**, revise tanto la pestaña **Issue Summary** como la pestaña **JSON** para confirmar que el cambio realizado queda reflejado antes de compartir la instantánea con el soporte técnico.
- Si planea exportar o copiar la instantánea para un informe de error, haga clic siempre en **Refresh Snapshot** primero para asegurarse de que los datos estén actualizados.

## Temas relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar una instantánea del slice para el soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje sencillo de posibles problemas del slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntarla a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
