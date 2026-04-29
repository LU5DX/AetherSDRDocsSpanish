# Diagnóstico de Slice

El diálogo de diagnóstico de slice (Slice Troubleshooting) captura una instantánea de cada slice, panadapter, transverter y canal DAX del radio conectado, y verifica si existen problemas de configuración probables. Úselo para diagnosticar problemas de audio, silenciamiento, antena y transverter, o para recopilar datos de diagnóstico antes de contactar al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El diálogo no está disponible sin una conexión de radio activa.

## Cómo funciona

Abra el diálogo con `Help > Slice Troubleshooting...`. Al abrirse, AetherSDR lee el estado actual del radio y genera una instantánea. La instantánea abarca slices, panadapters, transverters, canales DAX y los metadatos asociados. El diálogo analiza esa instantánea en busca de un conjunto de patrones de problemas conocidos —audio ausente, silenciamiento bloqueado, antena faltante y problemas de validez del transverter— y presenta los resultados en dos pestañas.

La pestaña **Issue Summary** muestra una lista con viñetas en lenguaje sencillo de los problemas detectados. Si no hay ningún problema, la lista aparece vacía. Esta es la forma más rápida de verificar si AetherSDR ha identificado un problema de configuración.

La pestaña **JSON** muestra la instantánea completa como JSON estructurado. Esta vista contiene todos los campos recopilados por AetherSDR: estado del slice, parámetros del panadapter, frecuencias RF/IF del transverter, desplazamientos, indicadores de validez y asignaciones de canales DAX. El personal de soporte y los usuarios avanzados pueden inspeccionar aquí los valores de cada campo individualmente.

La instantánea refleja el estado del radio en el momento en que fue tomada. Si cambia la configuración del slice mientras el diálogo está abierto, haga clic en **Refresh Snapshot** para volver a leer el estado actual antes de sacar conclusiones o compartir los datos.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Issue Summary | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados. |
| JSON | Pestaña | Muestra la instantánea JSON completa de los slices y canales DAX. |
| Refresh Snapshot | Botón | Vuelve a leer el estado del slice en la instantánea. Úselo después de cambiar la configuración del radio. |
| Copy Summary | Botón | Copia el texto del resumen de problemas al portapapeles. |
| Copy JSON | Botón | Copia la instantánea JSON completa al portapapeles. |
| Export JSON... | Botón | Abre un diálogo de archivo para guardar la instantánea JSON en un archivo. |
| Close | Botón | Cierra el diálogo. |
| Status label | Indicador | Muestra el resultado de la acción de copia o exportación más reciente (por ejemplo, "Copied to clipboard"). |

## Consejos

- Tome una nueva instantánea con **Refresh Snapshot** después de cada cambio de configuración. El diálogo no se actualiza automáticamente mientras está abierto.
- Use **Copy Summary** para pegar una lista concisa de problemas en una publicación de un foro de soporte o en un correo electrónico. Use **Copy JSON** o **Export JSON...** al adjuntar datos de diagnóstico completos a un informe de error.

## Relacionados

- [Capturar una instantánea de slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje sencillo de los problemas de slice sospechados](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntarlo a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspeccionar las frecuencias RF/IF, el desplazamiento y los indicadores de validez de cada transverter para el diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
