# Inspeccionar RF/FI, desplazamiento y banderas de validez de cada transvertidor para diagnóstico de XVTR

El cuadro de diálogo de solución de problemas de slices captura una instantánea de cada transvertidor configurado en su FLEX-8600 y muestra su frecuencia RF, frecuencia FI, desplazamiento de frecuencia y banderas de validez. Utilícelo cuando un slice basado en transvertidor se comporte incorrectamente — frecuencia errónea, falta de recepción o modo inesperado — y necesite confirmar qué reporta realmente la radio para cada entrada XVTR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El cuadro de diálogo requiere una conexión activa con la radio.
- Los transvertidores que desee inspeccionar ya deben estar configurados en el FLEX-8600.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el cuadro de diálogo de solución de problemas de slices.
2. Haga clic en la pestaña `Issue Summary`. Revise la lista con viñetas en busca de advertencias de validez XVTR. El resumen marca las entradas donde `is_valid` es falso o `has_is_valid` es falso.
3. Haga clic en la pestaña `JSON` para ver la instantánea completa. Localice las entradas de transvertidores en el JSON. Cada entrada XVTR reporta los siguientes campos:
   - `name` — la etiqueta asignada al transvertidor
   - `index` y `order` — identificadores de posición
   - `rf_freq_mhz` — la frecuencia RF (por el aire) en MHz
   - `if_freq_mhz` — la frecuencia FI (entrada de la radio) en MHz
   - `offset_mhz` — la diferencia aplicada entre FI y RF, en MHz
   - `is_valid` — si la entrada del transvertidor está marcada como válida (`Yes` / `No`)
   - `has_is_valid` — si la radio reportó una bandera de validez en absoluto (`Yes` / `No`)
   - `rx_only` — si la entrada es solo de recepción
   - `max_power` — potencia máxima en la entrada XVTR
4. Si realizó cambios en la configuración del transvertidor después de abrir el cuadro de diálogo, haga clic en `Refresh Snapshot` para volver a leer el estado actual desde la radio antes de sacar conclusiones.
5. Para compartir los hallazgos, haga clic en `Copy Summary` para copiar la lista de problemas en lenguaje sencillo al portapapeles, `Copy JSON` para copiar el JSON completo, o `Export JSON...` para guardar el JSON en un archivo.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control             | Tipo    | Comportamiento                                                                                     |
|---------------------|---------|----------------------------------------------------------------------------------------------------|
| `Issue Summary` tab | Pestaña | Lista con viñetas en lenguaje sencillo de los problemas detectados, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI), estado del punto final de audio, propiedad multi-cliente, estado de conexión del slice del panadapter y problemas de validez XVTR. |
| `JSON` tab          | Pestaña | Instantánea JSON completa (esquema versión 3) que contiene slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, puntos finales de audio, configuraciones de banda TX y todas las entradas de transvertidores con campos RF, FI, desplazamiento y validez. |
| `Refresh Snapshot`  | Botón   | Vuelve a leer el estado del slice en la instantánea.                                               |
| `Copy Summary`      | Botón   | Copia el resumen de problemas al portapapeles.                                                     |
| `Copy JSON`         | Botón   | Copia la instantánea JSON completa al portapapeles.                                                |
| `Export JSON...`    | Botón   | Guarda la instantánea JSON completa en un archivo.                                                 |
| `Status label`      | Etiqueta| Muestra el último resultado de copia/exportación (ej. "Copied to clipboard").                     |
| `Close`             | Botón   | Cierra el cuadro de diálogo.                                                                       |

## Estado de conexión del slice del panadapter en la instantánea

v26.6.1 agrega información del estado de conexión del slice a la sección del panadapter del Issue Summary. Cuando un panadapter tiene detalles de conexión del slice disponibles, la línea de resumen para ese panadapter incluye un bloque `slice_connection_status` con los siguientes campos:

| Campo                  | Significado                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| `state`                | El estado de la conexión (ej. "connected", "disconnected", "unknown").     |
| `summary`              | Una descripción en lenguaje sencillo del estado del enlace del slice.       |
| `connected_slice_ids`  | Lista separada por comas de IDs de slice conectados actualmente a este panadapter, o "none". |
| `active_slice_ids`     | Lista separada por comas de IDs de slice activos, o "none".                 |
| `attention_required`   | Si el estado de conexión requiere atención (`(attention)` añadido).       |

## Campos de punto final de audio en la instantánea

v26.6.1 agrega el estado del punto final de audio a la instantánea. Cada punto final de audio aparece en el Issue Summary con los siguientes detalles:

| Campo                  | Significado                                                               |
|------------------------|---------------------------------------------------------------------------|
| `name`                 | El nombre del punto final.                                                |
| `direction`            | Dirección (`INPUT` o `OUTPUT`).                                            |
| `kind`                 | Tipo de punto final (ej. "endpoint").                                     |
| `operational`          | Si el punto final es operativo (`Yes` / `No`).                           |
| `running`              | Si el punto final está en ejecución (`Yes` / `No`).                      |
| `state`                | Cadena de estado actual.                                                  |
| `error`                | Cadena de error, o "n/a" si no hay.                                       |
| `backend`              | Nombre del backend de audio.                                              |
| `device`               | Nombre del dispositivo, o "Unavailable".                                  |
| `sample_rate_hz`       | Frecuencia de muestreo en Hz.                                             |
| `channel_count`        | Número de canales.                                                        |
| `sample_format`        | Cadena de formato de muestra.                                             |
| `resampling_active`    | Si el remuestreo está activo.                                             |
| `buffer_bytes`         | Tamaño actual del búfer en bytes (si está disponible).                    |
| `buffer_peak_bytes`    | Tamaño máximo del búfer en bytes (si está disponible).                    |
| `underrun_count`       | Número de subejecuciones (si está disponible).                            |
| `note`                 | Nota adicional en lenguaje sencillo sobre el punto final.                 |

