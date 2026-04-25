# Actualizar la instantánea tras cambiar el estado de un slice

El diálogo Slice Troubleshooting captura una instantánea del estado del slice (porción de espectro) al abrirse. Si cambia algo — desactiva el silencio de un slice, cambia de antena, ajusta DAX — los datos mostrados quedan desactualizados. Al hacer clic en `Refresh Snapshot` se vuelve a leer el estado actual, de modo que el resumen y el JSON reflejen los cambios realizados.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión activa al radio.
- Abra el diálogo Slice Troubleshooting desde `Help > Slice Troubleshooting...`.

## Pasos

1. Realice el cambio en el slice que desea capturar (por ejemplo, desactive el silencio de un slice o reasigne una antena).
2. En el diálogo Slice Troubleshooting, haga clic en `Refresh Snapshot`.
3. Revise la pestaña `Issue Summary` para confirmar que el estado actualizado se refleja en la lista de problemas.
4. Cambie a la pestaña `JSON` si necesita verificar los valores sin procesar.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `Refresh Snapshot` | Botón | Vuelve a leer el estado del slice en la instantánea. Tanto la pestaña `Issue Summary` como la pestaña `JSON` se actualizan. |
| `Issue Summary` (pestaña) | Pestaña | Lista con viñetas en lenguaje claro de los problemas detectados en función de la instantánea actual. |
| `JSON` (pestaña) | Pestaña | Instantánea JSON completa de los slices y canales DAX basada en la instantánea actual. |
| `Copy Summary` | Botón | Copia el resumen de problemas al portapapeles. |
| `Copy JSON` | Botón | Copia el JSON completo al portapapeles. |
| `Export JSON...` | Botón | Guarda el JSON en un archivo. |
| `Close` | Botón | Cierra el diálogo. |
| Etiqueta de estado | Indicador | Muestra el último resultado de copia o exportación, por ejemplo `Copied to clipboard`. |

## Consejos

- El diálogo no consulta el radio de forma continua. Cualquier cambio de estado realizado después de abrir el diálogo no aparecerá hasta que haga clic en `Refresh Snapshot`.
- Tras actualizar, use `Copy Summary` o `Copy JSON` para capturar los datos actualizados e incluirlos en un informe de soporte.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Leer la lista en lenguaje claro de posibles problemas de slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
