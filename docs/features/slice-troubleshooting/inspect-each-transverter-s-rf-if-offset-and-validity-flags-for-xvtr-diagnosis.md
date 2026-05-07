# Inspeccione la RF/FI, el desplazamiento y los indicadores de validez de cada transvertidor para el diagnóstico de XVTR

El diálogo de Solución de Problemas de Slice captura una instantánea de cada transvertidor configurado en su FLEX-8600 y muestra su frecuencia de RF, frecuencia de FI, desplazamiento de frecuencia e indicadores de validez. Úselo cuando un slice basado en transvertidor se comporte incorrectamente — frecuencia equivocada, recepción ausente o modo inesperado — y necesite confirmar qué reporta realmente la radio para cada entrada XVTR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo requiere una conexión activa con la radio.
- Cualquier transvertidor que desee inspeccionar ya debe estar configurado en el FLEX-8600.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo de Solución de Problemas de Slice.
2. Haga clic en la pestaña `Issue Summary`. Revise la lista con viñetas en busca de advertencias de validez XVTR. El resumen marca las entradas donde `is_valid` es falso o `has_is_valid` es falso.
3. Haga clic en la pestaña `JSON` para ver la instantánea completa. Localice las entradas de transvertidor en el JSON. Cada entrada XVTR reporta los siguientes campos:
   - `name` — la etiqueta asignada al transvertidor
   - `index` y `order` — identificadores de posición
   - `rf_freq_mhz` — la frecuencia de RF (por el aire) en MHz
   - `if_freq_mhz` — la frecuencia de FI (entrada de la radio) en MHz
   - `offset_mhz` — la diferencia aplicada entre FI y RF, en MHz
   - `is_valid` — si la entrada del transvertidor está marcada como válida (`Yes` / `No`)
   - `has_is_valid` — si la radio reportó algún indicador de validez (`Yes` / `No`)
   - `rx_only` — si la entrada es solo de recepción
   - `max_power` — potencia máxima en la entrada XVTR
4. Si realizó cambios en la configuración del transvertidor después de abrir el diálogo, haga clic en `Refresh Snapshot` para volver a leer el estado actual desde la radio antes de sacar conclusiones.
5. Para compartir los hallazgos, haga clic en `Copy Summary` para copiar la lista de problemas en lenguaje sencillo al portapapeles, `Copy JSON` para copiar el JSON completo, o `Export JSON...` para guardar el JSON en un archivo.
6. Haga clic en `Close` cuando haya terminado.

## Qué hace cada control

| Control             | Tipo   | Comportamiento                                                                                        |
|---------------------|--------|-------------------------------------------------------------------------------------------------|
| Pestaña `Issue Summary` | Pestaña | Lista con viñetas en lenguaje sencillo de los problemas detectados, incluyendo enrutamiento de audio, DSP, estado de dispositivos de control (MIDI), propiedad multi-cliente y problemas de validez XVTR. |
| Pestaña `JSON`      | Pestaña | Instantánea JSON completa (versión de esquema 3) que contiene slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, configuración de banda TX y todas las entradas de transvertidor con campos de RF, FI, desplazamiento y validez. |
| `Refresh Snapshot`  | Botón | Vuelve a leer el estado del slice en la instantánea.                                                         |
| `Copy Summary`      | Botón | Copia el resumen de problemas al portapapeles.                                                      |
| `Copy JSON`         | Botón | Copia la instantánea JSON completa al portapapeles.                                                 |
| `Export JSON...`    | Botón | Guarda la instantánea JSON completa en un archivo.                                                                              |
| `Close`             | Botón | Cierra el diálogo.                                                                              |

## Campos de audio RX remoto en la instantánea

v0.9.4 agrega el estado de audio RX remoto tanto en la sección a nivel de radio como por slice del Resumen de Problemas y la instantánea JSON. Estos campos ayudan a diagnosticar problemas donde AetherSDR ha solicitado una transmisión de audio remoto desde la radio pero el audio no fluye.

### Audio RX remoto a nivel de radio

En el Resumen de Problemas, busque la línea que comienza con **Remote audio RX:**. Reporta lo siguiente:

| Campo              | Significado                                                                 |
|--------------------|-------------------------------------------------------------------------|
| `stream_id`        | El identificador de transmisión asignado por la radio, o `—` si no hay ninguno.           |
| `stream_expected`  | Si AetherSDR espera que esta transmisión exista (`Yes` / `No`).         |
| `create_pending`   | Si una solicitud de creación aún está pendiente (`Yes` / `No`).          |
| `status_seen`      | Si se ha recibido una actualización de estado para esta transmisión (`Yes` / `No`). |
| `owned_by_us`      | Si este cliente posee la transmisión (`Yes` / `No`).                    |
| `compression`      | El tipo de compresión en uso, o `—` si no se reporta.                   |

Una segunda línea, **Remote audio route note:**, contiene una nota en lenguaje sencillo sobre el estado del enrutamiento, o `—` si no se generó ninguna.

### Ruta de transmisión de radio por slice

En el Resumen de Problemas, busque la línea que comienza con **Radio stream route: remote_audio_rx**. Reporta lo siguiente:

| Campo                           | Significado                                                                   |
|---------------------------------|---------------------------------------------------------------------------|
| `remote_audio_rx_stream_id`     | El identificador de transmisión para el audio RX remoto de este slice, o `—` si no hay ninguno.  |
| `remote_audio_rx_expected`      | Si se espera que la transmisión exista.                                  |
| `remote_audio_rx_create_pending`| Si una solicitud de creación aún está pendiente.                            |
| `remote_audio_rx_remove_requested` | Si se ha enviado una solicitud de eliminación pero aún no se ha confirmado.          |
| `remote_audio_rx_status_seen`   | Si se ha recibido una actualización de estado para esta transmisión.                |
| `remote_audio_rx_owned_by_us`   | Si este cliente posee la transmisión.                                      |

Si `remote_audio_rx_expected` es verdadero pero `remote_audio_rx_status_seen` es falso, la radio aún no ha confirmado la transmisión. Si `create_pending` es verdadero durante un período prolongado, es posible que la solicitud de creación no haya llegado a la radio.

## Consejos

- Si `has_is_valid` es `No` para un transvertidor, la radio no reportó un indicador de validez para esa entrada en absoluto. Esto es distinto de que `is_valid` sea `No`, lo que significa que la radio reportó la entrada como explícitamente inválida.
- Haga clic en `Refresh Snapshot` después de ajustar la configuración del transvertidor en SmartSDR o en la radio antes de volver a leer los valores. La instantánea no se actualiza automáticamente.
- El campo `offset_mhz` debe ser igual a `rf_freq_mhz` menos `if_freq_mhz`. Si no coincide con la configuración de su transvertidor, esa discrepancia es una causa probable de errores de frecuencia en el slice.
- Al investigar audio faltante, revise primero los campos de audio RX remoto. Si `owned_by_us` es `No` y `stream_expected` es `Yes`, otro cliente puede haber tomado posesión de la transmisión.

## Relacionados

- [Slice Troubleshooting overview](overview.md)
- [Read a plain-language list of suspected slice problems](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Refresh the snapshot after changing slice state](refresh-the-snapshot-after-changing-slice-state.md)
- [Export the snapshot to a file to attach to a bug report](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
