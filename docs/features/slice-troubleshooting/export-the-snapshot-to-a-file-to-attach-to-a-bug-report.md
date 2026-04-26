# Exportar la instantánea a un archivo para adjuntar a un informe de error

Use esta página para guardar la instantánea JSON del diálogo Slice Troubleshooting en un archivo en disco, de modo que pueda adjuntarla a un informe de error o solicitud de soporte.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Slice Troubleshooting requiere una conexión de radio activa.
- Abra el diálogo Slice Troubleshooting mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. En el diálogo Slice Troubleshooting, haga clic en la pestaña `JSON` para confirmar que la instantánea contiene datos actuales. Si los datos parecen desactualizados, haga clic en `Refresh Snapshot` antes de exportar.
2. Haga clic en `Export JSON...`.
3. En el diálogo de guardar archivo que se abre, elija una carpeta de destino y un nombre de archivo, luego confirme el guardado.
4. Verifique la etiqueta de estado en la parte inferior del diálogo para confirmar que la exportación fue exitosa.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `Issue Summary` (pestaña) | Pestaña | Muestra una lista de viñetas en lenguaje sencillo de los problemas detectados. |
| `JSON` (pestaña) | Pestaña | Muestra la instantánea JSON completa de los slices y canales DAX. |
| `Refresh Snapshot` | Botón | Vuelve a leer el estado del slice en la instantánea. Haga clic antes de exportar si el estado del slice ha cambiado. |
| `Copy Summary` | Botón | Copia el texto del resumen de problemas al portapapeles. |
| `Copy JSON` | Botón | Copia el JSON completo al portapapeles. |
| `Export JSON...` | Botón | Abre un diálogo de guardar archivo y escribe la instantánea JSON en disco. |
| `Close` | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción de copia o exportación. |

## Consejos

- Haga clic en `Refresh Snapshot` inmediatamente antes de exportar si ha cambiado alguna configuración del slice desde que abrió el diálogo. La exportación escribe lo que se muestra actualmente en la pestaña `JSON`.
- Si necesita pegar la instantánea directamente en un formulario web o correo electrónico en lugar de adjuntar un archivo, use `Copy JSON` en su lugar.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
