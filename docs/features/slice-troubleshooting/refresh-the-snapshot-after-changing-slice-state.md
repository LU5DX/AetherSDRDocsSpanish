# Solución de problemas de slices

El cuadro de diálogo Solución de problemas de slices captura una instantánea JSON de cada slice, panadapter, transverter y canal DAX, y resume los problemas probables (audio faltante, silencio atascado, antena faltante, validez de XVTR) para que pueda compartirla con el soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El cuadro de diálogo Solución de problemas de slices requiere una conexión de radio activa.
- Abra el cuadro de diálogo mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Realice el cambio de estado del slice que desea capturar (por ejemplo, desilenciar un slice, reasignar una antena o ajustar un canal DAX).
2. En el cuadro de diálogo Solución de problemas de slices, haga clic en **Refresh Snapshot**.
3. El cuadro de diálogo vuelve a leer todo el estado de slices, panadapters, transverters, canales DAX, dispositivos de audio, DSP del cliente, enlaces de dispositivos de control (MIDI), puntos finales de audio, renderizadores, RX de audio remoto y estado de conexión de slices de panadapter.
4. Revise los resultados actualizados en la pestaña **Issue Summary** o en la pestaña **JSON**.

## Qué hace cada control

| Control                 | Tipo                                                                                           | Comportamiento                                                                                                                                                                                                                                                                         |
|-------------------------|------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Refresh Snapshot**    | Botón                                                                                          | Vuelve a leer el estado del slice en la instantánea. Úselo después de cualquier cambio en la configuración del slice.                                                                                                                                                                 |
| **Issue Summary** (pestaña) | Pestaña                                                                                     | Muestra una lista de viñetas en lenguaje sencillo de los problemas detectados según la instantánea actual, incluidos el enrutamiento de audio, DSP, estado del dispositivo de control (MIDI), propiedad multicliente, enrutamiento de RX de audio remoto, estado del punto final de audio, estado del renderizador y estado de conexión del slice de panadapter. |
| **JSON** (pestaña)      | Pestaña                                                                                         | Muestra la instantánea JSON completa (versión 3 del esquema) de slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, puntos finales de audio, renderizadores, configuración de banda TX, estado de RX de audio remoto y estado de conexión del slice de panadapter. |
| **Copy Summary**        | Botón                                                                                         | Copia el resumen de problemas al portapapeles.                                                                                                                                                                                                                                        |
| **Copy JSON**           | Botón                                                                                         | Copia el JSON completo al portapapeles.                                                                                                                                                                                                                                                |
| **Export JSON...**      | Botón                                                                                         | Guarda el JSON en un archivo.                                                                                                                                                                                                                                                            |
| **Find:**               | Campo de texto                                                                                | Resalta las coincidencias del término ingresado en la pestaña activa (Issue Summary o JSON). Tiene botón de borrado y texto de marcador 'Search snapshot...'. Enter salta a la siguiente coincidencia; el uso compartido de pestañas actualiza los recuentos de resaltado. La etiqueta de estado muestra '<N> match(es) in current tab.' |
| **Find Next**           | Botón                                                                                         | Salta a la siguiente coincidencia del término de búsqueda en la pestaña activa. Se ajusta dentro de la pestaña actual. Un término vacío no produce coincidencias.                                                                                                                       |
| **Close**               | Botón                                                                                         | Cierra el cuadro de diálogo.                                                                                                                                                                                                                                                            |

## Qué informa el Issue Summary

La pestaña **Issue Summary** incluye las siguientes categorías de información. Cada elemento aparece como viñeta en lenguaje sencillo en el resumen.

### Estado de audio y hardware a nivel de radio

- Ganancia de auriculares, silencio de auriculares y estado de silencio del altavoz frontal.
- Configuración del oscilador, estado de bloqueo, referencia externa y estado de TCXO.

### Estado del medidor de transmisor

El resumen informa el estado del medidor de TX, incluido si los medidores de TX están activos. Si los medidores de TX NO están activos, se muestra una viñeta de advertencia:

- **TX meters are NOT live** – Indica que la potencia directa de TX es el último valor recibido, no una lectura actual, y la ROE de TX se omite en lugar de mostrarse obsoleta. La viñeta incluye el tiempo desde la última muestra (por ejemplo, "last sample 250 ms ago") o señala que no se ha recibido ninguna muestra del medidor de TX en esta sesión. Esto evita que quien lea el paquete de soporte confunda una lectura de vatios obsoleta junto a una ROE faltante con un problema de antena.

### Estado de RX de audio remoto

El resumen incluye dos viñetas para RX de audio remoto:

- **Remote audio RX:** Informa el ID de flujo, si se espera un flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si este cliente posee el flujo y la configuración de compresión en uso.
- **Remote audio route note:** Una nota en lenguaje sencillo sobre el estado del enrutamiento de RX de audio remoto, si está disponible.

