# Inspeccionar los parámetros RF/IF, desplazamiento y banderas de validez de cada transverter para diagnóstico de XVTR

El diálogo Slice Troubleshooting captura una instantánea de cada transverter configurado en su FLEX-8600 y muestra su frecuencia de RF, frecuencia de IF, desplazamiento de frecuencia y banderas de validez. Utilícelo cuando un slice basado en transverter presente problemas — frecuencia incorrecta, recepción ausente o modo inesperado — y necesite confirmar lo que el radio reporta realmente para cada entrada XVTR.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión activa con el radio.
- Los transverters que desee inspeccionar deben estar ya configurados en el FLEX-8600.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo Slice Troubleshooting.
2. Haga clic en la pestaña `Issue Summary`. Revise la lista de puntos en busca de advertencias de validez XVTR. El resumen señala las entradas donde `is_valid` es falso o `has_is_valid` es falso.
3. Haga clic en la pestaña `JSON` para ver la instantánea completa. Localice las entradas de transverter en el JSON. Cada entrada XVTR reporta los siguientes campos:
   - `name` — la etiqueta asignada al transverter
   - `index` y `order` — identificadores de posición
   - `rf_freq_mhz` — la frecuencia de RF (en el aire) en MHz
   - `if_freq_mhz` — la frecuencia de IF (entrada del radio) en MHz
   - `offset_mhz` — la diferencia aplicada entre IF y RF, en MHz
   - `is_valid` — indica si la entrada del transverter está marcada como válida (`Yes` / `No`)
   - `has_is_valid` — indica si el radio reportó una bandera de validez (`Yes` / `No`)
   - `rx_only` — indica si la entrada es solo de recepción
   - `max_power` — potencia máxima en la entrada XVTR
4. Si realizó cambios en la configuración del transverter después de abrir el diálogo, haga clic en `Refresh Snapshot` para releer el estado actual del radio antes de sacar conclusiones.
5. Para compartir los resultados, haga clic en `Copy Summary` para copiar la lista de problemas en lenguaje sencillo al portapapeles, `Copy JSON` para copiar el JSON completo, o `Export JSON...` para guardar el JSON en un archivo.
6. Haga clic en `Close` cuando haya terminado.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Pestaña `Issue Summary` | Pestaña | Lista de puntos en lenguaje sencillo con los problemas detectados, incluidos los problemas de validez XVTR. |
| Pestaña `JSON` | Pestaña | Instantánea JSON completa con todas las entradas de transverter, incluyendo campos de RF, IF, desplazamiento y validez. |
| `Refresh Snapshot` | Botón | Relee el estado de los slices y transverters del radio para actualizar la instantánea. |
| `Copy Summary` | Botón | Copia el resumen de problemas al portapapeles. |
| `Copy JSON` | Botón | Copia la instantánea JSON completa al portapapeles. |
| `Export JSON...` | Botón | Guarda la instantánea JSON completa en un archivo. |
| `Close` | Botón | Cierra el diálogo. |

## Consejos

- Si `has_is_valid` es `No` para un transverter, el radio no reportó ninguna bandera de validez para esa entrada. Esto es distinto de que `is_valid` sea `No`, lo que significa que el radio reportó la entrada como explícitamente inválida.
- Haga clic en `Refresh Snapshot` después de ajustar la configuración del transverter en SmartSDR o en el radio antes de releer los valores. La instantánea no se actualiza automáticamente.
- El campo `offset_mhz` debe ser igual a `rf_freq_mhz` menos `if_freq_mhz`. Si no coincide con la configuración de su transverter, esa discrepancia es probablemente la causa de los errores de frecuencia en el slice.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje sencillo de los problemas detectados en el slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
