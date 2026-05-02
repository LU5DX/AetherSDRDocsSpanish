# Actualizar la instantánea después de cambiar el estado de un slice

Después de cambiar la configuración de un slice — como ajustar el enrutamiento de audio, activar o desactivar el silencio, o cambiar de antena — el diálogo Slice Troubleshooting no se actualiza automáticamente. Use **Refresh Snapshot** para releer el estado actual del slice y que el Issue Summary y el JSON reflejen los cambios realizados.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Slice Troubleshooting requiere una conexión activa con el radio.
- Abra el diálogo mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Realice el cambio de estado del slice que desea capturar (por ejemplo, quite el silencio a un slice, reasigne una antena o ajuste un canal DAX).
2. En el diálogo Slice Troubleshooting, haga clic en **Refresh Snapshot**.
3. El diálogo relee el estado de todos los slices, panadapters, transvertidores, canales DAX, dispositivos de audio, DSP de cliente, enlaces de dispositivos de control (MIDI) y el estado del audio RX remoto.
4. Revise los resultados actualizados en la pestaña **Issue Summary** o en la pestaña **JSON**.

## Qué hace cada control

| Control                 | Tipo   | Comportamiento                                                                               |
|-------------------------|--------|----------------------------------------------------------------------------------------------|
| **Refresh Snapshot**    | Botón  | Relee el estado del slice en la instantánea. Úselo después de cualquier cambio de configuración de un slice. |
| **Issue Summary** (pestaña) | Pestaña | Muestra una lista de puntos en lenguaje natural con los problemas detectados según la instantánea actual, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI), propiedad en múltiples clientes y enrutamiento del audio RX remoto. |
| **JSON** (pestaña)      | Pestaña | Muestra la instantánea JSON completa (versión de esquema 3) de slices, canales DAX, dispositivos de audio, DSP de cliente, dispositivos de control, configuración de banda TX y estado del audio RX remoto. |
| **Copy Summary**        | Botón  | Copia el resumen de problemas al portapapeles.                                               |
| **Copy JSON**           | Botón  | Copia el JSON completo al portapapeles.                                                      |
| **Export JSON...**      | Botón  | Guarda el JSON en un archivo.                                                                |
| **Close**               | Botón  | Cierra el diálogo.                                                                           |

## Qué informa el Issue Summary

La pestaña **Issue Summary** incluye las siguientes categorías de información. Cada elemento aparece como un punto en lenguaje natural en el resumen.

### Estado de audio y hardware a nivel de radio

- Estado del volumen de auriculares, silencio de auriculares y silencio del altavoz frontal.
- Configuración del oscilador, estado de bloqueo, referencia externa y estado del TCXO.

### Estado del audio RX remoto

El resumen incluye dos puntos sobre el audio RX remoto:

- **Audio RX remoto:** Informa el ID del flujo, si se espera un flujo, si la creación está pendiente, si se ha recibido un mensaje de estado, si este cliente es propietario del flujo y la configuración de compresión en uso.
- **Nota de enrutamiento del audio remoto:** Una nota en lenguaje natural sobre el estado del enrutamiento del audio RX remoto, si está disponible.

### Enrutamiento de audio por slice

Para cada slice, el resumen informa:

- Volumen RX del motor, estado de silencio y si el audio RX está transmitiendo.
- **Ruta del flujo de radio:** Informa el ID del flujo de audio RX remoto, si se espera el flujo, si la creación o eliminación está pendiente, si se ha recibido un mensaje de estado y si este cliente es propietario del flujo.
- Ruta de entrada TX, selección de micrófono, modo DAX TX y configuraciones relacionadas.

## Indicador de estado

Después de hacer clic en **Copy Summary**, **Copy JSON** o **Export JSON...**, una etiqueta de estado debajo de los botones muestra el resultado de la operación (por ejemplo, *Copied to clipboard*).

## Consejos

- Después de hacer clic en **Refresh Snapshot**, revise tanto la pestaña **Issue Summary** como la pestaña **JSON** para confirmar que el cambio realizado se refleja correctamente antes de compartir la instantánea con el soporte técnico.
- Si planea exportar o copiar la instantánea para un informe de error, haga clic en **Refresh Snapshot** primero para asegurarse de que los datos estén actualizados.
- La nota de enrutamiento del audio RX remoto en el Issue Summary es un primer indicador útil de problemas de propiedad del flujo o de creación cuando se diagnostica audio que no llega al cliente.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar una instantánea de slice para el soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje natural de problemas detectados en un slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
