# Descripción general de la solución de problemas de Slice

El diálogo Slice Troubleshooting captura una instantánea del estado actual en memoria de los slices, panadapters y medidores de AetherSDR, y lo analiza en busca de problemas comunes. Úselo para diagnosticar problemas por su cuenta o para recopilar información para una solicitud de soporte o un informe de errores.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión de radio activa.
- La instantánea refleja el estado en memoria de AetherSDR en el momento en que se toma. No vuelve a consultar el radio.

## Cómo funciona

Abra el diálogo desde `Help > Slice Troubleshooting...`. La instantánea se toma automáticamente cuando el diálogo se abre. Dos pestañas presentan los mismos datos en distintas formas:

- **Issue Summary** — una lista con viñetas en lenguaje sencillo de los problemas detectados, como audio ausente, silencio bloqueado y asignaciones de antena faltantes.
- **JSON** — la instantánea estructurada completa que abarca slices, panadapters, canales DAX, medidores, estado DSP del cliente y estado de la interfaz. Esta pestaña es adecuada para la solución de problemas asistida por IA o para adjuntar a un informe de errores.

Después de cambiar el estado de un slice —por ejemplo, quitar el silencio o reasignar una antena— haga clic en **Refresh Snapshot** para actualizar ambas vistas.

La etiqueta de estado en la parte inferior del diálogo confirma el resultado de cada acción; por ejemplo, muestra cuántos slices y medidores se encontraron, o confirma que el contenido fue copiado o exportado.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Issue Summary | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados. |
| JSON | Pestaña | Muestra la instantánea JSON completa de los slices y los canales DAX. |
| Refresh Snapshot | Botón | Vuelve a leer el estado del slice en la instantánea y actualiza ambas pestañas. |
| Copy Summary | Botón | Copia el texto del resumen de problemas al portapapeles. |
| Copy JSON | Botón | Copia el JSON completo al portapapeles. |
| Export JSON... | Botón | Abre un diálogo de guardar para escribir el JSON en un archivo. El nombre de archivo predeterminado es `aethersdr-slice-troubleshooting-<timestamp>.json` en su directorio de inicio. |
| Close | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción, como "Copied to clipboard" o el recuento de slices y medidores tras una actualización. |

## Consejos

- Use la pestaña **Issue Summary** al registrar un problema en GitHub. Use **Copy Summary** para pegar su contenido directamente en un informe.
- Use **Export JSON...** para guardar un archivo que pueda adjuntar a un informe de errores o compartir con soporte para análisis asistido por IA.
- La instantánea incluye el estado DSP del lado del cliente (NR2, NR4, DFNR) junto con el estado del radio, lo que ayuda a reproducir problemas que dependen de ambos.

## Relacionados

- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje sencillo de los problemas de slice sospechados](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de errores](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
