# Lea una lista en lenguaje sencillo de los problemas sospechosos del slice

El cuadro de diálogo Slice Troubleshooting analiza su slice, panadapter, transverter, canal DAX, dispositivo de audio, estado DSP del cliente, estado de vinculación del dispositivo de control (MIDI), estado del endpoint de audio y estado del renderizador (pantalla) actuales, y presenta un resumen en lenguaje sencillo de los problemas detectados. Úselo cuando sospeche de un problema de configuración —como audio faltante, silencio atascado, antena faltante, transverter no válido, flujo de audio remoto roto o problemas de renderizado— y quiera un diagnóstico rápido sin leer datos sin procesar.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. El cuadro de diálogo requiere una conexión activa con la radio.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña **Issue Summary** si no está ya seleccionada.
3. Lea la lista con viñetas de los problemas detectados.
4. Si ha cambiado recientemente la configuración del slice y desea que la lista refleje el estado actual, haga clic en **Refresh Snapshot**.

## Qué hace cada control

| Control              | Tipo   | Comportamiento                                                                                                                                                                                        |
|----------------------|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Issue Summary**    | Pestaña    | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI), estado del endpoint de audio, estado del renderizador y problemas de propiedad multi-cliente. |
| **JSON**             | Pestaña    | Muestra la instantánea JSON completa de slices, panadapters, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, endpoints de audio, renderizadores y configuración de banda TX. |
| **Refresh Snapshot** | Botón | Vuelve a leer el estado del slice en la instantánea. Haga clic en él después de cambiar la configuración del slice.                                                                                                               |
| **Copy Summary**     | Botón | Copia el texto del resumen de problemas al portapapeles.                                                                                                                                                 |
| **Copy JSON**        | Botón | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                 |
| **Export JSON...**   | Botón | Guarda la instantánea JSON completa en un archivo.                                                                                                                                                         |
| **Find:**            | Texto   | Resalta las coincidencias del término ingresado en la pestaña activa (Issue Summary o JSON). Tiene botón de borrar y texto de marcador 'Search snapshot...'. Enter salta a la siguiente coincidencia; el uso compartido de pestañas actualiza los contadores de resaltados. La etiqueta de estado muestra '<N> coincidencia(s) en la pestaña actual.' |
| **Find Next**        | Botón | Salta a la siguiente coincidencia del término de búsqueda en la pestaña activa. Se desplaza dentro de la pestaña actual. Un término vacío no produce coincidencias.                                                                       |
| **Close**            | Botón | Cierra el cuadro de diálogo.                                                                                                                                                                              |

La etiqueta de estado debajo de los botones confirma el resultado de la última acción de copia o exportación (por ejemplo, "Copiado al portapapeles") o muestra el número de coincidencias de búsqueda.

## Qué informa el Issue Summary

La lista con viñetas del Issue Summary cubre las siguientes áreas:

- **Salidas de audio** — ganancia y silencio de los auriculares, silencio del altavoz frontal.
- **RX de audio remoto** — ID del flujo, si se espera el flujo, si la creación está pendiente, si se ha visto un paquete de estado, si este cliente es propietario del flujo y el ajuste de compresión. Una línea de nota de enrutamiento separada explica cualquier condición de enrutamiento inusual detectada para el flujo de RX de audio remoto.
- **Oscilador** — ajuste actual, estado de bloqueo, referencia externa y presencia de TCXO.
- **Ruta de flujo de radio** — el ID de flujo de RX de audio remoto utilizado por la ruta de RX actual, junto con las banderas de esperado, creación pendiente, eliminación solicitada, estado visto y propiedad nuestra para ese flujo.
- **Ruta de entrada TX** — selección de entrada, subselecciones de micrófono y DAX, ganancia del micrófono de PC, ID de flujo TX, modo TX DAX y ruta de radio DAX.
- **Medidores TX** — Se emite una línea de advertencia cuando los medidores TX no están en vivo. Cuando la potencia directa TX mantiene su último valor suavizado mientras la ROE TX se lee correctamente como n/a, la advertencia deja claro que la potencia mostrada es el último valor recibido, no una lectura actual, y que la ROE TX se omite en lugar de mostrarse desactualizada. La advertencia incluye la antigüedad de la última muestra (por ejemplo, "última muestra hace 1234 ms") o nota que no se ha recibido ninguna muestra de medidor TX en esta sesión.
- **Panadapters** — para cada panadapter: ID, estado activo, frecuencia central, ancho de banda, ganancia RF, preamplificador, WNB activo/nivel, ID de waterfall y estado de conexión del slice (estado, resumen, IDs de slices conectados, IDs de slices activos, bandera de atención requerida).
- **Endpoints de audio** — para cada endpoint de audio: nombre, dirección, tipo, estado operativo y de ejecución, estado, error, backend, dispositivo, frecuencia de muestreo, número de canales, formato de muestra, estado de remuestreo, estado de normalización de entrada de voz a 48 kHz, estado de remuestreo de salida de voz a 24 kHz, estado de remuestreo RADE a 24 kHz, bytes de búfer, bytes máximos de búfer, contador de subdesbordamiento y cualquier nota.
- **Renderizadores (motor de pantalla)** — para cada renderizador: estado operativo, backend, dispositivo, estado, error, frecuencia de muestreo, información de búfer y métricas de subdesbordamiento.

## Qué incluye la instantánea JSON

La pestaña JSON muestra la instantánea de diagnóstico completa. Además de las áreas enumeradas anteriormente, la instantánea incluye los siguientes parámetros de configuración DSP del cliente:

- **Configuración NR2**: método de ganancia, método NPE, filtro AE, ganancia máxima, ganancia mínima, suavizado de ganancia y QSPP.
- **Configuración NR4**: estado habilitado y método de estimación de ruido.
- **Endpoints de audio**: estado de normalización de entrada de voz a 48 kHz, estado de remuestreo de salida de voz a 24 kHz y estado de remuestreo RADE a 24 kHz para cada endpoint.

## Consejos

- Haga clic en **Refresh Snapshot** después de realizar cualquier cambio en slice, antena, DAX, enrutamiento de audio, panadapter o renderizador antes de compartir o volver a leer el resumen. La instantánea no se actualiza automáticamente.
- Si un flujo de RX de audio remoto aparece como pendiente o no propiedad de este cliente, haga clic en **Refresh Snapshot** después de unos segundos para verificar si el flujo se ha establecido.
- Si necesita enviar los detalles al soporte técnico, use **Copy Summary** para pegar la lista en lenguaje sencillo en un correo electrónico o publicación de foro, o use **Export JSON...** para adjuntar la instantánea completa como archivo.
- Cuando el Issue Summary muestre una advertencia de que los medidores TX no están en vivo, trate la potencia directa TX mostrada como una lectura desactualizada, no como una medición actual, y verifique su antena y configuración TX por separado.

## Relacionado

- [Resumen de Slice Troubleshooting](overview.md)
- [Actualice la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Capture una instantánea del slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Exporte la instantánea a un archivo para adjuntarla a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Inspeccione las banderas RF/IF, compensación y validez de cada transverter para el diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
