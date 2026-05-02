# Leer una lista en lenguaje sencillo de problemas detectados en un slice

El diálogo Slice Troubleshooting analiza el slice actual, el panadapter, el transverter, el canal DAX, el dispositivo de audio, el estado DSP del cliente y el estado de asignación del dispositivo de control (MIDI), y presenta un resumen en lenguaje sencillo de los problemas detectados. Utilícelo cuando sospeche un problema de configuración — como ausencia de audio, un silenciamiento bloqueado, una antena faltante, un transverter inválido o una transmisión de audio remoto interrumpida — y desee un diagnóstico rápido sin tener que leer datos brutos.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. El diálogo requiere una conexión de radio activa.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña **Issue Summary** si no está ya seleccionada.
3. Lea la lista de problemas detectados.
4. Si ha cambiado recientemente la configuración del slice y desea que la lista refleje el estado actual, haga clic en **Refresh Snapshot**.

## Qué hace cada control

| Control              | Tipo   | Comportamiento                                                                                                                                                                                                              |
|----------------------|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Issue Summary**    | Pestaña | Muestra una lista en lenguaje sencillo de los problemas detectados, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI) y problemas de propiedad entre múltiples clientes.                      |
| **JSON**             | Pestaña | Muestra el snapshot JSON completo (versión de esquema 3) de slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control y configuración de banda TX.                                               |
| **Refresh Snapshot** | Botón  | Vuelve a leer el estado del slice en el snapshot. Haga clic aquí después de cambiar la configuración del slice.                                                                                                              |
| **Copy Summary**     | Botón  | Copia el texto del resumen de problemas al portapapeles.                                                                                                                                                                    |
| **Copy JSON**        | Botón  | Copia el snapshot JSON completo al portapapeles.                                                                                                                                                                            |
| **Export JSON...**   | Botón  | Guarda el snapshot JSON completo en un archivo.                                                                                                                                                                             |
| **Close**            | Botón  | Cierra el diálogo.                                                                                                                                                                                                          |

La etiqueta de estado debajo de los botones confirma el resultado de la última acción de copia o exportación (por ejemplo, `Copied to clipboard`).

## Qué reporta el Issue Summary

La lista del Issue Summary cubre las siguientes áreas:

- **Salidas de audio** — ganancia y silenciamiento de auriculares, silenciamiento del altavoz frontal.
- **Audio remoto RX** — ID de transmisión, si la transmisión es esperada, si la creación está pendiente, si se ha recibido un paquete de estado, si este cliente es propietario de la transmisión y la configuración de compresión. Una línea de nota de enrutamiento separada explica cualquier condición de enrutamiento inusual detectada para la transmisión de audio remoto RX.
- **Oscilador** — configuración actual, estado de bloqueo, referencia externa y presencia de TCXO.
- **Ruta de transmisión de radio** — el ID de transmisión de audio remoto RX utilizado por la ruta RX actual, junto con los indicadores de esperado, creación pendiente, eliminación solicitada, estado visto y en propiedad de este cliente para esa transmisión.
- **Ruta de entrada TX** — selección de entrada, subselecciones de micrófono y DAX, ganancia del micrófono de PC, ID de transmisión TX, modo DAX TX y ruta de radio DAX.

## Sugerencias

- Haga clic en **Refresh Snapshot** después de realizar cualquier cambio en el slice, la antena, DAX o el enrutamiento de audio antes de compartir o volver a leer el resumen. El snapshot no se actualiza automáticamente.
- Si una transmisión de audio remoto RX aparece como pendiente o no es propiedad de este cliente, haga clic en **Refresh Snapshot** después de unos segundos para verificar si la transmisión se ha establecido.
- Si necesita enviar los detalles al soporte técnico, use **Copy Summary** para pegar la lista en lenguaje sencillo en un correo electrónico o publicación en un foro, o use **Export JSON...** para adjuntar el snapshot completo como archivo.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Actualizar el snapshot después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Capturar un snapshot del slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Exportar el snapshot a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspeccionar los indicadores de RF/IF, desplazamiento y validez de cada transverter para el diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
