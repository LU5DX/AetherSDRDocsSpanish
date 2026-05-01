# Actualizar la instantánea después de cambiar el estado de la slice

Después de cambiar la configuración de la slice —como ajustar el enrutamiento de audio, alternar silencio o cambiar antenas— el diálogo Slice Troubleshooting no se actualiza automáticamente. Use **Refresh Snapshot** para releer el estado actual de la slice de modo que Issue Summary y JSON reflejen sus cambios.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Slice Troubleshooting requiere una conexión de radio activa.
- Abra el diálogo mediante `Help > Slice Troubleshooting...` si no está ya abierto.

## Pasos

1. Realice el cambio de estado de la slice que desea capturar (por ejemplo, desmuteaer una slice, reasignar una antena o ajustar un canal DAX).
2. En el diálogo Slice Troubleshooting, haga clic en **Refresh Snapshot**.
3. El diálogo relee todo el estado de la slice, panadapter, transverter, canal DAX, dispositivo de audio, DSP del cliente, enlace de dispositivo de control (MIDI) y audio remoto RX.
4. Revise los resultados actualizados en la pestaña **Issue Summary** o la pestaña **JSON**.

## Qué hace cada control

| Control                 | Tipo   | Comportamiento                                                                               |
|-------------------------|--------|----------------------------------------------------------------------------------------------|
| **Refresh Snapshot**    | Botón  | Relee el estado de la slice en la instantánea. Use esto después de cualquier cambio de configuración de slice. |
| **Issue Summary** (pestaña) | Pestaña | Muestra una lista de puntos en lenguaje natural de problemas detectados según la instantánea actual, incluido enrutamiento de audio, DSP, estado de dispositivo de control (MIDI), propiedad multicliente y enrutamiento de audio remoto RX. |
| **JSON** (pestaña)      | Pestaña | Muestra la instantánea JSON completa (versión de esquema 3) de slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, configuración de banda TX y estado de audio remoto RX. |
| **Copy Summary**        | Botón  | Copia el resumen de problemas al portapapeles.                                             |
| **Copy JSON**           | Botón  | Copia el JSON completo al portapapeles.                                                     |
| **Export JSON...**      | Botón  | Guarda el JSON en un archivo.                                                               |
| **Close**               | Botón  | Cierra el diálogo.                                                                          |

## Qué informa Issue Summary

La pestaña **Issue Summary** incluye las siguientes categorías de información. Cada elemento aparece como un punto en lenguaje natural en el resumen.

### Estado de audio y hardware a nivel de radio

- Estado de ganancia de auriculares, silencio de auriculares y silencio de altavoz frontal.
- Configuración del oscilador, estado de bloqueo, referencia externa y estado de TCXO.

### Estado de audio remoto RX

El resumen incluye dos puntos para audio remoto RX:

- **Remote audio RX:** Informa el ID de flujo, si se espera un flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si este cliente posee el flujo y la configuración de compresión en uso.
- **Remote audio route note:** Una nota en lenguaje natural sobre el estado de enrutamiento de audio remoto RX, si una está disponible.

### Enrutamiento de audio por slice

Para cada slice, el resumen informa:

- Volumen RX del motor, estado de silencio y si el audio RX se está transmitiendo.
- **Radio stream route:** Informa el ID de flujo de audio remoto RX, si se espera el flujo, si la creación o eliminación está pendiente, si se ha visto un mensaje de estado y si este cliente posee el flujo.
- Ruta de entrada TX, selección de micrófono, modo DAX TX y configuraciones relacionadas.

## Indicador de estado

Después de hacer clic en **Copy Summary**, **Copy JSON** o **Export JSON...**, una etiqueta de estado debajo de los botones muestra el resultado de la operación (por ejemplo, *Copied to clipboard*).

## Consejos

- Después de hacer clic en **Refresh Snapshot**, compruebe tanto la pestaña **Issue Summary** como la pestaña **JSON** para confirmar que el cambio que realizó se refleja antes de compartir la instantánea con soporte.
- Si planea exportar o copiar la instantánea para un informe de error, siempre haga clic en **Refresh Snapshot** primero para asegurar que los datos son actuales.
- La nota de enrutamiento de audio remoto RX en Issue Summary es un útil primer indicador de problemas de propiedad o creación de flujo al solucionar problemas de audio que no llega al cliente.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje natural de problemas sospechosos de slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntarla a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
