# Inspeccione los flags RF/IF, offset y validez de cada transverter para diagnóstico de XVTR

El diálogo Slice Troubleshooting captura una instantánea de cada transverter configurado en su FLEX-8600 y muestra su frecuencia RF, frecuencia IF, offset de frecuencia y flags de validez. Úselo cuando un slice basado en transverter se comporte de manera incorrecta (frecuencia equivocada, recepción ausente o modo inesperado) y necesite confirmar qué informa realmente la radio para cada entrada XVTR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo requiere una conexión activa con la radio.
- Los transverters que desee inspeccionar ya deben estar configurados en la FLEX-8600.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo Slice Troubleshooting.
2. Haga clic en la pestaña `Issue Summary`. Revise la lista con viñetas para detectar advertencias de validez XVTR. El resumen marca las entradas donde `is_valid` es false o `has_is_valid` es false.
3. Haga clic en la pestaña `JSON` para ver la instantánea completa. Localice las entradas de transverter en el JSON. Cada entrada XVTR informa los siguientes campos:
   - `name` — la etiqueta asignada al transverter
   - `index` y `order` — identificadores de posición
   - `rf_freq_mhz` — la frecuencia RF (por aire) en MHz
   - `if_freq_mhz` — la frecuencia IF (entrada de radio) en MHz
   - `offset_mhz` — la diferencia aplicada entre IF y RF, en MHz
   - `is_valid` — si la entrada del transverter está marcada como válida (`Yes` / `No`)
   - `has_is_valid` — si la radio informó algún flag de validez (`Yes` / `No`)
   - `rx_only` — si la entrada es solo de recepción
   - `max_power` — potencia máxima en la entrada XVTR
4. Si realizó cambios en la configuración de transverters después de abrir el diálogo, haga clic en `Refresh Snapshot` para volver a leer el estado actual desde la radio antes de sacar conclusiones.
5. Para compartir los hallazgos, haga clic en `Copy Summary` para copiar la lista de problemas en lenguaje natural al portapapeles, `Copy JSON` para copiar el JSON completo, o `Export JSON...` para guardar el JSON en un archivo.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control             | Tipo                                                                                           | Comportamiento                                                                                                                                                                                                                    |
|---------------------|------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pestaña `Issue Summary` | Pestaña                                                                                            | Lista con viñetas en lenguaje natural de los problemas detectados, incluyendo ruteo de audio, DSP, estado de dispositivos de control (MIDI), estado de endpoints de audio, propiedad multi-cliente, estado de conexión de slices del panadapter, actividad del medidor TX y problemas de validez XVTR. |
| Pestaña `JSON`          | Pestaña                                                                                            | Instantánea JSON completa (versión de esquema 3) que contiene slices, canales DAX, dispositivos de audio, DSP de cliente, dispositivos de control, endpoints de audio, configuraciones de banda TX y todas las entradas de transverter con campos RF, IF, offset y validez. |
| `Refresh Snapshot`  | Botón                                                                                         | Vuelve a leer el estado de los slices en la instantánea.                                                                                                                                                                                     |
| `Copy Summary`      | Botón                                                                                         | Copia el resumen de problemas al portapapeles.                                                                                                                                                                                  |
| `Copy JSON`         | Botón                                                                                         | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                                             |
| `Export JSON...`    | Botón                                                                                         | Guarda la instantánea JSON completa en un archivo.                                                                                                                                                                                     |
| Find:               | Campo de texto                                                                                     | Resalta las coincidencias del término ingresado en la pestaña activa (Issue Summary o JSON). Tiene botón de borrar y texto de marcador 'Search snapshot...'. Enter salta a la siguiente coincidencia; el uso compartido de pestañas actualiza los contadores de resaltado. La etiqueta de estado muestra '<N> match(es) in current tab.' |
| Find Next           | Botón                                                                                         | Salta a la siguiente coincidencia del término de búsqueda en la pestaña activa. Envuelve dentro de la pestaña actual. Un término vacío no produce coincidencias.                                                                 |
| `Status label`      | Etiqueta                                                                                          | Muestra el último resultado de copia/exportación (por ejemplo, "Copied to clipboard") o el conteo de coincidencias de búsqueda.                                                                                                                                      |
| `Close`             | Botón                                                                                         | Cierra el diálogo.                                                                                                                                                                                                          |

## Actividad del medidor TX en el Issue Summary

v26.8.4 agrega detección de actividad del medidor TX al Issue Summary. Cuando los medidores TX no están activos, el resumen incluye una línea de advertencia similar a:

```
  - ⚠ TX meters are NOT live (last sample 1234 ms ago) — TX forward power is the last value received, not a current reading, and TX SWR is omitted rather than shown stale.
```