### Enrutamiento de audio por slice

Para cada slice, el resumen informa:

- Volumen de RX del motor, estado de silencio y si el audio de RX se está transmitiendo.
- **Radio stream route:** Informa el ID de flujo de RX de audio remoto, si se espera el flujo, si la creación o eliminación está pendiente, si se ha visto un mensaje de estado y si este cliente posee el flujo.
- Ruta de entrada de TX, selección de micrófono, modo DAX TX y configuraciones relacionadas.

### Estado del punto final de audio

Para cada punto final de audio, el resumen informa:

- Nombre, dirección (INPUT o OUTPUT) y tipo (tipo de punto final).
- Backend, nombre del dispositivo, frecuencia de muestra, cantidad de canales, formato de muestra y si el remuestreo está activo.
- Para puntos finales de entrada de voz, se informan detalles adicionales de remuestreo:
  - Normalización de entrada de voz a 48 kHz.
  - Remuestreo de salida de voz a 24 kHz.
  - Remuestreo RADE a 24 kHz.
- Estado operativo y de ejecución, estado del flujo e información de errores.
- Estadísticas de búfer (bytes de búfer, bytes máximos y recuento de subejecución) si están disponibles.
- Cualquier nota adicional sobre el punto final.

### Estado del renderizador

Para cada renderizador en el motor de audio, el resumen informa el nombre del renderizador, un identificador de backend, la frecuencia de muestra y si el audio está actualmente activo.

### Estado de conexión del slice de panadapter

Para cada panadapter, el resumen informa:

- El estado de conexión del slice, un resumen legible del estado del enlace, la lista de IDs de slice conectados, la lista de IDs de slice activos y si la conexión requiere atención.

### Enlaces de dispositivos de control (MIDI)

El resumen informa cada dispositivo de control y los enlaces MIDI asociados a él, incluidos el alcance, los detalles de asignación y las condiciones de error.

## Detalles de la instantánea JSON

La instantánea JSON incluye los siguientes parámetros de DSP del cliente para NR2 (reducción de ruido 2):

- `nr2_enabled` – Si NR2 está habilitado.
- `gain_method` – El nombre del método de reducción de ganancia.
- `gain_method_id` – El ID del método de reducción de ganancia.
- `npe_method` – El nombre del método de estimación de potencia de ruido.
- `npe_method_id` – El ID del método de estimación de potencia de ruido.
- `ae_filter` – Si el filtro de eco adaptativo está habilitado.
- `gain_max` – Valor máximo de reducción de ganancia.
- `gain_floor` – Valor mínimo de ganancia.
- `gain_smooth` – Factor de suavizado de ganancia.
- `qspp` – Valor del procesador de potencia cuasiestacionaria.

El parámetro retirado `legacy_geometry_and_gain_mapping` y su clave de configuración asociada (`NR2UseOriginalGeometry`) ya no forman parte de la instantánea.

## Indicador de estado

Después de hacer clic en **Copy Summary**, **Copy JSON** o **Export JSON...**, una etiqueta de estado debajo de los botones muestra el resultado de la operación (por ejemplo, *Copied to clipboard*). La etiqueta de estado también muestra el recuento de coincidencias de búsqueda cuando usa **Find:** o **Find Next**.

## Consejos

- Después de hacer clic en **Refresh Snapshot**, revise tanto la pestaña **Issue Summary** como la pestaña **JSON** para confirmar que el cambio que realizó se refleja antes de compartir la instantánea con el soporte técnico.
- Si planea exportar o copiar la instantánea para un informe de errores, haga clic siempre en **Refresh Snapshot** primero para asegurarse de que los datos estén actualizados.
- La nota de enrutamiento de RX de audio remoto en el Issue Summary es un primer indicador útil de problemas de propiedad o creación de flujos al solucionar audio que no llega al cliente.
- El estado de conexión del slice de panadapter y los detalles del punto final de audio pueden ayudar a identificar problemas de conectividad o estado de flujo que pueden no aparecer en otros lugares.
- Si los medidores de TX se informan como NO activos, la potencia directa de TX mostrada es el último valor suavizado recibido, no una lectura en vivo. Trátela en consecuencia al diagnosticar problemas de antena o amplificador.
- Use **Find:** para localizar rápidamente un ID de slice, canal DAX o cadena de error en cualquiera de las pestañas sin exportar la instantánea.

## Relacionado

- [Slice Troubleshooting overview](overview.md)
- [Capture a slice snapshot for support](capture-a-slice-snapshot-for-support.md)
- [Read a plain-language list of suspected slice problems](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copy the full JSON snapshot to the clipboard](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Export the snapshot to a file to attach to a bug report](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
