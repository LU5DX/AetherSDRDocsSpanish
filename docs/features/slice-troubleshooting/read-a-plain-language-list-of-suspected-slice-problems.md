# Lea una lista en lenguaje sencillo de posibles problemas del slice

El cuadro de diálogo de solución de problemas del slice analiza el slice actual, el panadaptador, el transvertidor, el canal DAX, el dispositivo de audio, el estado del DSP del cliente y el estado de enlace del dispositivo de control (MIDI) y presenta un resumen en lenguaje sencillo de los problemas detectados. Utilícelo cuando sospeche de un problema de configuración — como la falta de audio, un silencio bloqueado, una antena faltante, un transvertidor no válido o una transmisión de audio remota rota — y desee un diagnóstico rápido sin leer datos sin procesar.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. El cuadro de diálogo requiere una conexión activa con la radio.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña **Issue Summary** si no está ya seleccionada.
3. Lea la lista con viñetas de los problemas detectados.
4. Si ha cambiado recientemente la configuración del slice y desea que la lista refleje el estado actual, haga clic en **Refresh Snapshot**.

## Qué hace cada control

| Control              | Tipo    | Comportamiento                                                                                                                                                                                                                            |
|----------------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Issue Summary**    | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI) y problemas de propiedad de múltiples clientes.                          |
| **JSON**             | Pestaña | Muestra la instantánea JSON completa (versión 3 del esquema) de slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control y configuración de banda TX.                                                         |
| **Refresh Snapshot** | Botón   | Vuelve a leer el estado del slice en la instantánea. Haga clic aquí después de cambiar la configuración del slice.                                                                                                                       |
| **Copy Summary**     | Botón   | Copia el texto del resumen de problemas al portapapeles.                                                                                                                                                                                  |
| **Copy JSON**        | Botón   | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                                                       |
| **Export JSON...**   | Botón   | Guarda la instantánea JSON completa en un archivo.                                                                                                                                                                                        |
| **Close**            | Botón   | Cierra el cuadro de diálogo.                                                                                                                                                                                                              |

La etiqueta de estado debajo de los botones confirma el resultado de la última acción de copia o exportación (por ejemplo, `Copied to clipboard`).

## Qué informa el resumen de problemas

La lista con viñetas del resumen de problemas cubre las siguientes áreas:

- **Salidas de audio** — ganancia y silencio de los auriculares, silencio del altavoz frontal.
- **Recepción de audio remota (RX)** — ID de la transmisión, si se espera la transmisión, si la creación está pendiente, si se ha visto un paquete de estado, si este cliente posee la transmisión y la configuración de compresión. Una línea separada de nota de enrutamiento explica cualquier condición de enrutamiento inusual detectada para la transmisión de audio RX remota.
- **Oscilador** — configuración actual, estado de bloqueo, referencia externa y presencia de TCXO.
- **Ruta de la transmisión de radio** — el ID de la transmisión de audio RX remota utilizado por la ruta RX actual, junto con los indicadores de esperado, creación pendiente, eliminación solicitada, estado visto y propiedad nuestra para esa transmisión.
- **Ruta de entrada TX** — selección de entrada, subselecciones de micrófono y DAX, ganancia del micrófono del PC, ID de la transmisión TX, modo TX DAX y ruta de radio DAX.

## Consejos

- Haga clic en **Refresh Snapshot** después de realizar cualquier cambio en el slice, la antena, el DAX o el enrutamiento de audio antes de compartir o volver a leer el resumen. La instantánea no se actualiza automáticamente.
- Si una transmisión de audio RX remota aparece como pendiente o no es propiedad de este cliente, haga clic en **Refresh Snapshot** después de unos segundos para verificar si la transmisión se ha establecido.
- Si necesita enviar los detalles al soporte técnico, use **Copy Summary** para pegar la lista en lenguaje sencillo en un correo electrónico o en una publicación de foro, o use **Export JSON...** para adjuntar la instantánea completa como archivo.

## Relacionado

- [Slice Troubleshooting overview](overview.md)
- [Refresh the snapshot after changing slice state](refresh-the-snapshot-after-changing-slice-state.md)
- [Capture a slice snapshot for support](capture-a-slice-snapshot-for-support.md)
- [Export the snapshot to a file to attach to a bug report](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspect each transverter's RF/IF, offset and validity flags for XVTR diagnosis](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
