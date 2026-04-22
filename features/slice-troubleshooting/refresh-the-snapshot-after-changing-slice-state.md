# Actualizar el snapshot después de cambiar el estado de un slice

El diálogo Slice Troubleshooting captura el estado del radio en el momento en que se abre. Si cambia algún parámetro de un slice — como quitarle el silencio, cambiar la antena o ajustar la asignación de canal DAX — haga clic en **Refresh Snapshot** para cargar el estado actualizado en el diálogo antes de revisar el resumen o compartir datos con soporte.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo no está disponible sin una conexión de radio activa.
- Abra el diálogo mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Realice los cambios al estado del slice en la ventana principal de AetherSDR (por ejemplo, quite el silencio a un slice, cambie la antena o ajuste un canal DAX).
2. Regrese al diálogo Slice Troubleshooting.
3. Haga clic en **Refresh Snapshot**.
4. Revise la etiqueta de estado en la parte inferior del diálogo. Mostrará algo como `Snapshot refreshed: 2 slice(s), 4 global meter(s), 48 total meter(s).`, lo que confirma que la actualización se completó.
5. Revise los resultados actualizados en la pestaña **Issue Summary** o en la pestaña **JSON**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Issue Summary** | Pestaña | Lista con viñetas en lenguaje sencillo de los problemas detectados, como audio ausente, silencio bloqueado o antena faltante. |
| **JSON** | Pestaña | Snapshot completo en JSON de los slices y canales DAX. |
| **Refresh Snapshot** | Botón | Vuelve a leer el estado del slice en el snapshot. Actualiza ambas pestañas y la etiqueta de estado. |
| **Copy Summary** | Botón | Copia el texto del resumen de problemas al portapapeles. |
| **Copy JSON** | Botón | Copia el JSON completo al portapapeles. |
| **Export JSON...** | Botón | Abre un diálogo de guardado y escribe el JSON en un archivo. |
| **Close** | Botón | Cierra el diálogo. |

## Sugerencias

- El diálogo lee desde el modelo en memoria de AetherSDR, no consultando el radio directamente. Si el radio aún no ha propagado un cambio de vuelta al cliente, espere un momento antes de hacer clic en **Refresh Snapshot**.
- Después de actualizar, use **Copy Summary** o **Copy JSON** para capturar el nuevo estado y adjuntarlo a un informe de error o solicitud de soporte.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar un snapshot de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje sencillo de problemas detectados en slices](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar el snapshot JSON completo al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar el snapshot a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
