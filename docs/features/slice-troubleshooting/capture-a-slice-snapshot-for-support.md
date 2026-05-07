# Capturar una instantánea de slice para soporte técnico

El diálogo de Slice Troubleshooting captura una instantánea puntual de todos los slices, panadapters, transverters, canales DAX, dispositivos de audio, estado DSP del cliente y enlaces de dispositivos de control (MIDI) en la radio conectada. Úselo para recopilar información antes de reportar un error o solicitar soporte, o para compartir con herramientas de diagnóstico asistidas por IA.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo no está disponible sin una conexión activa a la radio.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...`. Se abre el diálogo de Slice Troubleshooting y captura una instantánea inmediatamente.
2. Revise los problemas detectados en la pestaña **Issue Summary**. Cada entrada es un viñeta en lenguaje sencillo que describe un problema sospechado, como falta de audio, silencio bloqueado, antena faltante, configuración de transverter inválida, problemas de enrutamiento de audio, problemas de estado DSP, estado del dispositivo de control (MIDI) o conflictos de propiedad de múltiples clientes.
3. Revise los datos sin procesar en la pestaña **JSON** si necesita el detalle completo o planea adjuntarlo a un reporte. La instantánea usa la versión 3 del esquema e incluye slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, configuraciones de banda TX y estado del flujo de audio RX remoto.
4. Si cambió el estado del slice después de abrir el diálogo, haga clic en **Refresh Snapshot** para volver a leer el estado actual del slice.
5. Para compartir el texto del resumen, haga clic en **Copy Summary**. El texto se copia al portapapeles.
6. Para compartir el JSON completo, haga clic en **Copy JSON**. La instantánea JSON completa se copia al portapapeles.
7. Para guardar el JSON en un archivo, haga clic en **Export JSON...** y elija una ubicación de guardado en el diálogo de archivo que se abre.
8. Observe la etiqueta de estado en la parte inferior del diálogo. Confirma el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard").
9. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Control              | Tipo       | Comportamiento                                                                                                                                                                                                   |
|----------------------|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Issue Summary**    | Pestaña    | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI) y problemas de propiedad de múltiples clientes. |
| **JSON**             | Pestaña    | Muestra la instantánea JSON completa (versión 3 del esquema) de slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, configuraciones de banda TX y estado del flujo de audio RX remoto. |
| **Refresh Snapshot** | Botón      | Vuelve a leer el estado actual del slice desde la radio y actualiza ambas pestañas.                                                                                                                              |
| **Copy Summary**     | Botón      | Copia el texto del resumen de problemas al portapapeles.                                                                                                                                                         |
| **Copy JSON**        | Botón      | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                              |
| **Export JSON...**   | Botón      | Abre un diálogo de guardado para escribir la instantánea JSON en un archivo.                                                                                                                                     |
| **Close**            | Botón      | Cierra el diálogo.                                                                                                                                                                                               |
| Etiqueta de estado   | Indicador | Muestra el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard").                                                                                                           |

## Qué incluye el Issue Summary

La pestaña Issue Summary reporta problemas en varias áreas. Desde v0.9.4, el resumen también incluye dos secciones de audio RX remoto:

- **Radio-level remote audio RX** — Reporta el ID del flujo, si se espera el flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si el flujo es propiedad de este cliente, la configuración de compresión en uso y cualquier nota de enrutamiento que explique por qué el flujo está o no activo.
- **Per-slice radio stream route** — Reporta el ID del flujo de audio RX remoto para la ruta RX del slice, junto con indicadores de si se espera el flujo, la creación está pendiente, se ha solicitado la eliminación, se ha visto un mensaje de estado y si el flujo es propiedad de este cliente.

## Consejos

- Tome la instantánea antes y después de cambiar la configuración del slice si está intentando aislar un problema. Use **Refresh Snapshot** entre capturas para actualizar los datos.
- Si está reportando un problema de transverter, la pestaña **JSON** incluye la frecuencia RF de cada transverter, frecuencia FI, desplazamiento y banderas de validez. La pestaña **Issue Summary** marcará cualquier transverter cuya validez no pueda confirmarse.
- Si está reportando un problema de audio remoto, la pestaña **Issue Summary** ahora incluye el estado del flujo de audio RX remoto tanto a nivel de radio como a nivel de slice. Copie o exporte la instantánea y compártala con soporte técnico o péguela en una herramienta de diagnóstico asistida por IA para su análisis.

## Relacionados

- [Slice Troubleshooting overview](overview.md)
- [Read a plain-language list of suspected slice problems](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copy the full JSON snapshot to the clipboard](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Export the snapshot to a file to attach to a bug report](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Refresh the snapshot after changing slice state](refresh-the-snapshot-after-changing-slice-state.md)
- [Inspect each transverter's RF/IF, offset and validity flags for XVTR diagnosis](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
