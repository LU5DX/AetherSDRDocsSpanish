# Leer una lista en lenguaje sencillo de los problemas detectados en un slice

El cuadro de diálogo Slice Troubleshooting analiza el estado actual de su slice, panadapter, transverter y canal DAX, y presenta un resumen en lenguaje sencillo de los problemas detectados. Úselo cuando sospeche un problema de configuración — como audio ausente, silenciamiento bloqueado, antena faltante o un transverter no válido — y desee un diagnóstico rápido sin leer datos sin procesar.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. El cuadro de diálogo requiere una conexión de radio activa.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña **Issue Summary** si no está seleccionada.
3. Lea la lista de problemas detectados.
4. Si ha cambiado recientemente la configuración del slice y desea que la lista refleje el estado actual, haga clic en **Refresh Snapshot**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** | Pestaña | Muestra una lista en lenguaje sencillo de los problemas detectados, incluidos audio ausente, silenciamiento bloqueado, antena faltante e incidencias de validez del transverter. |
| **JSON** | Pestaña | Muestra el volcado JSON completo de los slices y canales DAX. |
| **Refresh Snapshot** | Botón | Vuelve a leer el estado del slice en el volcado. Haga clic aquí después de cambiar la configuración del slice. |
| **Copy Summary** | Botón | Copia el texto del resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia el volcado JSON completo al portapapeles. |
| **Export JSON...** | Botón | Guarda el volcado JSON completo en un archivo. |
| **Close** | Botón | Cierra el cuadro de diálogo. |

La etiqueta de estado que aparece debajo de los botones confirma el resultado de la última acción de copia o exportación (por ejemplo, `Copied to clipboard`).

## Consejos

- Haga clic en **Refresh Snapshot** después de realizar cualquier cambio en el slice, la antena o el canal DAX antes de compartir o volver a leer el resumen. El volcado no se actualiza automáticamente.
- Si necesita enviar los detalles al soporte técnico, use **Copy Summary** para pegar la lista en lenguaje sencillo en un correo electrónico o publicación en un foro, o use **Export JSON...** para adjuntar el volcado completo como archivo.

## Temas relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Actualizar el volcado tras cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Capturar un volcado del slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Exportar el volcado a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspeccionar los indicadores RF/IF, desplazamiento y validez de cada transverter para diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
