# Captura una instantánea de slice para soporte

El diálogo Slice Troubleshooting captura una instantánea en un punto en el tiempo de cada slice, panadapter, transverter, canal DAX, dispositivo de audio, estado DSP del cliente y enlaces de dispositivo de control (MIDI) en la radio conectada. Úsalo para recopilar información antes de presentar un informe de error o solicitar soporte, o para compartir con herramientas de resolución de problemas asistidas por IA.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo no está disponible sin una conexión activa a la radio.

## Pasos

1. Haz clic en `Help > Slice Troubleshooting...`. El diálogo Slice Troubleshooting se abre y captura una instantánea inmediatamente.
2. Revisa los problemas detectados en la pestaña **Issue Summary**. Cada entrada es una descripción en lenguaje natural de un problema sospechado, como audio faltante, silencio atascado, antena faltante, una configuración de transverter inválida, problemas de enrutamiento de audio, problemas de estado DSP, estado de dispositivo de control (MIDI) o conflictos de propiedad multicliente.
3. Revisa los datos sin formato en la pestaña **JSON** si necesitas el detalle completo o tienes la intención de adjuntarlo a un informe. La instantánea utiliza la versión de esquema 3 e incluye slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, configuración de banda TX y estado de secuencia de audio remoto RX.
4. Si cambiaste el estado del slice después de abrir el diálogo, haz clic en **Refresh Snapshot** para releer el estado actual del slice.
5. Para compartir el texto del resumen, haz clic en **Copy Summary**. El texto se copia al portapapeles.
6. Para compartir el JSON completo, haz clic en **Copy JSON**. La instantánea JSON completa se copia al portapapeles.
7. Para guardar el JSON en un archivo, haz clic en **Export JSON...** y elige una ubicación de guardado en el diálogo de archivo que se abre.
8. Observa la etiqueta de estado en la parte inferior del diálogo. Confirma el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard").
9. Haz clic en **Close** cuando termines.

## Qué hace cada control

| Control              | Tipo      | Comportamiento                                                                                                                                                                                                   |
|----------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Issue Summary**    | Pestaña   | Muestra una lista de viñetas en lenguaje natural de problemas detectados, incluido enrutamiento de audio, estado DSP, dispositivo de control (MIDI) y problemas de propiedad multicliente.                                                  |
| **JSON**             | Pestaña   | Muestra la instantánea JSON completa (versión de esquema 3) de slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, configuración de banda TX y estado de secuencia de audio remoto RX.                         |
| **Refresh Snapshot** | Botón    | Relee el estado actual del slice desde la radio y actualiza ambas pestañas.                                                                                                                                         |
| **Copy Summary**     | Botón    | Copia el texto del resumen de problemas al portapapeles.                                                                                                                                                            |
| **Copy JSON**        | Botón    | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                            |
| **Export JSON...**   | Botón    | Abre un diálogo de guardado para escribir la instantánea JSON en un archivo.                                                                                                                                  |
| **Close**            | Botón    | Cierra el diálogo.                                                                                                                                                                                         |
| Etiqueta de estado   | Indicador | Muestra el resultado de la última acción de copia o exportación (por ejemplo, "Copied to clipboard").                                                                                                                   |

## Lo que incluye Issue Summary

La pestaña Issue Summary reporta problemas en varias áreas. A partir de v0.9.4, el resumen también incluye dos secciones de audio remoto RX:

- **Radio-level remote audio RX** — Reporta el ID de secuencia, si la secuencia se espera, si la creación está pendiente, si se ha visto un mensaje de estado, si la secuencia es propiedad de este cliente, la configuración de compresión en uso y cualquier nota de enrutamiento que explique por qué la secuencia está o no activa.
- **Per-slice radio stream route** — Reporta el ID de secuencia de audio remoto RX para la ruta RX del slice junto con indicadores de si la secuencia se espera, la creación está pendiente, se ha solicitado la eliminación, se ha visto un mensaje de estado y si la secuencia es propiedad de este cliente.

## Sugerencias

- Captura la instantánea antes y después de cambiar la configuración del slice si estás intentando aislar un problema. Usa **Refresh Snapshot** entre capturas para actualizar los datos.
- Si estás reportando un problema de transverter, la pestaña **JSON** incluye la frecuencia RF, frecuencia IF, desplazamiento e indicadores de validez de cada transverter. La pestaña **Issue Summary** marcará cualquier transverter donde no se pueda confirmar la validez.
- Si estás reportando un problema de audio remoto, la pestaña **Issue Summary** ahora incluye el estado de la secuencia de audio remoto RX tanto a nivel de radio como a nivel individual de slice. Copia o exporta la instantánea y compártela con soporte o pégala en una herramienta de resolución de problemas asistida por IA para análisis.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Lee una lista en lenguaje natural de problemas sospechados con slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copia la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exporta la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualiza la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Inspecciona la RF/IF, desplazamiento e indicadores de validez de cada transverter para diagnóstico XVTR](inspect-each-transverter-s-rf-if-offset-and-validity-flags-for-xvtr-diagnosis.md)
