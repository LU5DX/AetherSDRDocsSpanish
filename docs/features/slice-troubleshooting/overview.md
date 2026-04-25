# Descripción general de la solución de problemas de slice

El diálogo de solución de problemas de slice captura una instantánea del estado actual de los slices, el panadapter y los canales DAX de AetherSDR, y luego los analiza en busca de problemas comunes. Úselo para diagnosticar problemas de audio, silenciamiento y antena por su cuenta, o para recopilar datos de diagnóstico antes de contactar al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión de radio activa.

## Cómo funciona

Abra el diálogo desde `Help > Slice Troubleshooting...`. Cuando el diálogo se abre, AetherSDR lee el estado actual del radio y de los slices en memoria para crear una instantánea. La instantánea no se actualiza automáticamente si cambia la configuración del slice después de abrir el diálogo — haga clic en "Refresh Snapshot" para actualizarla.

El diálogo tiene dos pestañas:

- **Issue Summary** — muestra una lista con viñetas en lenguaje claro de los problemas detectados, como audio faltante, silenciamiento bloqueado o asignaciones de antena ausentes.
- **JSON** — muestra la instantánea completa como JSON estructurado, que incluye slices, panadapters, canales DAX, medidores y el estado DSP del cliente.

Una etiqueta de estado debajo de las pestañas confirma el resultado de las acciones de copia y exportación (por ejemplo, "Copied to clipboard").

## Qué hace cada control

| Control | Tipo | Qué hace |
|---|---|---|
| Issue Summary (tab) | Pestaña | Muestra una lista con viñetas en lenguaje claro de los problemas detectados. |
| JSON (tab) | Pestaña | Muestra la instantánea JSON completa de los slices y canales DAX. |
| Refresh Snapshot | Botón | Vuelve a leer el estado actual del slice en la instantánea. Úselo después de cambiar la configuración del slice mientras el diálogo está abierto. |
| Copy Summary | Botón | Copia el texto del resumen de problemas al portapapeles. |
| Copy JSON | Botón | Copia la instantánea JSON completa al portapapeles. |
| Export JSON... | Botón | Abre un diálogo de guardado de archivo para escribir la instantánea JSON en un archivo. |
| Close | Botón | Cierra el diálogo. |

## Consejos

- Use la pestaña **Issue Summary** y "Copy Summary" al registrar un problema en GitHub — el formato en lenguaje claro es más fácil de leer en un informe de error.
- Use la pestaña **JSON** y "Copy JSON" o "Export JSON..." cuando necesite proporcionar datos de diagnóstico detallados, por ejemplo para la resolución de problemas asistida por IA o para adjuntar a un ticket de soporte.
- Si cambia una configuración del slice (modo, antena, silenciamiento) mientras el diálogo está abierto, haga clic en "Refresh Snapshot" antes de copiar o exportar; de lo contrario, la instantánea reflejará el estado en el momento en que se abrió el diálogo.

## Relacionados

- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje claro de posibles problemas de slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
