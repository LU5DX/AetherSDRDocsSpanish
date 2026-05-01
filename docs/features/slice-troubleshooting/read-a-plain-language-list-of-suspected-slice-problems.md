# Lea una lista en lenguaje natural de posibles problemas de slice

El diálogo Slice Troubleshooting analiza su slice actual, panadapter, transverter, canal DAX, dispositivo de audio, estado DSP del cliente y estado de vinculación del dispositivo de control (MIDI), y presenta un resumen en lenguaje natural de los problemas detectados. Úselo cuando sospeche un problema de configuración —como audio faltante, silenciamiento atascado, antena faltante, transverter inválido o flujo de audio remoto roto— y quiera un diagnóstico rápido sin leer datos sin procesar.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. El diálogo requiere una conexión de radio activa.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña **Issue Summary** si no está ya seleccionada.
3. Lea la lista de viñetas de problemas detectados.
4. Si ha cambiado recientemente la configuración del slice y desea que la lista refleje el estado actual, haga clic en **Refresh Snapshot**.

## Qué hace cada control

| Control              | Tipo   | Comportamiento                                                                                                                                                                                                        |
|----------------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Issue Summary**    | Pestaña | Muestra una lista de viñetas en lenguaje natural de problemas detectados, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI) y problemas de propiedad de múltiples clientes.                 |
| **JSON**             | Pestaña | Muestra la instantánea JSON completa (versión de esquema 3) de slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control y configuración de banda TX.                                        |
| **Refresh Snapshot** | Botón  | Relee el estado del slice en la instantánea. Haga clic después de cambiar la configuración del slice.                                                                                                                  |
| **Copy Summary**     | Botón  | Copia el texto del resumen de problemas al portapapeles.                                                                                                                                                               |
| **Copy JSON**        | Botón  | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                                    |
| **Export JSON...**   | Botón  | Guarda la instantánea JSON completa en un archivo.                                                                                                                                                                     |
| **Close**            | Botón  | Cierra el diálogo.                                                                                                                                                                                                    |

La etiqueta de estado debajo de los botones confirma el resultado de la última acción de copia o exportación (por ejemplo, `Copied to clipboard`).

## Lo que reporta Issue Summary

La lista de viñetas Issue Summary cubre las siguientes áreas:

- **Audio outputs** — ganancia de auriculares y silenciamiento, silenciamiento del altavoz frontal.
- **Remote audio RX** — ID de flujo, si el flujo es esperado, si la creación está pendiente, si se ha visto un paquete de estado, si este cliente posee el flujo y la configuración de compresión. Una línea de nota de enrutamiento separada explica cualquier condición de enrutamiento inusual detectada para el flujo de RX de audio remoto.
- **Oscillator** — configuración actual, estado de bloqueo, referencia externa y presencia de TCXO.
- **Radio stream route** — el ID de flujo de audio remoto RX utilizado por la ruta RX actual, junto con las banderas esperado, create-pending, remove-requested, status-seen y owned-by-us para ese flujo.
- **TX input route** — selección de entrada, sub-selecciones de micrófono y DAX, ganancia de micrófono de PC, ID de flujo TX, modo DAX TX y ruta de radio DAX.

## Consejos

- Haga clic en **Refresh Snapshot** después de realizar cambios en slice, antena, DAX o enrutamiento de audio antes de compartir o releer el resumen. La instantánea no se actualiza automáticamente.
- Si un flujo de audio remoto RX se enumera como pendiente o no es propiedad de este cliente, haga clic en **Refresh Snapshot** después de algunos segundos para verificar si el flujo se ha establecido.
- Si necesita enviar los detalles al soporte, use **Copy Summary** para pegar la lista en lenguaje natural en un correo electrónico o publicación de foro, o use **Export JSON...** para adjuntar la instantánea completa como archivo.

## Relacionado

- [Slice Troubleshooting overview](overview.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspeccionar RF/IF, desplazamiento y banderas de validez de cada transverter para diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
