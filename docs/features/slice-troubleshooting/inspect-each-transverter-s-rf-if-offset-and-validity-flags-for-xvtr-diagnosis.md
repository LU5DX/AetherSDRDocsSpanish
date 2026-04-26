# Inspeccionar RF/IF, desplazamiento e indicadores de validez de cada transverter para diagnóstico XVTR

El diálogo Slice Troubleshooting captura una instantánea que incluye una entrada formateada para cada transverter que el radio reporta. Úselo para verificar que la frecuencia RF, la frecuencia IF, el desplazamiento y los indicadores de validez de un transverter son los esperados, sin necesidad de analizar la salida bruta del protocolo SmartSDR.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión activa con el radio.
- Al menos un transverter debe estar configurado en el FLEX-8600 para que aparezcan entradas XVTR en la instantánea.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo Slice Troubleshooting.
2. Haga clic en la pestaña `JSON (tab)` para ver la instantánea completa, o haga clic en la pestaña `Issue Summary (tab)` para obtener un resumen en lenguaje sencillo que señala los problemas de validez XVTR.
3. Localice las entradas de transverter en la salida. Cada transverter se reporta con el siguiente formato:

   ```
   - `<name>` idx `<index>`, order `<order>`, RF `<rf_freq_mhz> MHz`, IF `<if_freq_mhz> MHz`, offset `<offset_mhz> MHz`, valid `<Yes/No>`, has is_valid `<Yes/No>`, rx only `<Yes/No>`, max power `<max_power>`
   ```

4. Compruebe el campo `valid`. Si muestra `No`, el radio no considera válido el transverter. Compruebe el campo `has is_valid`: si también muestra `No`, el radio aún no ha reportado un estado de validez para ese transverter.
5. Verifique que los valores `RF`, `IF` y `offset` coincidan con la configuración de su transverter.
6. Si modificó los ajustes del transverter en el radio después de abrir el diálogo, haga clic en `Refresh Snapshot` para releer el estado actual.
7. Para compartir los datos con soporte técnico, haga clic en `Copy JSON` para copiar la instantánea completa al portapapeles, o haga clic en `Export JSON...` para guardarla en un archivo. Para copiar solo el resumen de problemas, haga clic en `Copy Summary`.
8. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `Issue Summary (tab)` | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados, incluidos los problemas de validez XVTR. |
| `JSON (tab)` | Pestaña | Muestra la instantánea JSON completa, incluidas todas las entradas de transverter con los campos RF, IF, desplazamiento y validez. |
| `Refresh Snapshot` | Botón | Relee el estado del slice y del transverter desde el radio hacia la instantánea. |
| `Copy Summary` | Botón | Copia el texto del resumen de problemas al portapapeles. |
| `Copy JSON` | Botón | Copia la instantánea JSON completa al portapapeles. |
| `Export JSON...` | Botón | Guarda la instantánea JSON completa en un archivo. |
| `Close` | Botón | Cierra el diálogo. |

## Consejos

- El campo `has is_valid` permite distinguir entre un transverter explícitamente inválido y uno cuyo estado de validez simplemente no se ha recibido aún. Si `has is_valid` muestra `No`, espere un momento y haga clic en `Refresh Snapshot` antes de sacar conclusiones.
- El valor `offset` se deriva de las frecuencias RF e IF. Si el desplazamiento parece incorrecto, compare los valores `RF` e `IF` con lo que está configurado en el ajuste de transverter del radio.
- La etiqueta de estado en la parte inferior del diálogo confirma el resultado de las acciones de copia y exportación (por ejemplo, mostrará `Copied to clipboard` después de hacer clic en `Copy JSON`).

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje sencillo de posibles problemas de slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar la instantánea tras cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Exportar la instantánea a un archivo para adjuntar a un reporte de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
