# Inspeccione los parámetros RF/IF, offset y banderas de validez de cada transversor para diagnóstico XVTR

El diálogo Slice Troubleshooting captura una instantánea de cada transversor configurado en su FLEX-8600 y muestra su frecuencia RF, frecuencia IF, offset de frecuencia y banderas de validez. Úselo cuando un slice basado en transversor se comporte incorrectamente — frecuencia errónea, recepción ausente o modo inesperado — y necesite confirmar qué reporta realmente el radio para cada entrada XVTR.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión de radio activa.
- Cualquier transversor que desee inspeccionar ya debe estar configurado en el FLEX-8600.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo Slice Troubleshooting.
2. Haga clic en la pestaña `Issue Summary`. Examine la lista de viñetas para detectar advertencias de validez XVTR. El resumen marca entradas donde `is_valid` es falso o `has_is_valid` es falso.
3. Haga clic en la pestaña `JSON` para ver la instantánea completa. Localice las entradas del transversor en el JSON. Cada entrada XVTR reporta los siguientes campos:
   - `name` — la etiqueta asignada al transversor
   - `index` y `order` — identificadores de posición
   - `rf_freq_mhz` — la frecuencia RF (radiada) en MHz
   - `if_freq_mhz` — la frecuencia IF (entrada de radio) en MHz
   - `offset_mhz` — la diferencia aplicada entre IF y RF, en MHz
   - `is_valid` — si la entrada del transversor está marcada como válida (`Yes` / `No`)
   - `has_is_valid` — si el radio reportó una bandera de validez en absoluto (`Yes` / `No`)
   - `rx_only` — si la entrada es solo recepción
   - `max_power` — potencia máxima en la entrada XVTR
4. Si realizó cambios en la configuración del transversor después de abrir el diálogo, haga clic en `Refresh Snapshot` para releer el estado actual desde el radio antes de sacar conclusiones.
5. Para compartir los hallazgos, haga clic en `Copy Summary` para copiar la lista de problemas en lenguaje natural al portapapeles, `Copy JSON` para copiar el JSON completo, o `Export JSON...` para guardar el JSON en un archivo.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control             | Tipo   | Comportamiento                                                                                        |
|---------------------|--------|-------------------------------------------------------------------------------------------------|
| `Issue Summary` tab | Pestaña    | Lista de viñetas en lenguaje natural de problemas detectados, incluyendo enrutamiento de audio, estado DSP, dispositivo de control (MIDI), propiedad multicliente y problemas de validez XVTR. |
| `JSON` tab          | Pestaña    | Instantánea JSON completa (versión de esquema 3) que contiene slices, canales DAX, dispositivos de audio, DSP de cliente, dispositivos de control, configuración de banda TX y todas las entradas del transversor con campos RF, IF, offset y validez. |
| `Refresh Snapshot`  | Botón | Relee el estado del slice en la instantánea.                                                         |
| `Copy Summary`      | Botón | Copia el resumen de problemas al portapapeles.                                                      |
| `Copy JSON`         | Botón | Copia la instantánea JSON completa al portapapeles.                                                 |
| `Export JSON...`    | Botón | Guarda la instantánea JSON completa en un archivo.                                                        |
| `Close`             | Botón | Cierra el diálogo.                                                                              |

## Campos de recepción de audio remoto en la instantánea

v0.9.4 añade estado de recepción de audio remoto a las secciones de nivel de radio y por slice del resumen de problemas e instantánea JSON. Estos campos ayudan a diagnosticar problemas donde AetherSDR ha solicitado un flujo de audio remoto desde el radio pero el audio no está fluyendo.

### Audio remoto RX a nivel de radio

En el resumen de problemas, busque la línea que comienza con **Remote audio RX:**. Reporta lo siguiente:

| Campo              | Significado                                                                 |
|--------------------|-------------------------------------------------------------------------|
| `stream_id`        | El identificador de flujo asignado por el radio, o `—` si ninguno.           |
| `stream_expected`  | Si AetherSDR espera que este flujo exista (`Yes` / `No`).         |
| `create_pending`   | Si una solicitud de creación aún está pendiente (`Yes` / `No`).          |
| `status_seen`      | Si se ha recibido una actualización de estado para este flujo (`Yes` / `No`). |
| `owned_by_us`      | Si este cliente posee el flujo (`Yes` / `No`).                    |
| `compression`      | El tipo de compresión en uso, o `—` si no se reportó.                   |

Una segunda línea, **Remote audio route note:**, contiene una nota en lenguaje natural sobre el estado del enrutamiento, o `—` si ninguna fue generada.

### Ruta del flujo de radio por slice

En el resumen de problemas, busque la línea que comienza con **Radio stream route: remote_audio_rx**. Reporta lo siguiente:

| Campo                           | Significado                                                                   |
|---------------------------------|---------------------------------------------------------------------------|
| `remote_audio_rx_stream_id`     | El identificador de flujo para la recepción de audio remoto de este slice, o `—` si ninguno.  |
| `remote_audio_rx_expected`      | Si se espera que el flujo exista.                                  |
| `remote_audio_rx_create_pending`| Si una solicitud de creación aún está pendiente.                            |
| `remote_audio_rx_remove_requested` | Si se ha enviado una solicitud de eliminación pero aún no se ha confirmado.          |
| `remote_audio_rx_status_seen`   | Si se ha recibido una actualización de estado para este flujo.                |
| `remote_audio_rx_owned_by_us`   | Si este cliente posee el flujo.                                      |

Si `remote_audio_rx_expected` es verdadero pero `remote_audio_rx_status_seen` es falso, el radio aún no ha confirmado el flujo. Si `create_pending` es verdadero durante un período prolongado, la solicitud de creación puede no haber llegado al radio.

## Consejos

- Si `has_is_valid` es `No` para un transversor, el radio no reportó una bandera de validez para esa entrada en absoluto. Esto es distinto a que `is_valid` sea `No`, lo que significa que el radio reportó la entrada como explícitamente inválida.
- Haga clic en `Refresh Snapshot` después de ajustar la configuración del transversor en SmartSDR o en el radio antes de releer los valores. La instantánea no se actualiza automáticamente.
- El campo `offset_mhz` debe ser igual a `rf_freq_mhz` menos `if_freq_mhz`. Si no coincide con la configuración del transversor, esa discrepancia es una probable causa de errores de frecuencia en el slice.
- Al investigar audio faltante, primero verifique los campos de recepción de audio remoto. Si `owned_by_us` es `No` y `stream_expected` es `Yes`, otro cliente puede haber asumido la propiedad del flujo.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Lea una lista en lenguaje natural de problemas de slice sospechosos](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualice la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Exporte la instantánea a un archivo para adjuntarla a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
