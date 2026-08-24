# Capture una instantánea de slice para soporte

El diálogo Slice Troubleshooting captura una instantánea puntual de cada slice, panadapter, transverter, canal DAX, dispositivo de audio, estado DSP del cliente, vinculaciones de dispositivos de control (MIDI) y endpoints del renderizador de audio en la radio conectada. Úselo para recopilar información antes de presentar un informe de error o solicitar soporte, o para compartirla con herramientas de diagnóstico asistidas por IA.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo no está disponible sin una conexión de radio activa.

## Cómo abrir el diálogo

1. Haga clic en `Help > Slice Troubleshooting...`. Se abre el diálogo Slice Troubleshooting e inmediatamente captura una instantánea. El diálogo recuerda su tamaño y posición anteriores.
2. Revise los problemas detectados en la pestaña **Issue Summary**. Cada entrada es una viñeta en lenguaje sencillo que describe un problema sospechoso, como audio faltante, silencio atascado, antena faltante, una configuración de transverter no válida, problemas de enrutamiento de audio, problemas de estado DSP, estado de dispositivos de control (MIDI), conflictos de propiedad multi-cliente, problemas de endpoints del renderizador de audio o estado de conexión del panadapter.
3. Revise los datos sin procesar en la pestaña **JSON** si necesita el detalle completo o tiene la intención de adjuntarlos a un informe. La instantánea usa la versión 3 del esquema e incluye slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, configuraciones de banda TX, estado de flujo RX de audio remoto, endpoints del renderizador de audio y estado de conexión de slice del panadapter.

## Búsqueda en la instantánea

El diálogo incluye una búsqueda Find que funciona en la pestaña actual (Issue Summary o JSON).

1. Escriba un término en el campo **Find:**. El campo tiene un botón de borrar y un texto de marcador de posición "Search snapshot...".
2. La etiqueta de estado muestra el número de coincidencias, por ejemplo, "3 match(es) in current tab."
3. Presione Enter o haga clic en **Find Next** para saltar a la siguiente coincidencia. La búsqueda se envuelve dentro de la pestaña actual.
4. Borre el campo para eliminar el resaltado.

## Copiar y exportar datos

1. Para compartir el texto del resumen, haga clic en **Copy Summary**. El texto se copia al portapapeles.
2. Para compartir el JSON completo, haga clic en **Copy JSON**. La instantánea JSON completa se copia al portapapeles.
3. Para guardar el JSON en un archivo, haga clic en **Export JSON...** y elija una ubicación de guardado en el diálogo de archivo que se abre.
4. Observe la etiqueta de estado en la parte inferior del diálogo. Confirma el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard").
5. Haga clic en **Close** cuando haya terminado.

## Actualizar la instantánea

Si cambió el estado de los slices después de abrir el diálogo, haga clic en **Refresh Snapshot** para volver a leer el estado actual de los slices.

## Qué hace cada control

| Control              | Tipo         | Comportamiento                                                                                                                                                                                                                                        |
|----------------------|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Issue Summary**    | Pestaña      | Muestra una lista de viñetas en lenguaje sencillo de los problemas detectados, incluidos enrutamiento de audio, DSP, estado de dispositivos de control (MIDI), problemas de propiedad multi-cliente, problemas de endpoints del renderizador de audio y estado de conexión de slice del panadapter. |
| **JSON**             | Pestaña      | Muestra la instantánea JSON completa (versión 3 del esquema) de slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, configuraciones de banda TX, estado de flujo RX de audio remoto, endpoints del renderizador de audio y estado de conexión de slice del panadapter. |
| **Refresh Snapshot** | Botón        | Vuelve a leer el estado actual de los slices desde la radio y actualiza ambas pestañas.                                                                                                                                                               |
| **Copy Summary**     | Botón        | Copia el texto del resumen de problemas al portapapeles.                                                                                                                                                                                               |
| **Copy JSON**        | Botón        | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                                                                     |
| **Export JSON...**   | Botón        | Abre un diálogo de guardado para escribir la instantánea JSON en un archivo.                                                                                                                                                                           |
| **Close**            | Botón        | Cierra el diálogo.                                                                                                                                                                                                                                     |
| Etiqueta de estado   | Indicador    | Muestra el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard") o el recuento de coincidencias de búsqueda.                                                                                                       |
| **Find:**            | Campo de texto| Resalta las ocurrencias coincidentes del término ingresado en la pestaña activa (Issue Summary o JSON). Tiene botón de borrar y texto de marcador de posición "Search snapshot...". Enter salta a la siguiente coincidencia; el intercambio de pestañas actualiza los recuentos de resaltado. |
| **Find Next**        | Botón        | Salta a la siguiente coincidencia del término de búsqueda en la pestaña activa. Se envuelve dentro de la pestaña actual. Un término vacío no produce coincidencias.                                                                                       |

