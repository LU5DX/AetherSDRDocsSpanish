# Descripción general de solución de problemas de slice

El diálogo Slice Troubleshooting captura una instantánea completa del estado de los slices, panadapters, transverters y canales DAX de su radio, y los verifica en busca de problemas comunes. Úselo para diagnosticar problemas de audio, silenciamiento, antena y transverter, o para recopilar datos de diagnóstico antes de contactar al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo requiere una conexión de radio activa.

## Cómo funciona

Abra el diálogo desde `Help > Slice Troubleshooting...`. AetherSDR lee el estado actual de cada slice, panadapter, transverter y canal DAX, y construye una instantánea. La instantánea está disponible en dos formas: un resumen de problemas en lenguaje claro y una representación JSON completa. Puede actualizar la instantánea en cualquier momento, copiar cualquiera de las dos formas al portapapeles, o guardar el JSON en un archivo.

El diálogo verifica automáticamente los problemas más probables, incluyendo audio faltante, condiciones de silenciamiento bloqueado, asignaciones de antena faltantes y problemas de validez del transverter. Los problemas detectados aparecen como una lista de viñetas en la pestaña Issue Summary.

Este diálogo no guarda ninguna configuración. Lee el estado de la radio en el momento en que usted lo abre o hace clic en Refresh Snapshot.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Issue Summary (tab) | Pestaña | Muestra una lista de viñetas en lenguaje claro con los problemas detectados en la configuración actual de slices. |
| JSON (tab) | Pestaña | Muestra la instantánea JSON completa de slices, panadapters, transverters y canales DAX. |
| Refresh Snapshot | Botón | Vuelve a leer el estado actual de los slices y reconstruye la instantánea. Haga clic aquí después de cambiar cualquier configuración de slice. |
| Copy Summary | Botón | Copia el texto del resumen de problemas al portapapeles. |
| Copy JSON | Botón | Copia la instantánea JSON completa al portapapeles. |
| Export JSON... | Botón | Abre un diálogo de archivo para guardar la instantánea JSON en un archivo. |
| Close | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación, por ejemplo "Copied to clipboard". |

## Consejos

- Haga clic en Refresh Snapshot después de realizar cualquier cambio en la configuración de slice, antena o transverter, para que la instantánea refleje el estado actualizado antes de copiarla o exportarla.
- Use Copy Summary para pegar una lista concisa de problemas en una publicación de foro o en un ticket de soporte. Use Copy JSON o Export JSON... cuando el equipo de soporte solicite datos de diagnóstico completos.

## Temas relacionados

- [Capturar una instantánea de slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje claro de problemas sospechados en slices](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar la instantánea después de cambiar el estado de un slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspeccionar los indicadores de RF/IF, desplazamiento y validez de cada transverter para diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
