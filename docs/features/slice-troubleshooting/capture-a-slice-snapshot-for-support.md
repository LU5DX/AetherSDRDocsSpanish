# Capturar una instantánea de slice para soporte

El diálogo Slice Troubleshooting captura una instantánea en un momento determinado de cada slice (canal de recepción), panadapter (analizador panorámico) y canal DAX como documento JSON, y resume los problemas probables en lenguaje sencillo. Úselo para reunir la información que necesita una solicitud de soporte o un informe de error.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión activa con el radio.
- Reproduzca o alcance el estado del problema antes de abrir el diálogo. La instantánea lee el estado en memoria en el momento en que usted la abre o la actualiza; no consulta de nuevo al radio.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`. El diálogo Slice Troubleshooting se abre e inmediatamente captura una instantánea.
2. Revise la pestaña **Issue Summary** para ver una lista con viñetas en lenguaje sencillo de los problemas detectados (audio ausente, silencio bloqueado, antena faltante y condiciones similares).
3. Cambie a la pestaña **JSON** si necesita la instantánea técnica completa.
4. Si cambió el estado del slice después de abrir el diálogo, haga clic en **Refresh Snapshot** para releer el estado actual. La etiqueta de estado en la parte inferior del diálogo muestra un recuento de slices y medidores capturados.
5. Para compartir el resumen de problemas (por ejemplo, en un issue de GitHub), haga clic en **Copy Summary**. La etiqueta de estado confirma "Issue summary copied to clipboard."
6. Para compartir el JSON completo (por ejemplo, para solución de problemas asistida por IA), haga clic en **Copy JSON**. La etiqueta de estado confirma "JSON copied to clipboard."
7. Para guardar el JSON como archivo y adjuntarlo a un informe de error, haga clic en **Export JSON...**. Se abre un diálogo de guardar con un nombre de archivo predeterminado de la forma `aethersdr-slice-troubleshooting-YYYYMMDD-HHmmss.json` en su directorio personal. Elija una ubicación y confirme.
8. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados en la instantánea actual. |
| **JSON** | Pestaña | Muestra la instantánea JSON completa de slices, panadapters, canales DAX y estado DSP del cliente. |
| **Refresh Snapshot** | Botón | Relee el estado del slice en la instantánea. Úselo después de cambiar la configuración del slice. |
| **Copy Summary** | Botón | Copia el texto del resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia el texto JSON completo al portapapeles. |
| **Export JSON...** | Botón | Abre un diálogo de guardar para escribir el JSON en un archivo. El nombre de archivo predeterminado incluye una marca de tiempo. |
| **Close** | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción, como "Issue summary copied to clipboard." o un recuento de slices y medidores después de una actualización. |

## Consejos

- La instantánea se toma del modelo en memoria de AetherSDR, no enviando nuevos comandos al radio. Si el estado del radio ha cambiado, haga clic en **Refresh Snapshot** antes de copiar o exportar.
- El contenido de la pestaña **Issue Summary** está formateado para facilitar la lectura en issues de GitHub. El contenido de la pestaña **JSON** es más adecuado para pegar en herramientas de chat con IA o para adjuntar como archivo.
- El nombre del archivo JSON exportado incluye una marca de tiempo, por lo que exportar varias instantáneas en secuencia no sobreescribirá los archivos anteriores.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje sencillo de los problemas de slice detectados](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
