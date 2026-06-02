# Inspeccionar los parámetros RF/FI, desviación y banderas de validez de cada transvertidor para diagnosis de XVTR

El diálogo de Solución de Problemas del Slice captura una instantánea de cada transvertidor configurado en su FLEX-8600 y muestra su frecuencia RF, frecuencia FI, desviación de frecuencia y banderas de validez. Úselo cuando un slice basado en transvertidor se comporte de manera incorrecta — frecuencia errónea, recepción ausente o modo inesperado — y necesite confirmar qué reporta realmente la radio para cada entrada XVTR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo requiere una conexión activa con la radio.
- Los transvertidores que desee inspeccionar deben estar configurados en el FLEX-8600.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo de Solución de Problemas del Slice.
2. Haga clic en la pestaña `Issue Summary`. Examine la lista con viñetas en busca de advertencias de validez de XVTR. El resumen señala las entradas donde `is_valid` es falso o `has_is_valid` es falso.
3. Haga clic en la pestaña `JSON` para ver la instantánea completa. Localice las entradas de transvertidor en el JSON. Cada entrada XVTR reporta los siguientes campos:
   - `name` — la etiqueta asignada al transvertidor
   - `index` y `order` — identificadores de posición
   - `rf_freq_mhz` — la frecuencia RF (por el aire) en MHz
   - `if_freq_mhz` — la frecuencia FI (entrada de la radio) en MHz
   - `offset_mhz` — la diferencia aplicada entre FI y RF, en MHz
   - `is_valid` — si la entrada del transvertidor está marcada como válida (`Yes` / `No`)
   - `has_is_valid` — si la radio reportó una bandera de validez (`Yes` / `No`)
   - `rx_only` — si la entrada es solo de recepción
   - `max_power` — potencia máxima en la entrada XVTR
4. Si realizó cambios en la configuración del transvertidor después de abrir el diálogo, haga clic en `Refresh Snapshot` para volver a leer el estado actual desde la radio antes de sacar conclusiones.
5. Para compartir los hallazgos, haga clic en `Copy Summary` para copiar la lista de problemas en lenguaje sencillo al portapapeles, `Copy JSON` para copiar el JSON completo, o `Export JSON...` para guardar el JSON en un archivo.
6. Haga clic en `Close` al finalizar.

## Función de cada control

| Control             | Tipo   | Comportamiento                                                                                       |
|---------------------|--------|------------------------------------------------------------------------------------------------------|
| `Issue Summary` tab | Pestaña | Lista con viñetas en lenguaje sencillo de problemas detectados, incluyendo enrutamiento de audio, DSP, estado de dispositivos de control (MIDI), estado de puntos finales de audio, propiedad multicliente, estado de conexión del slice al panadapter, y problemas de validez de XVTR. |
| `JSON` tab          | Pestaña | Instantánea JSON completa (versión de esquema 3) que contiene slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, puntos finales de audio, configuraciones de banda TX y todas las entradas de transvertidor con campos de RF, FI, desviación y validez. |
| `Refresh Snapshot`  | Botón  | Vuelve a leer el estado del slice en la instantánea.                                                |
| `Copy Summary`      | Botón  | Copia el resumen de problemas al portapapeles.                                                       |
| `Copy JSON`         | Botón  | Copia la instantánea JSON completa al portapapeles.                                                  |
| `Export JSON...`    | Botón  | Guarda la instantánea JSON completa en un archivo.                                                   |
| `Status label`      | Etiqueta | Muestra el último resultado de copia/exportación (ej. "Copied to clipboard").                     |
| `Close`             | Botón  | Cierra el diálogo.                                                                                   |

## Estado de conexión del slice al panadapter en la instantánea

v26.6.1 añade información del estado de conexión del slice a la sección del panadapter en el Resumen de Problemas. Cuando un panadapter tiene detalles de conexión del slice disponibles, la línea de resumen para ese panadapter incluye un bloque `slice_connection_status` con los siguientes campos:

| Campo                  | Significado                                                              |
|------------------------|--------------------------------------------------------------------------|
| `state`                | El estado de conexión (ej. "connected", "disconnected", "unknown").      |
| `summary`              | Una descripción en lenguaje sencillo del estado del enlace del slice.    |
| `connected_slice_ids`  | Lista separada por comas de IDs de slice actualmente conectados a este panadapter, o "none". |
| `active_slice_ids`     | Lista separada por comas de IDs de slice activos, o "none".              |
| `attention_required`   | Si el estado de conexión requiere atención (se añade `(attention)`).     |

## Campos de punto final de audio en la instantánea

v26.6.1 añade el estado del punto final de audio a la instantánea. Cada punto final de audio aparece en el Resumen de Problemas con los siguientes detalles:

