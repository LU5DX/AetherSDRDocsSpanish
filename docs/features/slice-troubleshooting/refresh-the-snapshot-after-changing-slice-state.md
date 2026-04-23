# Actualizar la instantánea después de cambiar el estado de un slice

El diálogo Slice Troubleshooting captura una instantánea del estado del radio al abrirse. Si cambia algún ajuste de un slice después de abrir el diálogo —por ejemplo, desactivar el silencio de un slice o cambiar su antena— los datos mostrados quedarán desactualizados. Haga clic en **Refresh Snapshot** para releer el estado actual y que las pestañas **Issue Summary** y **JSON** reflejen sus cambios.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Slice Troubleshooting requiere una conexión activa con el radio.
- El diálogo Slice Troubleshooting debe estar ya abierto. Si no lo está, vaya a `Help > Slice Troubleshooting...`.

## Pasos

1. Realice el cambio de estado del slice que desea capturar (por ejemplo, desactivar el silencio de un slice, cambiar su modo o reasignar su antena).
2. En el diálogo Slice Troubleshooting, haga clic en **Refresh Snapshot**.
3. Revise la etiqueta de estado en la parte inferior del diálogo. Mostrará un mensaje con el formato `Snapshot refreshed: N slice(s), N global meter(s), N total meter(s).`
4. Revise el contenido actualizado en la pestaña **Issue Summary** o en la pestaña **JSON** según sea necesario.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados en la instantánea actualizada. |
| **JSON** | Pestaña | Muestra la instantánea JSON completa de los slices y canales DAX generada por la última actualización. |
| **Refresh Snapshot** | Botón | Relee el estado actual del slice en la instantánea y actualiza ambas pestañas. |
| **Copy Summary** | Botón | Copia el texto del resumen de problemas al portapapeles. La etiqueta de estado confirma la acción con `Issue summary copied to clipboard.` |
| **Copy JSON** | Botón | Copia el JSON completo al portapapeles. La etiqueta de estado confirma la acción con `JSON copied to clipboard.` |
| **Export JSON...** | Botón | Abre un diálogo para guardar el archivo y escribe el JSON en un fichero. |
| **Close** | Botón | Cierra el diálogo. |

## Consejos

- El diálogo no consulta el radio de forma continua. Cada vez que cambie el estado de un slice y desee datos actualizados, haga clic en **Refresh Snapshot** nuevamente.
- Después de actualizar, use **Copy Summary** para copiar la lista de problemas actualizada, o **Copy JSON** para copiar la instantánea sin procesar, antes de compartirlos con soporte técnico.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar una instantánea de slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje sencillo de los problemas sospechados en un slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
