# Exportar la instantánea a un archivo para adjuntar a un informe de errores

Use esta página para guardar la instantánea JSON del diálogo Slice Troubleshooting en un archivo y adjuntarla a una solicitud de soporte o informe de errores.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Slice Troubleshooting requiere una conexión de radio activa.
- Abra el diálogo Slice Troubleshooting mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en `Refresh Snapshot` para asegurarse de que la instantánea refleje el estado actual del radio.
3. Haga clic en `Export JSON...`.
4. En el diálogo de archivo que se abre, elija una carpeta de destino y un nombre de archivo, luego confirme el guardado.
5. Verifique la etiqueta de estado en la parte inferior del diálogo para confirmar que la exportación se completó.
6. Adjunte el archivo guardado a su informe de errores o ticket de soporte.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `Refresh Snapshot` | Botón | Vuelve a leer el estado actual del slice, panadapter, transverter y canal DAX en la instantánea. Haga clic aquí antes de exportar si el estado del slice ha cambiado. |
| `Export JSON...` | Botón | Abre un diálogo de archivo y guarda la instantánea JSON completa en el archivo elegido. |
| `Copy JSON` | Botón | Copia la instantánea JSON completa al portapapeles en lugar de guardarla en un archivo. |
| `JSON (tab)` | Pestaña | Muestra la instantánea JSON completa en el diálogo para que pueda revisarla antes de exportar. |
| `Issue Summary (tab)` | Pestaña | Muestra una lista en lenguaje sencillo de los problemas detectados junto al JSON sin procesar. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación. |

## Consejos

- Haga clic en `Refresh Snapshot` inmediatamente antes de exportar si realizó cambios en el slice desde que abrió el diálogo. La instantánea no se actualiza automáticamente.
- Si su sistema de seguimiento de errores no acepta archivos adjuntos, use `Copy JSON` para pegar la instantánea directamente en un comentario o campo de formulario.

## Relacionado

- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje sencillo de problemas de slice detectados](read-a-plain-language-list-of-suspected-slice-problems.md)