| Campo                  | Significado                                                              |
|------------------------|--------------------------------------------------------------------------|
| `name`                 | El nombre del punto final.                                               |
| `direction`            | Dirección (`INPUT` o `OUTPUT`).                                          |
| `kind`                 | Tipo de punto final (ej. "endpoint").                                    |
| `operational`          | Si el punto final es operativo (`Yes` / `No`).                           |
| `running`              | Si el punto final está en ejecución (`Yes` / `No`).                      |
| `state`                | Cadena de estado actual.                                                 |
| `error`                | Cadena de error, o "n/a" si no hay.                                      |
| `backend`              | Nombre del backend de audio.                                             |
| `device`               | Nombre del dispositivo, o "Unavailable".                                 |
| `sample_rate_hz`       | Frecuencia de muestreo en Hz.                                            |
| `channel_count`        | Número de canales.                                                       |
| `sample_format`        | Cadena de formato de muestra.                                            |
| `resampling_active`    | Si el remuestreo está activo.                                            |
| `buffer_bytes`         | Tamaño actual del búfer en bytes (si está disponible).                   |
| `buffer_peak_bytes`    | Tamaño máximo del búfer en bytes (si está disponible).                   |
| `underrun_count`       | Número de subejecuciones (si está disponible).                           |
| `note`                 | Nota adicional en lenguaje sencillo sobre el punto final.                |

## Campos de audio RX remoto en la instantánea

v0.9.4 añade el estado de audio RX remoto tanto en la sección a nivel de radio como en la de cada slice del Resumen de Problemas y la instantánea JSON. Estos campos ayudan a diagnosticar problemas cuando AetherSDR ha solicitado un flujo de audio remoto desde la radio pero el audio no fluye.

### Audio RX remoto a nivel de radio

En el Resumen de Problemas, busque la línea que comienza con **Remote audio RX:**. Reporta lo siguiente:

| Campo              | Significado                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| `stream_id`        | El identificador de flujo asignado por la radio, o `—` si no hay ninguno.  |
| `stream_expected`  | Si AetherSDR espera que este flujo exista (`Yes` / `No`).                   |
| `create_pending`   | Si una solicitud de creación aún está pendiente (`Yes` / `No`).             |
| `status_seen`      | Si se ha recibido una actualización de estado para este flujo (`Yes` / `No`). |
| `owned_by_us`      | Si este cliente posee el flujo (`Yes` / `No`).                              |
| `compression`      | El tipo de compresión en uso, o `—` si no se reporta.                       |

Una segunda línea, **Remote audio route note:**, contiene una nota en lenguaje sencillo sobre el estado de enrutamiento, o `—` si no se generó ninguna.

### Ruta de flujo de radio por slice

En el Resumen de Problemas, busque la línea que comienza con **Radio stream route: remote_audio_rx**. Reporta lo siguiente:

| Campo                           | Significado                                                                   |
|---------------------------------|-------------------------------------------------------------------------------|
| `remote_audio_rx_stream_id`     | El identificador de flujo para el audio RX remoto de este slice, o `—` si no. |
| `remote_audio_rx_expected`      | Si se espera que exista el flujo.                                             |
| `remote_audio_rx_create_pending`| Si una solicitud de creación aún está pendiente.                              |
| `remote_audio_rx_remove_requested` | Si se ha enviado una solicitud de eliminación pero aún no se ha confirmado.|
| `remote_audio_rx_status_seen`   | Si se ha recibido una actualización de estado para este flujo.                |
| `remote_audio_rx_owned_by_us`   | Si este cliente posee el flujo.                                               |

Si `remote_audio_rx_expected` es verdadero pero `remote_audio_rx_status_seen` es falso, la radio aún no ha confirmado el flujo. Si `create_pending` es verdadero durante un período prolongado, es posible que la solicitud de creación no haya llegado a la radio.

## Consejos

- Si `has_is_valid` es `No` para un transvertidor, la radio no reportó una bandera de validez para esa entrada en absoluto. Esto es diferente a que `is_valid` sea `No`, lo que significa que la radio reportó la entrada como explícitamente inválida.
- Haga clic en `Refresh Snapshot` después de ajustar la configuración del transvertidor en SmartSDR o en la radio antes de volver a leer los valores. La instantánea no se actualiza automáticamente.
- El campo `offset_mhz` debe ser igual a `rf_freq_mhz` menos `if_freq_mhz`. Si no coincide con su configuración del transvertidor, esa discrepancia es una causa probable de errores de frecuencia en el slice.
- Al investigar audio faltante, revise primero los campos de audio RX remoto. Si `owned_by_us` es `No` y `stream_expected` es `Yes`, otro cliente puede haber tomado posesión del flujo.
- Al investigar problemas de conexión del panadapter, revise el campo `slice_connection_status`. Si `attention_required` es verdadero, se necesita una investigación adicional.
- Las subejecuciones del punto final de audio indicadas por un `underrun_count` distinto de cero pueden apuntar a problemas de rendimiento o configuración del búfer.

## Relacionados

- [Slice Troubleshooting overview](overview.md)
- [Read a plain-language list of suspected slice problems](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Refresh the snapshot after changing slice state](refresh-the-snapshot-after-changing-slice-state.md)
- [Export the snapshot to a file to attach to a bug report](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