## Campos de RX de audio remoto en la instantánea

v0.9.4 agrega el estado de RX de audio remoto tanto a nivel de radio como por slice en el Issue Summary y la instantánea JSON. Estos campos ayudan a diagnosticar problemas donde AetherSDR ha solicitado un flujo de audio remoto desde la radio pero el audio no fluye.

### RX de audio remoto a nivel de radio

En el Issue Summary, busque la línea que comienza con **Remote audio RX:**. Reporta lo siguiente:

| Campo              | Significado                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| `stream_id`        | El identificador de flujo asignado por la radio, o `—` si ninguno.         |
| `stream_expected`  | Si AetherSDR espera que este flujo exista (`Yes` / `No`).                  |
| `create_pending`   | Si una solicitud de creación aún está pendiente (`Yes` / `No`).           |
| `status_seen`      | Si se ha recibido una actualización de estado para este flujo (`Yes` / `No`). |
| `owned_by_us`      | Si este cliente posee el flujo (`Yes` / `No`).                            |
| `compression`      | El tipo de compresión en uso, o `—` si no se reporta.                     |

Una segunda línea, **Remote audio route note:**, contiene una nota en lenguaje sencillo sobre el estado del enrutamiento, o `—` si no se generó ninguna.

### Ruta de flujo de radio por slice

En el Issue Summary, busque la línea que comienza con **Radio stream route: remote_audio_rx**. Reporta lo siguiente:

| Campo                           | Significado                                                                   |
|---------------------------------|-------------------------------------------------------------------------------|
| `remote_audio_rx_stream_id`     | El identificador de flujo para el RX de audio remoto de este slice, o `—` si ninguno. |
| `remote_audio_rx_expected`      | Si se espera que el flujo exista.                                             |
| `remote_audio_rx_create_pending`| Si una solicitud de creación aún está pendiente.                              |
| `remote_audio_rx_remove_requested` | Si se ha enviado una solicitud de eliminación pero aún no se ha confirmado. |
| `remote_audio_rx_status_seen`   | Si se ha recibido una actualización de estado para este flujo.                |
| `remote_audio_rx_owned_by_us`   | Si este cliente posee el flujo.                                               |

Si `remote_audio_rx_expected` es verdadero pero `remote_audio_rx_status_seen` es falso, la radio aún no ha confirmado el flujo. Si `create_pending` es verdadero durante un período prolongado, la solicitud de creación puede no haber llegado a la radio.

## Campos de la instantánea DSP del cliente en la pestaña JSON

v26.7.4 agrega campos de configuración adicionales de NR2 (Reducción de Ruido 2) a la instantánea JSON. La sección DSP del cliente del JSON ahora incluye:

| Campo                              | Significado                                                                                     |
|------------------------------------|-------------------------------------------------------------------------------------------------|
| `nr2.gain_method`                  | El nombre del método de ganancia NR2 actual.                                                    |
| `nr2.gain_method_id`               | El identificador numérico del método de ganancia.                                               |
| `nr2.npe_method`                   | El nombre del método de estimación de potencia de ruido NR2 actual.                             |
| `nr2.npe_method_id`                | El identificador numérico del método NPE.                                                       |
| `nr2.ae_filter`                    | Si el filtro adaptativo de eco está habilitado (`true` / `false`).                             |
| `nr2.gain_max`                     | El valor máximo de ganancia.                                                                    |
| `nr2.gain_floor`                   | El valor mínimo del piso de ganancia (nuevo en v26.7.4).                                       |
| `nr2.gain_smooth`                  | El factor de suavizado de ganancia.                                                             |
| `nr2.qspp`                         | El valor percentil de potencia cuasi-estacionaria.                                              |
| `nr2.legacy_geometry_and_gain_mapping` | Si se utiliza el mapeo de geometría y ganancia heredado (nuevo en v26.7.4).              |

## Consejos

- Si `has_is_valid` es `No` para un transvertidor, la radio no reportó ninguna bandera de validez para esa entrada. Esto es diferente a que `is_valid` sea `No`, lo que significa que la radio reportó la entrada como explícitamente inválida.
- Haga clic en `Refresh Snapshot` después de ajustar la configuración del transvertidor en SmartSDR o en la radio antes de volver a leer los valores. La instantánea no se actualiza automáticamente.
- El campo `offset_mhz` debe ser igual a `rf_freq_mhz` menos `if_freq_mhz`. Si no coincide con su configuración de transvertidor, esa discrepancia es una causa probable de errores de frecuencia en el slice.
- Al investigar audio faltante, revise primero los campos de RX de audio remoto. Si `owned_by_us` es `No` y `stream_expected` es `Yes`, otro cliente puede haber tomado posesión del flujo.
- Al investigar problemas de conexión del panadapter, revise el campo `slice_connection_status`. Si `attention_required` es verdadero, se necesita más investigación.
- Las subejecuciones del punto final de audio indicadas por un `underrun_count` distinto de cero pueden apuntar a problemas de rendimiento o configuración del búfer.

## Relacionados

- [Descripción general de solución de problemas de slices](overview.md)
- [Leer una lista en lenguaje sencillo de posibles problemas del slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
