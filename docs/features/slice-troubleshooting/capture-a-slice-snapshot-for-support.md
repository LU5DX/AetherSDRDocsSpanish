# Capturar una instantánea de slice para soporte

El diálogo Slice Troubleshooting captura una instantánea completa de sus slices, panadapters, transvertidores y canales DAX, y resume los problemas probables en lenguaje claro. Úselo para reunir la información que necesita una solicitud de soporte antes de enviar un informe de error o pedir ayuda.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión de radio activa.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo Slice Troubleshooting. La instantánea se toma automáticamente cuando se abre el diálogo.
2. Revise los problemas detectados en la pestaña **Issue Summary**. Cada entrada es un punto en lenguaje claro que describe un problema sospechado, como audio faltante, silencio bloqueado, antena faltante o un transvertidor no válido.
3. Cambie a la pestaña **JSON** para ver la instantánea completa en formato legible por máquina, que cubre cada slice, panadapter, transvertidor y canal DAX.
4. Si modificó el estado del radio después de abrir el diálogo, haga clic en **Refresh Snapshot** para releer el estado actual del slice.
5. Para compartir el resumen con soporte, haga clic en **Copy Summary**. El resumen de problemas se copia al portapapeles. La etiqueta de estado en la parte inferior del diálogo confirma el resultado.
6. Para compartir el detalle completo, haga clic en **Copy JSON** para copiar el JSON completo al portapapeles, o haga clic en **Export JSON...** para guardarlo en un archivo que pueda adjuntar a un informe de error.
7. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** | Pestaña | Muestra una lista de puntos en lenguaje claro con los problemas detectados. |
| **JSON** | Pestaña | Muestra la instantánea JSON completa de slices, panadapters, transvertidores y canales DAX. |
| **Refresh Snapshot** | Botón | Relee el estado del slice en la instantánea. Úselo después de cambiar la configuración del radio. |
| **Copy Summary** | Botón | Copia el resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia la instantánea JSON completa al portapapeles. |
| **Export JSON...** | Botón | Abre un diálogo para guardar archivos y escribe la instantánea JSON en un archivo. |
| **Close** | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación, por ejemplo "Copied to clipboard". |

## Consejos

- Haga clic en **Refresh Snapshot** después de cualquier cambio en los ajustes de slice, antena o DAX para que la instantánea refleje el estado actual antes de copiarla o exportarla.
- Si va a enviar un informe de error, use **Export JSON...** en lugar de **Copy JSON** para tener un archivo guardado que adjuntar, sin riesgo de sobrescribir el portapapeles.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje claro de problemas de slice sospechados](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Inspeccionar la RF/IF, el desplazamiento y los indicadores de validez de cada transvertidor para el diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
