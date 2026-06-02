# Capturar una instantánea de un slice para soporte técnico

El diálogo de Solución de problemas de Slices captura una instantánea puntual de cada slice, panadaptador, transverter, canal DAX, dispositivo de audio, estado DSP del cliente, enlaces del dispositivo de control (MIDI) y puntos finales del procesador de audio en la radio conectada. Úselo para recopilar información antes de presentar un informe de error o solicitar soporte, o para compartir con herramientas de resolución de problemas asistidas por IA.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo no está disponible sin una conexión activa a la radio.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`. El diálogo de Solución de problemas de Slices se abre y captura una instantánea inmediatamente.
2. Revise los problemas detectados en la pestaña **Issue Summary**. Cada entrada es un punto en lenguaje sencillo que describe un problema sospechado, como falta de audio, silencio atascado, antena faltante, una configuración de transverter no válida, problemas de enrutamiento de audio, problemas de estado DSP, estado del dispositivo de control (MIDI), conflictos de propiedad de múltiples clientes, problemas del punto final del procesador de audio o estado de conexión del panadaptador.
3. Revise los datos sin procesar en la pestaña **JSON** si necesita el detalle completo o planea adjuntarlo a un informe. La instantánea usa la versión 3 del esquema e incluye slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, configuraciones de banda TX, estado del flujo de recepción de audio remoto, puntos finales del procesador de audio y estado de conexión de slices del panadaptador.
4. Si cambió el estado del slice después de abrir el diálogo, haga clic en **Refresh Snapshot** para volver a leer el estado actual del slice.
5. Para compartir el texto del resumen, haga clic en **Copy Summary**. El texto se copia al portapapeles.
6. Para compartir el JSON completo, haga clic en **Copy JSON**. La instantánea JSON completa se copia al portapapeles.
7. Para guardar el JSON en un archivo, haga clic en **Export JSON...** y elija una ubicación de guardado en el diálogo de archivo que se abre.
8. Observe la etiqueta de estado en la parte inferior del diálogo. Confirma el resultado de la última acción de copia o exportación (por ejemplo, "Copiado al portapapeles").
9. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Control              | Tipo       | Comportamiento                                                                                                                                                                                                   |
|----------------------|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Issue Summary**    | Pestaña    | Muestra una lista en lenguaje sencillo con viñetas de los problemas detectados, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI), problemas de propiedad de múltiples clientes, problemas del punto final del procesador de audio y estado de conexión de slices del panadaptador. |
| **JSON**             | Pestaña    | Muestra la instantánea JSON completa (versión 3 del esquema) de slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, configuraciones de banda TX, estado del flujo de recepción de audio remoto, puntos finales del procesador de audio y estado de conexión de slices del panadaptador. |
| **Refresh Snapshot** | Botón      | Vuelve a leer el estado actual del slice desde la radio y actualiza ambas pestañas.                                                                                                                                         |
| **Copy Summary**     | Botón      | Copia el texto del resumen de problemas al portapapeles.                                                                                                                                                            |
| **Copy JSON**        | Botón      | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                            |
| **Export JSON...**   | Botón      | Abre un diálogo de guardado para escribir la instantánea JSON en un archivo.                                                                                                                                                  |
| **Close**            | Botón      | Cierra el diálogo.                                                                                                                                                                                         |
| Etiqueta de estado   | Indicador  | Muestra el resultado de la última acción de copia o exportación (por ejemplo, "Copiado al portapapeles").                                                                                                                   |

## Qué incluye el Issue Summary

La pestaña Issue Summary informa problemas en varias áreas:

- **Recepción de audio remoto a nivel de radio** — Informa el ID del flujo, si se espera el flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si el flujo es propiedad de este cliente, la configuración de compresión en uso y cualquier nota de enrutamiento que explique por qué el flujo está o no activo.
- **Ruta de flujo de radio por slice** — Informa el ID del flujo de recepción de audio remoto para la ruta RX del slice junto con indicadores de si se espera el flujo, la creación está pendiente, se ha solicitado la eliminación, se ha visto un mensaje de estado y si el flujo es propiedad de este cliente.
- **Puntos finales del procesador de audio** — Para cada punto final de audio, informa la dirección, el tipo, el backend, el nombre del dispositivo, la frecuencia de muestreo, el recuento de canales, el formato de muestra, el estado de remuestreo, los bytes del búfer, el pico del búfer, el recuento de desbordamientos, cualquier estado operativo o de error y cualquier nota adicional.
- **Estado de conexión de slices del panadaptador** — Para cada panadaptador, informa el resumen del estado de conexión, qué IDs de slice están conectados, cuáles están activos y si se requiere atención.

## Qué incluye el JSON

La instantánea JSON incluye todos los datos del Issue Summary más detalles para la resolución de problemas. A partir de la v26.6.1, la instantánea también incluye:

- **Puntos finales del procesador de audio** — La configuración completa de cada punto final: nombre, dirección, tipo, backend, dispositivo, frecuencia de muestreo, recuento de canales, formato de muestra, estado de remuestreo, estadísticas del búfer, indicadores operativos y de ejecución, estado, error y notas.
- **Estado de conexión de slices del panadaptador** — Para cada panadaptador, el objeto `slice_connection_status` que contiene el estado, el resumen, los IDs de slice conectados, los IDs de slice activos y el indicador de atención requerida.

## Consejos

- Tome la instantánea antes y después de cambiar la configuración del slice si está tratando de aislar un problema. Use **Refresh Snapshot** entre capturas para actualizar los datos.
- Si está informando un problema con un transverter, la pestaña **JSON** incluye la frecuencia RF, la frecuencia FI, el desplazamiento y los indicadores de validez de cada transverter. La pestaña **Issue Summary** marcará cualquier transverter cuya validez no se pueda confirmar.
- Si está informando un problema de audio remoto, la pestaña **Issue Summary** ahora incluye el estado del flujo de recepción de audio remoto tanto a nivel de radio como a nivel de slice. Copie o exporte la instantánea y compártala con el soporte o péguela en una herramienta de resolución de problemas asistida por IA para su análisis.
- Si sospecha de un problema en un punto final de audio, verifique las entradas del punto final del procesador de audio en el Issue Summary para detectar desbordamientos, estados de error o discrepancias de configuración. La pestaña JSON proporciona el detalle completo para cada punto final.

## Relacionados

- [Slice Troubleshooting overview](overview.md)
- [Read a plain-language list of suspected slice problems](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copy the full JSON snapshot to the clipboard](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Export the snapshot to a file to attach to a bug report](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Refresh the snapshot after changing slice state](refresh-the-snapshot-after-changing-slice-state.md)
- [Inspect each transverter's RF/IF, offset and validity flags for XVTR diagnosis](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