La advertencia solo se emite cuando los medidores TX están desactualizados; un grupo activo no produce ninguna advertencia. Esto evita malinterpretar un valor de potencia directa desactualizado como una lectura en vivo cuando el SWR muestra correctamente `n/a`.

Según el estado, la parte entre paréntesis dice `last sample <N> ms ago` (cuando se ha recibido una muestra) o `no TX meter sample this session` (cuando no se ha recibido ninguna muestra en esta sesión).

## Campos de endpoints de audio en la instantánea

v26.6.1 agrega el estado de endpoints de audio a la instantánea. Cada endpoint de audio aparece en el Issue Summary con los siguientes detalles:

| Campo                  | Significado                                                                 |
|------------------------|-------------------------------------------------------------------------|
| `name`                 | El nombre del endpoint.                                                      |
| `direction`            | Dirección (`INPUT` o `OUTPUT`).                                        |
| `kind`                 | Tipo de endpoint (por ejemplo, "endpoint").                                     |
| `operational`          | Si el endpoint es operativo (`Yes` / `No`).                     |
| `running`              | Si el endpoint está en ejecución (`Yes` / `No`).                     |
| `state`                | Cadena de estado actual.                                                   |
| `error`                | Cadena de error, o "n/a" si no hay ninguno.                                         |
| `backend`              | Nombre del backend de audio.                                                     |
| `device`               | Nombre del dispositivo, o "Unavailable".                                          |
| `sample_rate_hz`       | Frecuencia de muestreo en Hz.                                                      |
| `channel_count`        | Número de canales.                                                     |
| `sample_format`        | Cadena de formato de muestra.                                                   |
| `resampling_active`    | Si el remuestreo está activo.                                           |
| `voice_input_normalizing_to_48k` | Si la normalización de entrada de voz a 48 kHz está activa (nuevo en v26.8.4). |
| `voice_egress_resampling_to_24k` | Si el remuestreo de salida de voz a 24 kHz está activo (nuevo en v26.8.4). |
| `rade_resampling_to_24k` | Si el remuestreo RADE a 24 kHz está activo (nuevo en v26.8.4).        |
| `buffer_bytes`         | Tamaño actual del búfer en bytes (si está disponible).                            |
| `buffer_peak_bytes`    | Tamaño máximo del búfer en bytes (si está disponible).                               |
| `underrun_count`       | Número de underruns (si está disponible).                                     |
| `note`                 | Nota adicional en lenguaje natural sobre el endpoint.                      |

En v26.8.4, la línea de detalles del endpoint incluye tres flags adicionales cuando el sistema de audio subyacente los informa: `voice input normalization to 48 kHz`, `voice egress resampling to 24 kHz` y `RADE resampling to 24 kHz`. Estos indican si el sistema de audio está remuestreando activamente para esos fines.

## Campos de RX de audio remoto en la instantánea

v0.9.4 agrega el estado de RX de audio remoto tanto en las secciones a nivel de radio como por slice del Issue Summary y la instantánea JSON. Estos campos ayudan a diagnosticar problemas donde AetherSDR ha solicitado una transmisión de audio remoto desde la radio pero el audio no fluye.

### RX de audio remoto a nivel de radio

En el Issue Summary, busque la línea que comienza con **Remote audio RX:**. Informa lo siguiente:

| Campo              | Significado                                                                 |
|--------------------|-------------------------------------------------------------------------|
| `stream_id`        | El identificador de transmisión asignado por la radio, o `—` si no hay ninguno.           |
| `stream_expected`  | Si AetherSDR espera que esta transmisión exista (`Yes` / `No`).         |
| `create_pending`   | Si una solicitud de creación sigue pendiente (`Yes` / `No`).          |
| `status_seen`      | Si se ha recibido una actualización de estado para esta transmisión (`Yes` / `No`). |
| `owned_by_us`      | Si este cliente posee la transmisión (`Yes` / `No`).                    |
| `compression`      | El tipo de compresión en uso, o `—` si no se informa.                   |

Una segunda línea, **Remote audio route note:**, contiene una nota en lenguaje natural sobre el estado de ruteo, o `—` si no se generó ninguna.

### Ruta de transmisión de radio por slice

En el Issue Summary, busque la línea que comienza con **Radio stream route: remote_audio_rx**. Informa lo siguiente:

| Campo                           | Significado                                                                   |
|---------------------------------|---------------------------------------------------------------------------|
| `remote_audio_rx_stream_id`     | El identificador de transmisión para el RX de audio remoto de este slice, o `—` si no hay ninguno.  |
| `remote_audio_rx_expected`      | Si se espera que la transmisión exista.                                  |
| `remote_audio_rx_create_pending`| Si una solicitud de creación sigue pendiente.                            |
| `remote_audio_rx_remove_requested` | Si se ha enviado una solicitud de eliminación pero aún no se ha confirmado.          |
| `remote_audio_rx_status_seen`   | Si se ha recibido una actualización de estado para esta transmisión.                |
| `remote_audio_rx_owned_by_us`   | Si este cliente posee la transmisión.                                      |

Si `remote_audio_rx_expected` es true pero `remote_audio_rx_status_seen` es false, la radio aún no ha confirmado la transmisión. Si `create_pending` es true durante un período prolongado, la solicitud de creación puede no haber llegado a la radio.

## Estado de conexión de slices del panadapter en la instantánea

v26.6.1 agrega información de estado de conexión de slices a la sección de panadapter del Issue Summary. Cuando un panadapter tiene detalles de conexión de slices disponibles, la línea de resumen para ese panadapter incluye un bloque `slice_connection_status` con los siguientes campos:

| Campo                  | Significado                                                                 |
|------------------------|-------------------------------------------------------------------------|
| `state`                | El estado de conexión (por ejemplo, "connected", "disconnected", "unknown").    |
| `summary`              | Una descripción en lenguaje natural del estado del enlace de slices.                   |
| `connected_slice_ids`  | Lista separada por comas de IDs de slices actualmente conectados a este panadapter, o "none". |
| `active_slice_ids`     | Lista separada por comas de IDs de slices activos, o "none".                    |
| `attention_required`   | Si el estado de conexión requiere atención (`(attention)` añadido). |

## Campos de DSP de cliente en la instantánea en la pestaña JSON

v26.7.4 agrega campos adicionales de configuración NR2 (Noise Reduction 2) a la instantánea JSON. La sección de DSP de cliente del JSON ahora incluye:

| Campo                              | Significado                                                                                     |
|------------------------------------|---------------------------------------------------------------------------------------------|
| `nr2.gain_method`                  | El nombre actual del método de ganancia NR2.                                                           |
| `nr2.gain_method_id`               | El identificador numérico del método de ganancia.                                                  |
| `nr2.npe_method`                   | El nombre actual del método de estimación de potencia de ruido NR2.                                         |
| `nr2.npe_method_id`                | El identificador numérico del método NPE.                                                   |
| `nr2.ae_filter`                    | Si el filtro de eco adaptativo está habilitado (`true` / `false`).                             |
| `nr2.gain_max`                     | El valor máximo de ganancia.                                                                     |
| `nr2.gain_floor`                   | El valor mínimo de piso de ganancia (nuevo en v26.7.4).                                             |
| `nr2.gain_smooth`                  | El factor de suavizado de ganancia.                                                                  |
| `nr2.qspp`                         | El valor de percentil de potencia casi estacionaria.                                                |

Nota: El campo `legacy_geometry_and_gain_mapping`, que aparecía en instantáneas de v26.7.4, se ha eliminado en v26.8.4 porque la opción de geometría heredada fue retirada y ya no tiene un control visible para el usuario.

## Consejos

- Si `has_is_valid` es `No` para un transverter, la radio no informó ningún flag de validez para esa entrada. Esto es distinto de que `is_valid` sea `No`, lo que significa que la radio informó la entrada como explícitamente inválida.
- Haga clic en `Refresh Snapshot` después de ajustar la configuración de transverters en SmartSDR o en la radio antes de volver a leer los valores. La instantánea no se actualiza automáticamente.
- El campo `offset_mhz` debe ser igual a `rf_freq_mhz` menos `if_freq_mhz`. Si no coincide con su configuración de transverter, esa discrepancia es una causa probable de errores de frecuencia en el slice.
- Al investigar audio faltante, revise primero los campos de RX de audio remoto. Si `owned_by_us` es `No` y `stream_expected` es `Yes`, otro cliente puede haber tomado posesión de la transmisión.
- Al investigar problemas de conexión del panadapter, revise el campo `slice_connection_status`. Si `attention_required` es true, se necesita investigación adicional.
- Los underruns de endpoints de audio indicados por un `underrun_count` distinto de cero pueden apuntar a problemas de rendimiento o configuración de búfer.
- Cuando la advertencia de medidores TX aparece en el Issue Summary, no confíe en la potencia directa mostrada para decisiones de sintonización o adaptación — es el último valor recibido, no una lectura en vivo.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Lea una lista en lenguaje natural de problemas sospechosos de slices](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualice la instantánea después de cambiar el estado de los slices](refresh-the-snapshot-after-changing-slice-state.md)
- [Exporte la instantánea a un archivo para adjuntarla a un informe de errores](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
