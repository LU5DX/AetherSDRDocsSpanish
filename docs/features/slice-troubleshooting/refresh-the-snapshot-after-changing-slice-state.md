# Actualizar la instantánea tras cambiar el estado de un slice

Después de modificar la configuración de un slice —como ajustar el enrutamiento de audio, silenciar o cambiar de antena— el cuadro de diálogo "Slice Troubleshooting" no se actualiza automáticamente. Use **Refresh Snapshot** para volver a leer el estado actual del slice y que el "Issue Summary" y el JSON reflejen sus cambios.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El cuadro de diálogo "Slice Troubleshooting" requiere una conexión activa con la radio.
- Abra el cuadro de diálogo desde `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Realice el cambio de estado del slice que desea capturar (por ejemplo, activar el audio de un slice, reasignar una antena o ajustar un canal DAX).
2. En el cuadro de diálogo "Slice Troubleshooting", haga clic en **Refresh Snapshot**.
3. El cuadro de diálogo vuelve a leer todo el estado de los slices, panadapters, transverters, canales DAX, dispositivos de audio, DSP del cliente, vinculaciones de dispositivos de control (MIDI) y audio RX remoto.
4. Revise los resultados actualizados en la pestaña **Issue Summary** o en la pestaña **JSON**.

## Función de cada control

| Control                  | Tipo   | Comportamiento                                                                                                                               |
|--------------------------|--------|----------------------------------------------------------------------------------------------------------------------------------------------|
| **Refresh Snapshot**     | Botón  | Vuelve a leer el estado del slice en la instantánea. Úselo después de cualquier cambio en la configuración del slice.                       |
| **Issue Summary** (pestaña) | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados según la instantánea actual, incluidos enrutamiento de audio, DSP, estado de dispositivos de control (MIDI), propiedad de múltiples clientes y enrutamiento de audio RX remoto. |
| **JSON** (pestaña)       | Pestaña | Muestra la instantánea JSON completa (esquema versión 3) de slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, configuraciones de banda TX y estado de audio RX remoto. |
| **Copy Summary**         | Botón  | Copia el resumen de problemas al portapapeles.                                                                                               |
| **Copy JSON**            | Botón  | Copia el JSON completo al portapapeles.                                                                                                      |
| **Export JSON...**       | Botón  | Guarda el JSON en un archivo.                                                                                                                |
| **Close**                | Botón  | Cierra el cuadro de diálogo.                                                                                                                 |

## Qué informa el Issue Summary

La pestaña **Issue Summary** incluye las siguientes categorías de información. Cada elemento aparece como una viñeta en lenguaje sencillo en el resumen.

### Estado de audio a nivel de radio y del hardware

- Ganancia de los auriculares, silencio de auriculares y estado del silencio del altavoz frontal.
- Configuración del oscilador, estado de bloqueo, referencia externa y estado del TCXO.

### Estado del audio RX remoto

El resumen incluye dos viñetas para el audio RX remoto:

- **Remote audio RX:** Informa el ID del flujo, si se espera un flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si este cliente posee el flujo y la configuración de compresión en uso.
- **Remote audio route note:** Una nota en lenguaje sencillo sobre el estado del enrutamiento de audio RX remoto, si está disponible.

### Enrutamiento de audio por slice

Para cada slice, el resumen informa:

- Volumen RX del motor, estado de silencio y si el audio RX está en transmisión.
- **Radio stream route:** Informa el ID del flujo de audio RX remoto, si se espera el flujo, si la creación o eliminación están pendientes, si se ha visto un mensaje de estado y si este cliente posee el flujo.
- Ruta de entrada TX, selección de micrófono, modo DAX TX y configuraciones relacionadas.

## Indicador de estado

Después de hacer clic en **Copy Summary**, **Copy JSON** o **Export JSON...**, una etiqueta de estado debajo de los botones muestra el resultado de la operación (por ejemplo, *Copied to clipboard*).

## Consejos

- Después de hacer clic en **Refresh Snapshot**, revise tanto la pestaña **Issue Summary** como la pestaña **JSON** para confirmar que el cambio realizado se refleja antes de compartir la instantánea con soporte técnico.
- Si planea exportar o copiar la instantánea para un informe de error, haga clic siempre primero en **Refresh Snapshot** para asegurarse de que los datos estén actualizados.
- La nota de enrutamiento de audio RX remoto en el "Issue Summary" es un indicador útil inicial de problemas de propiedad o creación de flujos al solucionar problemas de audio que no llegan al cliente.

## Relacionados

- [Slice Troubleshooting overview](overview.md)
- [Capture a slice snapshot for support](capture-a-slice-snapshot-for-support.md)
- [Read a plain-language list of suspected slice problems](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copy the full JSON snapshot to the clipboard](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Export the snapshot to a file to attach to a bug report](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
