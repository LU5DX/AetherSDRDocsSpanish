# Copiar el snapshot JSON completo al portapapeles

Copie el snapshot JSON completo del estado de los slices, el panadapter y los medidores de su radio al portapapeles para pegarlo en un hilo de soporte, un informe de errores o una sesión de diagnóstico asistida por IA.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El diálogo requiere una conexión activa con el radio.
- Abra el diálogo Slice Troubleshooting mediante `Help > Slice Troubleshooting...`.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña **JSON** para confirmar que el contenido del snapshot se vea actualizado.
3. Si recientemente cambió el estado de un slice y desea los datos más recientes, haga clic en **Refresh Snapshot** antes de copiar.
4. Haga clic en **Copy JSON**.
5. La etiqueta de estado en la parte inferior del diálogo muestra **JSON copied to clipboard.**, lo que confirma que la copia se realizó correctamente.
6. Pegue el contenido del portapapeles donde sea necesario.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **JSON** (pestaña) | Pestaña | Muestra el snapshot JSON completo de los slices y los canales DAX. |
| **Refresh Snapshot** | Botón | Vuelve a leer el estado del slice en el snapshot. Haga clic aquí después de cambiar cualquier configuración de slice para asegurarse de que el JSON copiado refleje el estado actual. |
| **Copy JSON** | Botón | Copia el JSON completo al portapapeles. |
| **Export JSON...** | Botón | Guarda el JSON en un archivo en lugar de en el portapapeles. |
| **Copy Summary** | Botón | Copia el resumen del problema en lenguaje natural al portapapeles en lugar del JSON sin procesar. |
| **Close** | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el resultado de la última acción, como **JSON copied to clipboard.** |

## Consejos

- El diálogo no consulta el radio automáticamente. Si realizó cambios desde que abrió el diálogo, haga clic en **Refresh Snapshot** antes de hacer clic en **Copy JSON** para asegurarse de que los datos copiados estén actualizados.
- El snapshot incluye el estado del slice, el estado del panadapter, las lecturas de los medidores, la configuración DSP del cliente y el estado de bloqueo de la interfaz. Todo esto queda capturado en un solo pegado del portapapeles.
- Si necesita un archivo adjunto en lugar de texto en el portapapeles, use **Export JSON...** en su lugar.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar un snapshot de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar el snapshot a un archivo para adjuntarlo a un informe de errores](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar el snapshot después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje natural de posibles problemas del slice](read-a-plain-language-list-of-suspected-slice-problems.md)
