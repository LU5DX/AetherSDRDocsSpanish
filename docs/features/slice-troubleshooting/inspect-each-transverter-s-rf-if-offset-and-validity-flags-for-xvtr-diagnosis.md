# Inspeccionar RF/IF, desplazamiento e indicadores de validez de cada transverter para el diagnóstico XVTR

El diálogo Slice Troubleshooting captura un instantánea de todos los transverters configurados en su FLEX-8600 y muestra su frecuencia RF, frecuencia IF, desplazamiento de frecuencia e indicadores de validez. Utilícelo cuando un slice basado en transverter presente problemas — frecuencia incorrecta, recepción ausente o modo inesperado — y necesite confirmar lo que el radio reporta realmente para cada entrada XVTR.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión activa con el radio.
- Los transverters que desee inspeccionar deben estar ya configurados en el FLEX-8600.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo Slice Troubleshooting.
2. Haga clic en la pestaña `Issue Summary`. Revise la lista de elementos en busca de advertencias de validez XVTR. El resumen marca las entradas donde `is_valid` es false o `has_is_valid` es false.
3. Haga clic en la pestaña `JSON` para ver la instantánea completa. Localice las entradas de transverter en el JSON. Cada entrada XVTR reporta los siguientes campos:
   - `name` — la etiqueta asignada al transverter
   - `index` y `order` — identificadores de posición
   - `rf_freq_mhz` — la frecuencia RF (sobre el aire) en MHz
   - `if_freq_mhz` — la frecuencia IF (entrada del radio) en MHz
   - `offset_mhz` — la diferencia aplicada entre IF y RF, en MHz
   - `is_valid` — indica si la entrada del transverter está marcada como válida (`Yes` / `No`)
   - `has_is_valid` — indica si el radio reportó un indicador de validez (`Yes` / `No`)
   - `rx_only` — indica si la entrada es solo de recepción
   - `max_power` — potencia máxima en la entrada XVTR
4. Si realizó cambios en la configuración del transverter después de abrir el diálogo, haga clic en `Refresh Snapshot` para releer el estado actual del radio antes de sacar conclusiones.
5. Para compartir los hallazgos, haga clic en `Copy Summary` para copiar la lista de problemas en lenguaje natural al portapapeles, en `Copy JSON` para copiar el JSON completo, o en `Export JSON...` para guardar el JSON en un archivo.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Pestaña `Issue Summary` | Pestaña | Lista de elementos en lenguaje natural con los problemas detectados, incluidos los problemas de validez XVTR. |
| Pestaña `JSON` | Pestaña | Instantánea JSON completa con todas las entradas de transverter, incluyendo campos de RF, IF, desplazamiento y validez. |
| `Refresh Snapshot` | Botón | Relee el estado del slice y del transverter desde el radio hacia la instantánea. |
| `Copy Summary` | Botón | Copia el resumen de problemas al portapapeles. |
| `Copy JSON` | Botón | Copia la instantánea JSON completa al portapapeles. |
| `Export JSON...` | Botón | Guarda la instantánea JSON completa en un archivo. |
| `Close` | Botón | Cierra el diálogo. |

## Consejos

- Si `has_is_valid` es `No` para un transverter, el radio no reportó ningún indicador de validez para esa entrada. Esto es distinto a que `is_valid` sea `No`, lo cual significa que el radio reportó la entrada como explícitamente inválida.
- Haga clic en `Refresh Snapshot` después de ajustar la configuración del transverter en SmartSDR o en el radio antes de releer los valores. La instantánea no se actualiza automáticamente.
- El campo `offset_mhz` debe ser igual a `rf_freq_mhz` menos `if_freq_mhz`. Si no coincide con la configuración de su transverter, esa discrepancia es una causa probable de errores de frecuencia en el slice.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje natural de posibles problemas de slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