## Qué incluye el Issue Summary

La pestaña Issue Summary informa problemas en varias áreas:

- **RX de audio remoto a nivel de radio** — Informa el ID del flujo, si se espera el flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si el flujo es propiedad de este cliente, el ajuste de compresión en uso y cualquier nota de enrutamiento que explique por qué el flujo está o no activo.
- **Ruta de flujo de radio por slice** — Informa el ID del flujo RX de audio remoto para la ruta RX del slice junto con indicadores de si se espera el flujo, si la creación está pendiente, si se ha solicitado la eliminación, si se ha visto un mensaje de estado y si el flujo es propiedad de este cliente.
- **Endpoints del renderizador de audio** — Para cada endpoint de audio, informa la dirección, el tipo, el backend, el nombre del dispositivo, la frecuencia de muestreo, el número de canales, el formato de muestra, el estado de remuestreo, los bytes del buffer, el pico del buffer, el recuento de underruns, cualquier estado operativo o de error, y cualquier nota adicional.
- **Estado de conexión de slice del panadapter** — Para cada panadapter, informa el resumen del estado de conexión, qué IDs de slice están conectados, cuáles están activos y si se requiere atención.
- **Actualización de los medidores TX** — Cuando los datos del medidor TX no están en vivo, el resumen lo indica con una advertencia: la potencia directa TX es el último valor suavizado recibido en lugar de una lectura actual, y la ROE TX se omite en lugar de mostrarse desactualizada. El mensaje muestra la antigüedad de la última muestra cuando está disponible.

## Qué incluye el JSON

La instantánea JSON incluye todos los datos del Issue Summary más el detalle para el diagnóstico. Desde v26.6.1, la instantánea también incluye:

- **Endpoints del renderizador de audio** — La configuración completa de cada endpoint: nombre, dirección, tipo, backend, dispositivo, frecuencia de muestreo, número de canales, formato de muestra, estado de remuestreo, estadísticas del buffer, indicadores operativos y de ejecución, estado, error y notas.
- **Estado de conexión de slice del panadapter** — Para cada panadapter, el objeto `slice_connection_status` que contiene el estado, el resumen, los IDs de slice conectados, los IDs de slice activos y el indicador de atención requerida.
- **Configuración DSP NR2** — Los ajustes completos de reducción de ruido NR2, incluido el campo `gain_floor` junto con los campos existentes `ae_filter`, `gain_method`, `gain_max`, `gain_smooth`, `npe_method` y `qspp`.

Desde v26.8.4, la instantánea también incluye:

- **Detalles de remuestreo de endpoints de audio** — Para los endpoints de audio que incluyen entrada de voz o configuración de remuestreo, campos adicionales informan la normalización de entrada de voz a 48 kHz, el remuestreo de salida de voz a 24 kHz y los indicadores de remuestreo RADE a 24 kHz.
- **Actualización de los medidores TX** — La instantánea incluye los campos `tx_meters_fresh` y `tx_meters_age_ms` para indicar si los datos del medidor TX están actualizados.

## Consejos

- Tome la instantánea antes y después de cambiar la configuración de slices si está tratando de aislar un problema. Use **Refresh Snapshot** entre capturas para actualizar los datos.
- Si está informando un problema de transverter, la pestaña **JSON** incluye la frecuencia RF, la frecuencia FI, el offset y los indicadores de validez de cada transverter. La pestaña **Issue Summary** marcará cualquier transverter cuya validez no pueda confirmarse.
- Si está informando un problema de audio remoto, la pestaña **Issue Summary** ahora incluye el estado del flujo RX de audio remoto tanto a nivel de radio como a nivel de slice. Copie o exporte la instantánea y compártala con soporte o péguela en una herramienta de diagnóstico asistida por IA para su análisis.
- Si sospecha un problema de endpoint de audio, revise las entradas del endpoint del renderizador de audio en el Issue Summary para detectar underruns, estados de error o discrepancias de configuración. La pestaña JSON proporciona el detalle completo de cada endpoint.
- Si se sospecha un problema de medidor TX, el Issue Summary indicará cuándo los medidores TX no están en vivo y explicará que las lecturas de potencia directa TX y ROE pueden estar desactualizadas u omitidas.
- El diálogo recuerda su posición y tamaño entre sesiones. Si necesita restablecerlo, cierre el diálogo y elimine el ajuste `SliceTroubleshootingDialogGeometry` del archivo de configuración.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Lea una lista en lenguaje sencillo de problemas de slice sospechosos](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copie la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exporte la instantánea a un archivo para adjuntarla a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualice la instantánea después de cambiar el estado de los slices](refresh-the-snapshot-after-changing-slice-state.md)
- [Inspeccione el RF/FI, el offset y los indicadores de validez de cada transverter para el diagnóstico de XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
