# Copiar el snapshot JSON completo al portapapeles

El diálogo Slice Troubleshooting captura un snapshot JSON (esquema v3) de cada slice, panadapter, transverter, canal DAX, dispositivo de audio, estado DSP del cliente y enlaces de dispositivo de control (MIDI). Esta página explica cómo copiar ese snapshot al portapapeles para pegarlo en un ticket de soporte, una publicación en el foro o un informe de error.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El diálogo requiere una conexión de radio activa.
- Si el estado del slice ha cambiado desde la última vez que abrió el diálogo, haga clic en `Refresh Snapshot` antes de copiar para asegurarse de que los datos estén actualizados.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña `JSON`.
3. Haga clic en `Copy JSON`.
4. Confirme que la etiqueta de estado muestre `Copied to clipboard`.
5. Pegue el contenido en la aplicación de destino.

## Qué hace cada control

| Control               | Tipo   | Comportamiento                                                                                                                                                                             |
|-----------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `JSON` (pestaña)      | Pestaña | Muestra el snapshot JSON completo (esquema v3) de los slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control y configuración de banda TX.            |
| `Issue Summary` (pestaña) | Pestaña | Muestra una lista de viñetas en lenguaje sencillo con los problemas detectados, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI) y propiedad multicliente. |
| `Refresh Snapshot`    | Botón  | Vuelve a leer el estado actual del slice en el snapshot. Haga clic aquí después de realizar cualquier cambio en el slice antes de copiar.                                                  |
| `Copy JSON`           | Botón  | Copia el snapshot JSON completo al portapapeles.                                                                                                                                           |
| `Copy Summary`        | Botón  | Copia el texto del resumen de problemas al portapapeles en su lugar.                                                                                                                       |
| `Export JSON...`      | Botón  | Guarda el snapshot JSON en un archivo.                                                                                                                                                     |
| `Close`               | Botón  | Cierra el diálogo.                                                                                                                                                                         |

## Qué incluye el Issue Summary

La pestaña `Issue Summary` genera una lista de viñetas en lenguaje sencillo a partir del snapshot. A partir de la v0.9.4, el resumen incluye los siguientes elementos adicionales:

### Audio RX remoto (nivel de radio)

El resumen ahora reporta el estado del flujo de audio RX remoto a nivel de radio, incluyendo:

- ID del flujo, si el flujo era esperado, si la creación está pendiente, si se ha recibido un mensaje de estado, si este cliente es propietario del flujo y la configuración de compresión en uso.
- Una nota de enrutamiento que explica cualquier problema de enrutamiento detectado para el flujo de audio RX remoto.

### Audio RX remoto (ruta de flujo de radio por slice)

Para cada slice, el resumen también reporta la ruta del flujo de radio por slice para el audio RX remoto, incluyendo:

- ID del flujo, indicador de esperado, indicador de creación pendiente, indicador de eliminación solicitada, indicador de estado recibido e indicador de propiedad propia.

Estas entradas aparecen junto a la información existente de dispositivo de audio, DSP y ruta TX ya presente en el resumen.

## Consejos

- Si desea únicamente un resumen de problemas en lenguaje sencillo en lugar del JSON completo, use `Copy Summary` en la pestaña `Issue Summary`.
- Para obtener el snapshot más preciso, realice primero los cambios de configuración del slice, luego haga clic en `Refresh Snapshot` y después en `Copy JSON`.
- El snapshot JSON puede pegarse directamente en un asistente de inteligencia artificial para obtener orientación en la resolución de problemas.

## Temas relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar un snapshot de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar el snapshot a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar el snapshot después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje sencillo de posibles problemas del slice](read-a-plain-language-list-of-suspected-slice-problems.md)
