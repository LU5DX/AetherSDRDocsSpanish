# Leer una lista en lenguaje claro de posibles problemas de slice

El diálogo Slice Troubleshooting analiza el estado actual en memoria de los slices (canales de recepción) de AetherSDR y muestra un resumen en lenguaje claro de los problemas más probables, como audio ausente, silenciamiento bloqueado o antena no detectada. Úselo cuando un slice se comporte de forma inesperada y desee un diagnóstico rápido antes de contactar al soporte.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión activa con el radio.
- La instantánea refleja el estado en memoria de AetherSDR en el momento en que se toma. No consulta nuevamente el radio. Si acaba de cambiar la configuración de un slice, actualice la instantánea antes de leer los resultados.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`.
2. El diálogo se abre con la pestaña **Issue Summary** activa y una instantánea ya tomada.
3. Lea la lista de problemas detectados en la pestaña **Issue Summary**.
4. Si ha cambiado el estado del slice desde que abrió el diálogo, haga clic en **Refresh Snapshot** para actualizar la lista.
5. Cuando termine, haga clic en **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** (pestaña) | Pestaña | Lista de problemas detectados en lenguaje claro. |
| **JSON** (pestaña) | Pestaña | Instantánea JSON completa de los slices y canales DAX. |
| **Refresh Snapshot** | Botón | Vuelve a leer el estado del slice en la instantánea y actualiza ambas pestañas. |
| **Copy Summary** | Botón | Copia el texto del resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia el JSON completo al portapapeles. |
| **Export JSON...** | Botón | Guarda el JSON en un archivo. |
| **Close** | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción, por ejemplo "Issue summary copied to clipboard." o los conteos de slices y medidores tras una actualización. |

## Consejos

- La etiqueta de estado en la parte inferior del diálogo muestra los conteos de la instantánea tras cada actualización: número de slices, medidores globales y total de medidores. Úsela para confirmar que la instantánea capturó lo que usted esperaba.
- Si el resumen de problemas está vacío, no se detectaron problemas en la instantánea actual. Pruebe con **Refresh Snapshot** si ha cambiado el estado del slice recientemente.
- Para compartir los hallazgos con el soporte, haga clic en **Copy Summary** y péguelo en un issue de GitHub o en una publicación del foro. Para diagnóstico asistido por inteligencia artificial, use **Copy JSON** o **Export JSON...** en su lugar.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Actualizar la instantánea tras cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Capturar una instantánea de slice para el soporte](capture-a-slice-snapshot-for-support.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
