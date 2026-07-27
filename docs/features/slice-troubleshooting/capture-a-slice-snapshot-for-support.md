# Capturar una instantánea de slice para soporte técnico

El cuadro de diálogo de solución de problemas de Slice captura una instantánea puntual de cada slice, panadapter, transverter, canal DAX, dispositivo de audio, estado DSP del cliente, enlaces del dispositivo de control (MIDI) y puntos finales del renderizador de audio en la radio conectada. Úselo para recopilar información antes de presentar un informe de error o solicitar soporte técnico, o para compartir con herramientas de solución de problemas asistidas por inteligencia artificial.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El cuadro de diálogo no está disponible sin una conexión activa a la radio.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`. Se abre el cuadro de diálogo Slice Troubleshooting y captura una instantánea inmediatamente. El cuadro de diálogo recuerda su tamaño y posición anteriores.
2. Revise los problemas detectados en la pestaña **Issue Summary**. Cada entrada es un viñeta en lenguaje sencillo que describe un problema sospechado, como audio faltante, silencio atascado, antena faltante, una configuración de transverter no válida, problemas de enrutamiento de audio, problemas de estado DSP, estado del dispositivo de control (MIDI), conflictos de propiedad de múltiples clientes, problemas con los puntos finales del renderizador de audio o el estado de conexión del panadapter.
3. Revise los datos sin procesar en la pestaña **JSON** si necesita el detalle completo o si tiene la intención de adjuntarlo a un informe. La instantánea usa la versión 3 del esquema e incluye slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, configuraciones de banda TX, estado del flujo RX de audio remoto, puntos finales del renderizador de audio y el estado de conexión del slice del panadapter.
4. Si cambió el estado del slice después de abrir el cuadro de diálogo, haga clic en **Refresh Snapshot** para volver a leer el estado actual del slice.
5. Para compartir el texto del resumen, haga clic en **Copy Summary**. El texto se copia al portapapeles.
6. Para compartir el JSON completo, haga clic en **Copy JSON**. La instantánea JSON completa se copia al portapapeles.
7. Para guardar el JSON en un archivo, haga clic en **Export JSON...** y elija una ubicación de guardado en el cuadro de diálogo de archivo que se abre.
8. Observe la etiqueta de estado en la parte inferior del cuadro de diálogo. Confirma el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard").
9. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Control              | Tipo       | Comportamiento                                                                                                                                                                                                                          |
|----------------------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Issue Summary**    | Pestaña    | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados, que incluye enrutamiento de audio, DSP, estado del dispositivo de control (MIDI), problemas de propiedad de múltiples clientes, problemas con los puntos finales del renderizador de audio y el estado de conexión del slice del panadapter. |
| **JSON**             | Pestaña    | Muestra la instantánea JSON completa (versión 3 del esquema) de slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, configuraciones de banda TX, estado del flujo RX de audio remoto, puntos finales del renderizador de audio y el estado de conexión del slice del panadapter.              |
| **Refresh Snapshot** | Botón      | Vuelve a leer el estado actual del slice desde la radio y actualiza ambas pestañas.                                                                                                                                                     |
| **Copy Summary**     | Botón      | Copia el texto del resumen de problemas al portapapeles.                                                                                                                                                                               |
| **Copy JSON**        | Botón      | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                                                    |
| **Export JSON...**   | Botón      | Abre un cuadro de diálogo para guardar la instantánea JSON en un archivo.                                                                                                                                                               |
| **Close**            | Botón      | Cierra el cuadro de diálogo.                                                                                                                                                                                                            |
| Etiqueta de estado   | Indicador  | Muestra el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard").                                                                                                                                  |

## Qué incluye el Issue Summary

La pestaña Issue Summary informa problemas en varias áreas:

- **Audio RX remoto a nivel de radio** — Informa el ID del flujo, si se espera el flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si el flujo es propiedad de este cliente, la configuración de compresión en uso y cualquier nota de enrutamiento que explique por qué el flujo está o no activo.
- **Ruta del flujo de radio por slice** — Informa el ID del flujo RX de audio remoto para la ruta RX del slice junto con indicadores de si se espera el flujo, la creación está pendiente, se ha solicitado la eliminación, se ha visto un mensaje de estado y si el flujo es propiedad de este cliente.
- **Puntos finales del renderizador de audio** — Para cada punto final de audio, informa la dirección, el tipo, el backend, el nombre del dispositivo, la frecuencia de muestreo, el número de canales, el formato de muestra, el estado de remuestreo, los bytes del búfer, el pico del búfer, el recuento de subejecuciones, cualquier estado operativo o de error y cualquier nota adicional.
- **Estado de conexión del slice del panadapter** — Para cada panadapter, informa el resumen del estado de conexión, qué IDs de slice están conectados, cuáles están activos y si se requiere atención.

## Qué incluye el JSON

La instantánea JSON incluye todos los datos del Issue Summary más detalles para la solución de problemas. A partir de la v26.6.1, la instantánea también incluye:

- **Puntos finales del renderizador de audio** — La configuración completa de cada punto final: nombre, dirección, tipo, backend, dispositivo, frecuencia de muestreo, número de canales, formato de muestra, estado de remuestreo, estadísticas del búfer, indicadores operativos y de ejecución, estado, error y notas.
- **Estado de conexión del slice del panadapter** — Para cada panadapter, el objeto `slice_connection_status` que contiene el estado, el resumen, los IDs de slice conectados, los IDs de slice activos y el indicador de atención requerida.
- **Configuración DSP NR2** — La configuración completa de reducción de ruido NR2, incluidos los nuevos campos `gain_floor` y `legacy_geometry_and_gain_mapping` junto con los campos existentes `ae_filter`, `gain_method`, `gain_max`, `gain_smooth`, `npe_method` y `qspp`.

## Consejos

- Tome la instantánea antes y después de cambiar la configuración del slice si está intentando aislar un problema. Use **Refresh Snapshot** entre capturas para actualizar los datos.
- Si está informando un problema de transverter, la pestaña **JSON** incluye la frecuencia RF, la frecuencia FI, el desplazamiento y los indicadores de validez de cada transverter. La pestaña **Issue Summary** marcará cualquier transverter cuya validez no se pueda confirmar.
- Si está informando un problema de audio remoto, la pestaña **Issue Summary** ahora incluye el estado del flujo RX de audio remoto tanto a nivel de radio como a nivel de slice. Copie o exporte la instantánea y compártala con el soporte técnico o péguela en una herramienta de solución de problemas asistida por IA para su análisis.
- Si sospecha de un problema en el punto final de audio, verifique las entradas del punto final del renderizador de audio en el Issue Summary para detectar subejecuciones, estados de error o discrepancias de configuración. La pestaña JSON proporciona detalles completos para cada punto final.
- El cuadro de diálogo recuerda su posición y tamaño entre sesiones. Si necesita restablecerlo, cierre el cuadro de diálogo y elimine la configuración `SliceTroubleshootingDialogGeometry` del archivo de configuración.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje sencillo de problemas sospechosos de slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Inspeccionar la RF/FI, el desplazamiento y los indicadores de validez de cada transverter para el diagnóstico de XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
