# Lea una lista en lenguaje sencillo de problemas sospechosos en el slice

El cuadro de diálogo de Solución de problemas del slice analiza su slice, panadapter, transvertidor, canal DAX, dispositivo de audio, estado del DSP del cliente, estado de vinculación del dispositivo de control (MIDI), estado del punto final de audio y estado del renderizador (pantalla) actuales, y presenta un resumen en lenguaje sencillo de los problemas detectados. Úselo cuando sospeche de un problema de configuración — como falta de audio, un silencio atascado, una antena faltante, un transvertidor no válido, un flujo de audio remoto interrumpido o un problema de representación — y desee un diagnóstico rápido sin leer datos sin procesar.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. El cuadro de diálogo requiere una conexión activa con la radio.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña **Issue Summary** si aún no está seleccionada.
3. Lea la lista con viñetas de los problemas detectados.
4. Si ha cambiado recientemente la configuración del slice y desea que la lista refleje el estado actual, haga clic en **Refresh Snapshot**.

## Función de cada control

| Control              | Tipo   | Comportamiento                                                                                                                                                                                                                     |
|----------------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Issue Summary**    | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI), estado del punto final de audio, estado del renderizador y problemas de propiedad entre múltiples clientes. |
| **JSON**             | Pestaña | Muestra la instantánea JSON completa de slices, panadapters, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, puntos finales de audio, renderizadores y configuraciones de banda de TX.                                               |
| **Refresh Snapshot** | Botón   | Vuelve a leer el estado del slice en la instantánea. Haga clic aquí después de cambiar la configuración del slice.                                                                                                              |
| **Copy Summary**     | Botón   | Copia el texto del resumen de problemas al portapapeles.                                                                                                                                                                           |
| **Copy JSON**        | Botón   | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                                               |
| **Export JSON...**   | Botón   | Guarda la instantánea JSON completa en un archivo.                                                                                                                                                                                |
| **Close**            | Botón   | Cierra el cuadro de diálogo.                                                                                                                                                                                                      |

La etiqueta de estado debajo de los botones confirma el resultado de la última acción de copia o exportación (por ejemplo, `Copied to clipboard`).

## Qué informa el Resumen de problemas

La lista con viñetas del Resumen de problemas cubre las siguientes áreas:

- **Salidas de audio** — ganancia y silencio de auriculares, silencio del altavoz frontal.
- **RX de audio remoto** — ID del flujo, si se espera el flujo, si la creación está pendiente, si se ha visto un paquete de estado, si este cliente es propietario del flujo y la configuración de compresión. Una nota de línea de enrutamiento separada explica cualquier condición de enrutamiento inusual detectada para el flujo de RX de audio remoto.
- **Oscilador** — configuración actual, estado de bloqueo, referencia externa y presencia de TCXO.
- **Ruta del flujo de radio** — el ID del flujo de RX de audio remoto utilizado por la ruta de RX actual, junto con las banderas de esperado, creación-pendiente, eliminación-solicitada, estado-visto y propiedad-nuestra para ese flujo.
- **Ruta de entrada de TX** — selección de entrada, subselecciones de micrófono y DAX, ganancia de micrófono de PC, ID del flujo de TX, modo DAX TX y ruta de radio DAX.
- **Panadapters** — para cada panadapter: ID, estado activo, frecuencia central, ancho de banda, ganancia de RF, preamplificador, WNB activo/nivel, ID de waterfall y estado de conexión del slice (estado, resumen, IDs de slice conectados, IDs de slice activos, bandera de atención requerida).
- **Puntos finales de audio** — para cada punto final de audio: nombre, dirección, tipo, estado operativo y en ejecución, estado, error, backend, dispositivo, frecuencia de muestreo, número de canales, formato de muestra, estado de remuestreo, bytes de búfer, pico de bytes de búfer, recuento de subejecución y cualquier nota.
- **Renderizadores (motor de pantalla)** — para cada renderizador: estado operativo, backend, dispositivo, estado, error, frecuencia de muestreo, información del búfer y métricas de subejecución.

## Consejos

- Haga clic en **Refresh Snapshot** después de realizar cualquier cambio en el slice, antena, DAX, enrutamiento de audio, panadapter o renderizador antes de compartir o volver a leer el resumen. La instantánea no se actualiza automáticamente.
- Si un flujo de RX de audio remoto aparece como pendiente o no es propiedad de este cliente, haga clic en **Refresh Snapshot** después de unos segundos para verificar si el flujo se ha establecido.
- Si necesita enviar los detalles al soporte técnico, use **Copy Summary** para pegar la lista en lenguaje sencillo en un correo electrónico o publicación en un foro, o use **Export JSON...** para adjuntar la instantánea completa como archivo.

## Relacionado

- [Resumen de solución de problemas del slice](overview.md)
- [Actualice la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Capture una instantánea del slice para el soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Exporte la instantánea a un archivo para adjuntarla a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspeccione las banderas de RF/IF, compensación y validez de cada transvertidor para el diagnóstico de XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
