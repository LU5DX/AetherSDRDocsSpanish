# Capturar una instantánea de slice para soporte técnico

El diálogo Slice Troubleshooting captura una instantánea en un momento determinado de cada slice (receptor virtual), panadapter, transverter y canal DAX del radio conectado. Úselo para recopilar información antes de presentar un informe de error o solicitar soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El diálogo no está disponible sin una conexión de radio activa.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`. El diálogo Slice Troubleshooting se abre y captura una instantánea de inmediato.
2. Revise los problemas detectados en la pestaña **Issue Summary**. Cada entrada es un punto en lenguaje sencillo que describe un problema sospechado, como audio faltante, silenciamiento bloqueado, antena faltante o una configuración de transverter no válida.
3. Revise los datos sin procesar en la pestaña **JSON** si necesita el detalle completo o si tiene intención de adjuntarlos a un informe.
4. Si modificó el estado del slice después de abrir el diálogo, haga clic en **Refresh Snapshot** para volver a leer el estado actual del slice.
5. Para compartir el texto del resumen, haga clic en **Copy Summary**. El texto se copia al portapapeles.
6. Para compartir el JSON completo, haga clic en **Copy JSON**. La instantánea JSON completa se copia al portapapeles.
7. Para guardar el JSON en un archivo, haga clic en **Export JSON...** y elija una ubicación de guardado en el diálogo de archivo que se abre.
8. Observe la etiqueta de estado en la parte inferior del diálogo. Confirma el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard").
9. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** | Pestaña | Muestra una lista de puntos en lenguaje sencillo con los problemas detectados, incluyendo audio faltante, silenciamiento bloqueado, antena faltante y problemas de validez del transverter. |
| **JSON** | Pestaña | Muestra la instantánea JSON completa de todos los slices, panadapters, transverters y canales DAX. |
| **Refresh Snapshot** | Botón | Vuelve a leer el estado actual del slice desde el radio y actualiza ambas pestañas. |
| **Copy Summary** | Botón | Copia el texto del resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia la instantánea JSON completa al portapapeles. |
| **Export JSON...** | Botón | Abre un diálogo de guardado para escribir la instantánea JSON en un archivo. |
| **Close** | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación. |

## Consejos

- Tome la instantánea antes y después de cambiar la configuración del slice si está intentando aislar un problema. Use **Refresh Snapshot** entre capturas para actualizar los datos.
- Si está reportando un problema con un transverter, la pestaña **JSON** incluye la frecuencia RF, la frecuencia IF, el desplazamiento y los indicadores de validez de cada transverter. La pestaña **Issue Summary** marcará cualquier transverter cuya validez no pueda confirmarse.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje sencillo de problemas sospechados en el slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea tras cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Inspeccionar la frecuencia RF/IF, el desplazamiento y los indicadores de validez de cada transverter para diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
