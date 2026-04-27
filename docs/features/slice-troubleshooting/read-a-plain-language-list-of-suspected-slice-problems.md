# Leer una lista en lenguaje sencillo de problemas detectados en el slice

El cuadro de diálogo Slice Troubleshooting analiza el estado actual del slice (canal de recepción), el panadapter, el transverter y el canal DAX, y presenta un resumen en lenguaje sencillo de los problemas detectados. Úselo cuando sospeche un problema de configuración — como audio ausente, silencio bloqueado (mute), antena faltante o transverter inválido — y desee un diagnóstico rápido sin tener que leer datos sin procesar.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. El cuadro de diálogo requiere una conexión de radio activa.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña **Issue Summary** si no está ya seleccionada.
3. Lea la lista de problemas detectados.
4. Si recientemente cambió la configuración del slice y desea que la lista refleje el estado actual, haga clic en **Refresh Snapshot**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** | Pestaña | Muestra una lista en lenguaje sencillo de los problemas detectados, incluyendo audio ausente, silencio bloqueado, antena faltante y problemas de validez del transverter. |
| **JSON** | Pestaña | Muestra la instantánea JSON completa de los slices y canales DAX. |
| **Refresh Snapshot** | Botón | Vuelve a leer el estado del slice en la instantánea. Haga clic en este botón después de cambiar la configuración del slice. |
| **Copy Summary** | Botón | Copia el texto del resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia la instantánea JSON completa al portapapeles. |
| **Export JSON...** | Botón | Guarda la instantánea JSON completa en un archivo. |
| **Close** | Botón | Cierra el cuadro de diálogo. |

La etiqueta de estado situada debajo de los botones confirma el resultado de la última acción de copia o exportación (por ejemplo, `Copied to clipboard`).

## Consejos

- Haga clic en **Refresh Snapshot** después de realizar cualquier cambio en el slice, la antena o DAX antes de compartir o volver a leer el resumen. La instantánea no se actualiza automáticamente.
- Si necesita enviar los detalles al soporte técnico, use **Copy Summary** para pegar la lista en lenguaje sencillo en un correo electrónico o publicación en un foro, o use **Export JSON...** para adjuntar la instantánea completa como archivo.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Capturar una instantánea del slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspeccionar las frecuencias RF/IF, el desplazamiento y los indicadores de validez de cada transverter para el diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
