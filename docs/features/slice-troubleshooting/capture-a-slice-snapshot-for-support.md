# Capturar una instantánea de slice para soporte técnico

El diálogo Slice Troubleshooting captura una instantánea en un momento determinado de cada slice (receptor de banda), panadapter, transverter, canal DAX, dispositivo de audio, estado DSP del cliente y asignaciones de dispositivos de control (MIDI) en la radio conectada. Úselo para recopilar información antes de presentar un informe de error o solicitar soporte técnico, o para compartirla con herramientas de diagnóstico asistidas por IA.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo no está disponible sin una conexión de radio activa.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`. El diálogo Slice Troubleshooting se abre y captura una instantánea de inmediato.
2. Revise los problemas detectados en la pestaña **Issue Summary**. Cada entrada es un punto en lenguaje sencillo que describe un problema sospechado, como audio faltante, silenciamiento bloqueado, antena ausente, configuración de transverter no válida, problemas de enrutamiento de audio, problemas de estado DSP, estado de dispositivo de control (MIDI) o conflictos de propiedad en entornos multicliente.
3. Revise los datos sin procesar en la pestaña **JSON** si necesita el detalle completo o tiene intención de adjuntarlo a un informe. La instantánea utiliza la versión de esquema 3 e incluye slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, configuraciones de banda TX y estado del flujo de audio RX remoto.
4. Si cambió el estado del slice después de abrir el diálogo, haga clic en **Refresh Snapshot** para releer el estado actual del slice.
5. Para compartir el texto del resumen, haga clic en **Copy Summary**. El texto se copia al portapapeles.
6. Para compartir el JSON completo, haga clic en **Copy JSON**. La instantánea JSON completa se copia al portapapeles.
7. Para guardar el JSON en un archivo, haga clic en **Export JSON...** y elija una ubicación en el diálogo de guardado que se abre.
8. Observe la etiqueta de estado en la parte inferior del diálogo. Confirma el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard").
9. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Control              | Tipo       | Comportamiento                                                                                                                                                                                                          |
|----------------------|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Issue Summary**    | Pestaña    | Muestra una lista de puntos en lenguaje sencillo con los problemas detectados, incluyendo enrutamiento de audio, estado DSP, estado de dispositivo de control (MIDI) y problemas de propiedad en entornos multicliente. |
| **JSON**             | Pestaña    | Muestra la instantánea JSON completa (versión de esquema 3) de slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, configuraciones de banda TX y estado del flujo de audio RX remoto. |
| **Refresh Snapshot** | Botón      | Relee el estado actual del slice desde la radio y actualiza ambas pestañas.                                                                                                                                             |
| **Copy Summary**     | Botón      | Copia el texto del resumen de problemas al portapapeles.                                                                                                                                                                |
| **Copy JSON**        | Botón      | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                                     |
| **Export JSON...**   | Botón      | Abre un diálogo de guardado para escribir la instantánea JSON en un archivo.                                                                                                                                            |
| **Close**            | Botón      | Cierra el diálogo.                                                                                                                                                                                                      |
| Etiqueta de estado   | Indicador  | Muestra el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard").                                                                                                                   |

## Qué incluye el Issue Summary

La pestaña Issue Summary reporta problemas en varias áreas. A partir de la versión v0.9.4, el resumen también incluye dos secciones de audio RX remoto:

- **Audio RX remoto a nivel de radio** — Reporta el ID del flujo, si el flujo es esperado, si la creación está pendiente, si se ha recibido un mensaje de estado, si el flujo pertenece a este cliente, la configuración de compresión en uso y cualquier nota de enrutamiento que explique por qué el flujo está o no activo.
- **Ruta del flujo de radio por slice** — Reporta el ID del flujo de audio RX remoto para la ruta RX del slice, junto con indicadores sobre si el flujo es esperado, si la creación está pendiente, si se ha solicitado la eliminación, si se ha recibido un mensaje de estado y si el flujo pertenece a este cliente.

## Consejos

- Tome la instantánea antes y después de cambiar la configuración del slice si está intentando aislar un problema. Use **Refresh Snapshot** entre capturas para actualizar los datos.
- Si está reportando un problema de transverter, la pestaña **JSON** incluye la frecuencia RF, la frecuencia IF, el desplazamiento y los indicadores de validez de cada transverter. La pestaña **Issue Summary** marcará cualquier transverter cuya validez no pueda confirmarse.
- Si está reportando un problema de audio remoto, la pestaña **Issue Summary** ahora incluye el estado del flujo de audio RX remoto tanto a nivel de radio como por slice. Copie o exporte la instantánea y compártala con soporte técnico, o péguela en una herramienta de diagnóstico asistida por IA para su análisis.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Leer una lista en lenguaje sencillo de problemas de slice sospechados](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntarla a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Inspeccionar la RF/IF, el desplazamiento y los indicadores de validez de cada transverter para diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
