# Capturar una instantánea de slice para soporte

El diálogo Slice Troubleshooting captura una instantánea del estado actual de cada slice (receptor virtual) y resume los problemas probables. Úselo para recopilar información antes de enviar un informe de error o solicitar soporte.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El diálogo requiere una conexión de radio activa.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo Slice Troubleshooting.
2. Revise la pestaña **Issue Summary** para ver una lista de problemas detectados en lenguaje sencillo (audio faltante, silencio bloqueado, antena ausente y problemas similares).
3. Haga clic en la pestaña **JSON** para ver la instantánea completa de los slices y los canales DAX.
4. Realice una de las siguientes acciones para compartir la instantánea:
   - Haga clic en **Copy Summary** para copiar el resumen de problemas al portapapeles.
   - Haga clic en **Copy JSON** para copiar la instantánea JSON completa al portapapeles.
   - Haga clic en **Export JSON...** para guardar el JSON en un archivo que pueda adjuntar a un informe de error.
5. Si cambia el estado del slice mientras el diálogo está abierto, haga clic en **Refresh Snapshot** para releer el estado actual antes de copiar o exportar.
6. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** | Pestaña | Lista de viñetas en lenguaje sencillo con los problemas detectados. |
| **JSON** | Pestaña | Instantánea JSON completa de los slices y los canales DAX. |
| **Refresh Snapshot** | Botón | Vuelve a leer el estado del slice en la instantánea. |
| **Copy Summary** | Botón | Copia el resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia la instantánea JSON completa al portapapeles. |
| **Export JSON...** | Botón | Guarda el JSON en un archivo. |
| **Close** | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard"). |

## Consejos

- Use la pestaña **Issue Summary** al registrar un problema en GitHub. Use la salida de la pestaña **JSON** cuando busque ayuda con diagnóstico asistido por IA o cuando el soporte solicite el estado completo.
- Haga clic en **Refresh Snapshot** después de realizar cualquier cambio en la configuración de un slice para que la instantánea refleje el estado actual antes de exportar o copiar.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje sencillo de problemas sospechados en slices](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
