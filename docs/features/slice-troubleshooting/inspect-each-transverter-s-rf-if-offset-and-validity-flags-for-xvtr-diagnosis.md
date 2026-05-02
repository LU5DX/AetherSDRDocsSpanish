# Inspeccionar los valores de RF/IF, desplazamiento e indicadores de validez de cada transverter para diagnóstico de XVTR

El diálogo Slice Troubleshooting captura una instantánea de cada transverter configurado en su FLEX-8600 y muestra su frecuencia de RF, frecuencia de IF, desplazamiento de frecuencia e indicadores de validez. Utilícelo cuando un slice basado en transverter presente problemas — frecuencia incorrecta, ausencia de recepción o modo inesperado — y necesite confirmar lo que el radio reporta realmente para cada entrada XVTR.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión activa con el radio.
- Los transverters que desee inspeccionar deben estar ya configurados en el FLEX-8600.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo Slice Troubleshooting.
2. Haga clic en la pestaña `Issue Summary`. Revise la lista de puntos en busca de advertencias de validez de XVTR. El resumen marca las entradas donde `is_valid` es false o `has_is_valid` es false.
3. Haga clic en la pestaña `JSON` para ver la instantánea completa. Localice las entradas de transverter en el JSON. Cada entrada XVTR reporta los siguientes campos:
   - `name` — la etiqueta asignada al transverter
   - `index` y `order` — identificadores de posición
   - `rf_freq_mhz` — la frecuencia de RF (en el aire) en MHz
   - `if_freq_mhz` — la frecuencia de IF (entrada del radio) en MHz
   - `offset_mhz` — la diferencia aplicada entre IF y RF, en MHz
   - `is_valid` — indica si la entrada del transverter está marcada como válida (`Yes` / `No`)
   - `has_is_valid` — indica si el radio reportó un indicador de validez (`Yes` / `No`)
   - `rx_only` — indica si la entrada es solo de recepción
   - `max_power` — potencia máxima en la entrada XVTR
4. Si realizó cambios en la configuración del transverter después de abrir el diálogo, haga clic en `Refresh Snapshot` para releer el estado actual desde el radio antes de sacar conclusiones.
5. Para compartir los resultados, haga clic en `Copy Summary` para copiar la lista de problemas en lenguaje natural al portapapeles, en `Copy JSON` para copiar el JSON completo, o en `Export JSON...` para guardar el JSON en un archivo.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control             | Tipo   | Comportamiento                                                                                        |
|---------------------|--------|-------------------------------------------------------------------------------------------------------|
| Pestaña `Issue Summary` | Pestaña | Lista de puntos en lenguaje natural con los problemas detectados, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI), propiedad en entornos multicliente y problemas de validez de XVTR. |
| Pestaña `JSON`      | Pestaña | Instantánea JSON completa (versión de esquema 3) que contiene slices, canales DAX, dispositivos de audio, DSP de cliente, dispositivos de control, configuración de banda de TX y todas las entradas de transverter con campos de RF, IF, desplazamiento y validez. |
| `Refresh Snapshot`  | Botón  | Relee el estado del slice en la instantánea.                                                          |
| `Copy Summary`      | Botón  | Copia el resumen de problemas al portapapeles.                                                        |
| `Copy JSON`         | Botón  | Copia la instantánea JSON completa al portapapeles.                                                   |
| `Export JSON...`    | Botón  | Guarda la instantánea JSON completa en un archivo.                                                    |
| `Close`             | Botón  | Cierra el diálogo.                                                                                    |

## Campos de audio RX remoto en la instantánea

La versión v0.9.4 agrega el estado de audio RX remoto tanto a la sección de nivel de radio como a la sección por slice del Issue Summary y de la instantánea JSON. Estos campos ayudan a diagnosticar problemas en los que AetherSDR ha solicitado un flujo de audio remoto al radio pero el audio no está fluyendo.

### Audio RX remoto a nivel de radio

En el Issue Summary, busque la línea que comienza con **Remote audio RX:**. Reporta los siguientes campos:

| Campo              | Significado                                                                  |
|--------------------|------------------------------------------------------------------------------|
| `stream_id`        | El identificador de flujo asignado por el radio, o `—` si no hay ninguno.   |
| `stream_expected`  | Indica si AetherSDR espera que este flujo exista (`Yes` / `No`).            |
| `create_pending`   | Indica si una solicitud de creación sigue pendiente (`Yes` / `No`).         |
| `status_seen`      | Indica si se ha recibido una actualización de estado para este flujo (`Yes` / `No`). |
| `owned_by_us`      | Indica si este cliente es propietario del flujo (`Yes` / `No`).             |
| `compression`      | El tipo de compresión en uso, o `—` si no se ha reportado.                  |

Una segunda línea, **Remote audio route note:**, contiene una nota en lenguaje natural sobre el estado del enrutamiento, o `—` si no se generó ninguna.

### Ruta de flujo de radio por slice

En el Issue Summary, busque la línea que comienza con **Radio stream route: remote_audio_rx**. Reporta los siguientes campos:

| Campo                               | Significado                                                                     |
|-------------------------------------|---------------------------------------------------------------------------------|
| `remote_audio_rx_stream_id`         | El identificador de flujo para el audio RX remoto de este slice, o `—` si no hay ninguno. |
| `remote_audio_rx_expected`          | Indica si se espera que el flujo exista.                                        |
| `remote_audio_rx_create_pending`    | Indica si una solicitud de creación sigue pendiente.                            |
| `remote_audio_rx_remove_requested`  | Indica si se ha enviado una solicitud de eliminación pero aún no se ha confirmado. |
| `remote_audio_rx_status_seen`       | Indica si se ha recibido una actualización de estado para este flujo.           |
| `remote_audio_rx_owned_by_us`       | Indica si este cliente es propietario del flujo.                                |

Si `remote_audio_rx_expected` es true pero `remote_audio_rx_status_seen` es false, el radio aún no ha confirmado el flujo. Si `create_pending` es true durante un período prolongado, es posible que la solicitud de creación no haya llegado al radio.

## Consejos

- Si `has_is_valid` es `No` para un transverter, el radio no reportó ningún indicador de validez para esa entrada. Esto es distinto de que `is_valid` sea `No`, lo cual significa que el radio reportó la entrada como explícitamente inválida.
- Haga clic en `Refresh Snapshot` después de ajustar la configuración del transverter en SmartSDR o en el radio antes de releer los valores. La instantánea no se actualiza de forma automática.
- El campo `offset_mhz` debe ser igual a `rf_freq_mhz` menos `if_freq_mhz`. Si no coincide con su configuración del transverter, esa discrepancia es probablemente la causa de los errores de frecuencia en el slice.
- Al investigar la ausencia de audio, revise primero los campos de audio RX remoto. Si `owned_by_us` es `No` y `stream_expected` es `Yes`, otro cliente puede haber tomado la propiedad del flujo.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje natural de los problemas sospechados en el slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
