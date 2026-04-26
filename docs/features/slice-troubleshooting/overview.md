# Resolución de problemas de slice

El diálogo Slice Troubleshooting captura una instantánea de cada slice y canal DAX en la radio conectada, y luego la analiza en busca de problemas probables, como audio ausente, silenciamiento bloqueado y antena no configurada. Úselo para diagnosticar problemas de slice por su cuenta o para recopilar información que compartir con soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo requiere una conexión de radio activa.

## Cómo funciona

Abra el diálogo desde `Help > Slice Troubleshooting...`. Al abrirse, AetherSDR lee el estado actual de todos los slices y canales DAX en una instantánea. El diálogo presenta esa instantánea en dos vistas, accesibles como pestañas.

**Pestaña Issue Summary** — muestra una lista con viñetas en lenguaje claro de los problemas detectados en la instantánea, como dispositivos de audio ausentes, estados de silenciamiento bloqueados o antenas sin configurar. Revise esta pestaña primero para obtener una lectura rápida de lo que puede estar fallando.

**Pestaña JSON** — muestra la instantánea completa como JSON estructurado, con cada propiedad de slice y asignación de canal DAX. Use esta vista cuando la pestaña Issue Summary no capture suficiente detalle, o cuando un contacto de soporte solicite los datos sin procesar.

La instantánea se toma cuando se abre el diálogo. Si cambia la configuración de los slices mientras el diálogo está abierto, haga clic en "Refresh Snapshot" para volver a leer el estado actual antes de copiar o exportar.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Issue Summary (tab) | Pestaña | Muestra una lista con viñetas en lenguaje claro de los problemas de slice detectados. |
| JSON (tab) | Pestaña | Muestra la instantánea JSON completa de los slices y canales DAX. |
| Refresh Snapshot | Botón | Vuelve a leer el estado de los slices y actualiza ambas pestañas con los datos actuales. |
| Copy Summary | Botón | Copia el texto de Issue Summary al portapapeles. |
| Copy JSON | Botón | Copia la instantánea JSON completa al portapapeles. |
| Export JSON... | Botón | Abre un diálogo de archivo para guardar la instantánea JSON en un fichero. |
| Close | Botón | Cierra el diálogo. |
| Status label | Indicador | Muestra el resultado de la acción de copia o exportación más reciente (por ejemplo, "Copied to clipboard"). |

## Consejos

- Haga clic en "Refresh Snapshot" después de realizar cualquier cambio en la configuración de los slices — el diálogo no se actualiza automáticamente.
- Use "Copy Summary" para pegar una lista concisa de problemas en una publicación de un foro de soporte. Use "Copy JSON" o "Export JSON..." cuando un contacto de soporte necesite la instantánea completa.

## Relacionados

- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje claro de los problemas de slice sospechados](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
