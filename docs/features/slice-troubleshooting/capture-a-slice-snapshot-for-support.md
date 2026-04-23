# Capturar una instantánea de slice para soporte

El diálogo Slice Troubleshooting captura una instantánea en un momento determinado de cada slice, panadapter y canal DAX en el estado actual en memoria de AetherSDR. Úselo para recopilar información de diagnóstico antes de enviar un informe de error o solicitar ayuda.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo requiere una conexión de radio activa.
- Reproduzca o confirme el problema que desea reportar antes de abrir el diálogo, para que la instantánea refleje el estado relevante.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. El diálogo se abre en la pestaña **Issue Summary** y toma una instantánea automáticamente. Revise la lista de puntos para ver los problemas detectados (audio faltante, silencio bloqueado, antena ausente).
3. Haga clic en la pestaña **JSON** para ver la instantánea JSON completa de los slices y canales DAX.
4. Si modificó el estado del slice después de abrir el diálogo, haga clic en **Refresh Snapshot** para releer el estado actual.
5. Para compartir un resumen en lenguaje natural, haga clic en **Copy Summary**. El texto se copia al portapapeles.
6. Para compartir el detalle técnico completo, haga clic en **Copy JSON**. El JSON completo se copia al portapapeles.
7. Para guardar la instantánea como archivo adjunto a un informe de error, haga clic en **Export JSON...**, elija una ubicación de guardado y confirme. El nombre de archivo predeterminado es `aethersdr-slice-troubleshooting-<timestamp>.json` en su directorio de inicio.
8. Verifique la etiqueta de estado en la parte inferior del diálogo para confirmar la última acción (por ejemplo, `Issue summary copied to clipboard.` o `JSON copied to clipboard.`).
9. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** | Pestaña | Muestra una lista de puntos en lenguaje natural con los problemas detectados. |
| **JSON** | Pestaña | Muestra la instantánea JSON completa de los slices y canales DAX. |
| **Refresh Snapshot** | Botón | Relee el estado del slice en la instantánea. |
| **Copy Summary** | Botón | Copia el resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia el JSON completo al portapapeles. |
| **Export JSON...** | Botón | Abre un diálogo de guardado y escribe el JSON en un archivo. |
| **Close** | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación. |

## Consejos

- El diálogo lee únicamente el estado en memoria de AetherSDR. No vuelve a consultar la radio a través de la red. Si el estado de la radio cambió recientemente y la instantánea parece desactualizada, haga clic en **Refresh Snapshot**.
- La pestaña **Issue Summary** es adecuada para pegar en issues de GitHub o publicaciones en foros. La salida de la pestaña **JSON** es más apropiada para diagnósticos detallados o asistidos por inteligencia artificial.
- El nombre del archivo exportado incluye una marca de tiempo, por lo que las exportaciones repetidas no se sobrescriben entre sí.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje natural de posibles problemas de slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
