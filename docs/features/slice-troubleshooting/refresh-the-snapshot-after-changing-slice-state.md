# Solución de problemas de slices

El cuadro de diálogo **Slice Troubleshooting** captura una instantánea JSON de cada slice, panadapter, transverter y canal DAX, y resume los problemas probables (audio faltante, silencio bloqueado, antena faltante, validez de XVTR) para que pueda compartirla con el soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El cuadro de diálogo **Slice Troubleshooting** requiere una conexión activa con la radio.
- Abra el cuadro de diálogo mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Realice el cambio de estado del slice que desea capturar (por ejemplo, reactivar el audio de un slice, reasignar una antena o ajustar un canal DAX).
2. En el cuadro de diálogo **Slice Troubleshooting**, haga clic en **Refresh Snapshot**.
3. El cuadro de diálogo vuelve a leer todo el estado de slices, panadapters, transverters, canales DAX, dispositivos de audio, DSP del cliente, enlaces de dispositivos de control (MIDI), puntos de conexión de audio, renderizadores, audio RX remoto y conexiones de slice con el panadapter.
4. Revise los resultados actualizados en la pestaña **Issue Summary** o en la pestaña **JSON**.

## Función de cada control

| Control                 | Tipo   | Comportamiento                                                                               |
|-------------------------|--------|----------------------------------------------------------------------------------------------|
| **Refresh Snapshot**    | Botón  | Vuelve a leer el estado del slice en la instantánea. Úselo después de cualquier cambio en la configuración del slice. |
| **Issue Summary** (pestaña) | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados según la instantánea actual, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI), propiedad multi-cliente, enrutamiento de audio RX remoto, estado del punto de conexión de audio, estado del renderizador y estado de la conexión del slice con el panadapter. |
| **JSON** (pestaña)      | Pestaña | Muestra la instantánea JSON completa (versión 3 del esquema) de slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, puntos de conexión de audio, renderizadores, configuración de banda TX, estado de audio RX remoto y estado de la conexión del slice con el panadapter. |
| **Copy Summary**        | Botón  | Copia el resumen de problemas al portapapeles.                                              |
| **Copy JSON**           | Botón  | Copia el JSON completo al portapapeles.                                                     |
| **Export JSON...**      | Botón  | Guarda el JSON en un archivo.                                                               |
| **Close**               | Botón  | Cierra el cuadro de diálogo.                                                                |

## Qué informa el Issue Summary

La pestaña **Issue Summary** incluye las siguientes categorías de información. Cada elemento aparece como una viñeta en lenguaje sencillo en el resumen.

### Estado de audio y hardware a nivel de radio

- Ganancia de auriculares, silencio de auriculares y estado de silencio del altavoz frontal.
- Configuración del oscilador, estado de bloqueo, referencia externa y estado del TCXO.

### Estado del audio RX remoto

El resumen incluye dos viñetas para el audio RX remoto:

- **Remote audio RX:** Informa el ID del flujo, si se espera un flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si este cliente posee el flujo y la configuración de compresión en uso.
- **Remote audio route note:** Una nota en lenguaje sencillo sobre el estado de enrutamiento del audio RX remoto, si está disponible.

### Enrutamiento de audio por slice

Para cada slice, el resumen informa:

- Volumen de RX del motor, estado de silencio y si el audio de RX está en transmisión.
- **Radio stream route:** Informa el ID del flujo de audio RX remoto, si se espera el flujo, si la creación o eliminación está pendiente, si se ha visto un mensaje de estado y si este cliente posee el flujo.
- Ruta de entrada TX, selección de micrófono, modo DAX TX y configuraciones relacionadas.

### Estado del punto de conexión de audio

Para cada punto de conexión de audio, el resumen informa:

- Nombre, dirección (INPUT o OUTPUT) y tipo (tipo de punto de conexión).
- Backend, nombre del dispositivo, frecuencia de muestreo, cantidad de canales, formato de muestreo y si el remuestreo está activo.
- Estado operativo y de ejecución, estado del flujo e información de error.
- Estadísticas del búfer (bytes en búfer, bytes pico y cantidad de subdesbordamientos) si están disponibles.
- Cualquier nota adicional sobre el punto de conexión.

### Estado del renderizador

Para cada renderizador en el motor de audio, el resumen informa el nombre del renderizador, un identificador del backend, la frecuencia de muestreo y si el audio está activo actualmente.

### Estado de la conexión del slice con el panadapter

Para cada panadapter, el resumen informa:

- El estado de la conexión del slice, un resumen legible del estado del enlace, la lista de IDs de slices conectados, la lista de IDs de slices activos y si la conexión requiere atención.

### Enlaces del dispositivo de control (MIDI)

El resumen informa cada dispositivo de control y los enlaces MIDI asociados, incluyendo el alcance, los detalles de asignación y las condiciones de error.

## Detalles de la instantánea JSON

La instantánea JSON incluye los siguientes parámetros de DSP del cliente para NR2 (reducción de ruido 2):

- `nr2_enabled` – Indica si NR2 está habilitado.
- `gain_method` – El nombre del método de reducción de ganancia.
- `gain_method_id` – El ID del método de reducción de ganancia.
- `npe_method` – El nombre del método de estimación de potencia de ruido.
- `npe_method_id` – El ID del método de estimación de potencia de ruido.
- `ae_filter` – Indica si el filtro de eco adaptativo está habilitado.
- `gain_max` – Valor máximo de reducción de ganancia.
- `gain_floor` – Valor del piso de ganancia.
- `gain_smooth` – Factor de suavizado de ganancia.
- `qspp` – Valor del procesador de potencia cuasi-estacionaria.
- `legacy_geometry_and_gain_mapping` – Indica si la asignación heredada de geometría y ganancia está habilitada.

## Indicador de estado

Después de hacer clic en **Copy Summary**, **Copy JSON** o **Export JSON...**, una etiqueta de estado debajo de los botones muestra el resultado de la operación (por ejemplo, *Copied to clipboard*).

## Consejos

- Después de hacer clic en **Refresh Snapshot**, revise tanto la pestaña **Issue Summary** como la pestaña **JSON** para confirmar que el cambio realizado se refleje antes de compartir la instantánea con el soporte técnico.
- Si planea exportar o copiar la instantánea para un informe de error, siempre haga clic primero en **Refresh Snapshot** para asegurarse de que los datos estén actualizados.
- La nota de enrutamiento de audio RX remoto en el Issue Summary es un primer indicador útil de problemas de propiedad del flujo o de creación al solucionar problemas de audio que no llegan al cliente.
- El estado de la conexión del slice con el panadapter y los detalles del punto de conexión de audio pueden ayudar a identificar problemas de conectividad o estado del flujo que podrían no aparecer en otro lugar.

## Relacionados

- [Slice Troubleshooting overview](overview.md)
- [Capture a slice snapshot for support](capture-a-slice-snapshot-for-support.md)
- [Read a plain-language list of suspected slice problems](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copy the full JSON snapshot to the clipboard](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Export the snapshot to a file to attach to a bug report](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
