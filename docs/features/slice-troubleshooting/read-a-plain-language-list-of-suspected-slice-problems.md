# Leer una lista en lenguaje claro de problemas detectados en un slice

El diálogo Slice Troubleshooting inspecciona el estado actual de los slices en AetherSDR y muestra un resumen en lenguaje claro de los problemas detectados — como audio ausente, silenciamiento bloqueado o antena no encontrada. Úselo cuando un slice se comporte de manera inesperada y desee un diagnóstico rápido antes de contactar al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión activa al radio.
- La instantánea refleja el estado en memoria de AetherSDR en el momento en que abre o actualiza el diálogo. No vuelve a consultar el radio.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. El diálogo se abre con la pestaña **Issue Summary** activa. Lea la lista de problemas detectados.
3. Si ha cambiado el estado del slice desde que abrió el diálogo, haga clic en **Refresh Snapshot** para actualizar la lista.
4. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** | Pestaña | Muestra una lista en lenguaje claro de los problemas detectados en los slices actuales. |
| **JSON** | Pestaña | Muestra la instantánea JSON completa de los slices y canales DAX. |
| **Refresh Snapshot** | Botón | Vuelve a leer el estado del slice en la instantánea y actualiza ambas pestañas. |
| **Copy Summary** | Botón | Copia el texto del resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia la instantánea JSON completa al portapapeles. |
| **Export JSON...** | Botón | Guarda la instantánea JSON en un archivo. |
| **Close** | Botón | Cierra el diálogo. |

La etiqueta de estado en la parte inferior del diálogo muestra el resultado de la última acción, por ejemplo, "Issue summary copied to clipboard." o los conteos de slices y medidores tras una actualización.

## Sugerencias

- La instantánea se toma automáticamente cuando se abre el diálogo. No es necesario hacer clic en **Refresh Snapshot** a menos que haya cambiado algo en el radio desde que abrió el diálogo.
- Si está registrando un informe de error, el contenido de la pestaña **Issue Summary** es adecuado para pegarlo directamente en un issue de GitHub. Use **Copy Summary** para copiarlo al portapapeles con un solo clic.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Capturar una instantánea de slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
