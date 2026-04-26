# Actualizar la instantánea tras cambiar el estado de un slice

Después de realizar un cambio en un slice — como reactivar el audio silenciado, cambiar la antena o ajustar un canal DAX — el diálogo Slice Troubleshooting no se actualiza automáticamente. Use **Refresh Snapshot** para volver a leer el estado actual del slice y que las pestañas **Issue Summary** y **JSON** reflejen los cambios.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Slice Troubleshooting requiere una conexión activa con la radio.
- Abra el diálogo mediante `Help > Slice Troubleshooting...`.

## Pasos

1. Realice el cambio de estado del slice que desea verificar (por ejemplo, reactive el audio de un slice, asigne una antena o habilite un canal DAX).
2. En el diálogo Slice Troubleshooting, haga clic en **Refresh Snapshot**.
3. Revise la pestaña **Issue Summary** para ver una lista actualizada en lenguaje sencillo de los problemas detectados, o haga clic en la pestaña **JSON** para inspeccionar la instantánea completa actualizada.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Refresh Snapshot** | Botón | Vuelve a leer el estado de todos los slices, panadapters, transverters y canales DAX en la instantánea. |
| **Issue Summary** (pestaña) | Pestaña | Muestra una lista en lenguaje sencillo de los problemas detectados según la instantánea actual. |
| **JSON** (pestaña) | Pestaña | Muestra la instantánea JSON completa de los slices y canales DAX. |
| **Copy Summary** | Botón | Copia el texto del resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia el JSON completo al portapapeles. |
| **Export JSON...** | Botón | Guarda la instantánea JSON en un archivo. |
| **Close** | Botón | Cierra el diálogo. |

## Consejos

- Después de hacer clic en **Refresh Snapshot**, revise la etiqueta de estado en la parte inferior del diálogo para confirmar el resultado de la última operación.
- Si desea comparar el estado antes y después de un cambio, use **Export JSON...** para guardar una copia de la instantánea antes de actualizar.

## Temas relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje sencillo de los problemas detectados en un slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Capturar una instantánea de slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
