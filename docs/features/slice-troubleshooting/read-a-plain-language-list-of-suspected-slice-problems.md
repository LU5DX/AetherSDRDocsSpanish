# Leer una lista en lenguaje claro de problemas sospechados en un slice

El diálogo Slice Troubleshooting inspecciona el slice, panadapter, transverter y estado del canal DAX actuales, y presenta un resumen en lenguaje claro de los problemas detectados. Úselo cuando falte audio, un slice se comporte de manera inesperada, o cuando desee una verificación rápida antes de contactar al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión de radio activa.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`.
2. El diálogo se abre. La pestaña **Issue Summary** se muestra de forma predeterminada.
3. Lea la lista con viñetas de problemas detectados. Cada viñeta describe un problema sospechado específico, como audio faltante, un silenciamiento bloqueado, una asignación de antena faltante o un problema de validez de XVTR.
4. Si la lista no refleja cambios recientes que haya realizado en el estado del slice, haga clic en **Refresh Snapshot** para volver a leer el estado actual desde el radio.
5. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** (pestaña) | Pestaña | Muestra una lista con viñetas en lenguaje claro de los problemas detectados. |
| **JSON** (pestaña) | Pestaña | Muestra la instantánea JSON completa de los slices y canales DAX. |
| **Refresh Snapshot** | Botón | Vuelve a leer el estado del slice en la instantánea. Úselo después de cambiar la configuración del slice. |
| **Copy Summary** | Botón | Copia el texto del resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia la instantánea JSON completa al portapapeles. |
| **Export JSON...** | Botón | Guarda la instantánea JSON en un archivo. |
| **Close** | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación (por ejemplo, `Copied to clipboard`). |

## Consejos

- Si no se encuentran problemas, la pestaña **Issue Summary** estará vacía o no mostrará viñetas. Cambie a la pestaña **JSON** para inspeccionar el estado sin procesar del slice si necesita profundizar más.
- Después de cambiar una configuración del slice —como quitar el silenciamiento o reasignar una antena— haga clic en **Refresh Snapshot** antes de volver a leer el resumen. El diálogo no se actualiza automáticamente.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Capturar una instantánea del slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspeccionar los indicadores de RF/IF, desplazamiento y validez de cada transverter para el diagnóstico de XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
