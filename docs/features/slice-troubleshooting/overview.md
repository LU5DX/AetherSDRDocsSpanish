# Descripción general de la solución de problemas de slice

El diálogo de solución de problemas de slice captura una instantánea del estado actual en memoria de la radio, el panadapter, el slice (receptor individual) y los medidores de AetherSDR. Utilícelo para diagnosticar problemas comunes de slice por su cuenta o para generar un informe destinado al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo requiere una conexión de radio activa.
- La instantánea refleja el estado en memoria en el momento en que abre el diálogo o hace clic en Refresh Snapshot. No vuelve a consultar la radio.

## Cómo funciona

Abra el diálogo desde `Help > Slice Troubleshooting...`. La instantánea se toma automáticamente al abrir el diálogo.

El diálogo presenta dos vistas de la misma instantánea, seleccionables mediante pestañas:

- **Issue Summary** — una lista con viñetas en lenguaje sencillo de los problemas detectados, como audio ausente, silencio bloqueado o asignaciones de antena faltantes.
- **JSON** — la instantánea completa en formato JSON, que abarca slices, canales DAX, panadapters, medidores, estado DSP del cliente y estado de la interfaz.

Una vez obtenida la instantánea, puede copiarla o exportarla mediante los botones situados en la parte inferior del diálogo. La etiqueta de estado que aparece encima de los botones muestra el resultado de la última acción (por ejemplo, "Issue summary copied to clipboard." o "JSON copied to clipboard.").

Para capturar una instantánea actualizada después de realizar cambios en el estado del slice, haga clic en Refresh Snapshot. La etiqueta de estado mostrará entonces cuántos slices, medidores globales y medidores en total se encontraron.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Issue Summary | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas de slice detectados. |
| JSON | Pestaña | Muestra la instantánea JSON completa de los slices y los canales DAX. |
| Refresh Snapshot | Botón | Vuelve a leer el estado del slice en la instantánea y actualiza ambas pestañas. |
| Copy Summary | Botón | Copia el texto del resumen de problemas al portapapeles. |
| Copy JSON | Botón | Copia el JSON completo al portapapeles. |
| Export JSON... | Botón | Abre un diálogo de guardado para escribir el JSON en un archivo. El nombre de archivo predeterminado incluye una marca de tiempo, por ejemplo `aethersdr-slice-troubleshooting-20240501-143022.json`. |
| Close | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación, y el recuento de slices y medidores tras una actualización. |

## Consejos

- Use la pestaña Issue Summary al registrar un problema en GitHub. Use la pestaña JSON cuando trabaje en un problema con herramientas asistidas por inteligencia artificial o cuando adjunte un archivo a un informe de error.
- Si cambia alguna configuración de un slice (como quitar el silencio o reasignar una antena) mientras el diálogo está abierto, haga clic en Refresh Snapshot para actualizar la instantánea antes de copiarla o exportarla.

## Temas relacionados

- [Capturar una instantánea de slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje sencillo de los problemas de slice detectados](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
