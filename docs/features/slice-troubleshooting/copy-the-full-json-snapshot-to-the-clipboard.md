# Copiar la instantánea JSON completa al portapapeles

El diálogo Slice Troubleshooting captura una instantánea JSON (esquema v3) de cada slice, panadapter, transverter, canal DAX, dispositivo de audio, estado DSP del cliente y enlaces de dispositivos de control (MIDI). Esta página explica cómo copiar esa instantánea al portapapeles para pegarla en un ticket de soporte, publicación de foro o informe de errores.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo requiere una conexión de radio activa.
- Si el estado del slice ha cambiado desde la última vez que abrió el diálogo, haga clic en `Refresh Snapshot` antes de copiar para garantizar que los datos estén actualizados.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña `JSON`.
3. Haga clic en `Copy JSON`.
4. Confirme que la etiqueta de estado indica `Copied to clipboard`.
5. Pegue en su aplicación de destino.

## Qué hace cada control

| Control               | Tipo   | Comportamiento                                                                                                                                                                                   |
|-----------------------|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `JSON` (pestaña)      | Pestaña | Muestra la instantánea JSON completa (esquema v3) de slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control y configuración de banda TX.                    |
| `Issue Summary` (pestaña) | Pestaña | Muestra una lista con viñetas en lenguaje natural de problemas detectados, incluido enrutamiento de audio, DSP, estado de dispositivos de control (MIDI) y propiedad de múltiples clientes.     |
| `Refresh Snapshot`    | Botón  | Vuelve a leer el estado actual del slice en la instantánea. Haga clic después de realizar cualquier cambio en el slice antes de copiar.                                                       |
| `Copy JSON`           | Botón  | Copia la instantánea JSON completa al portapapeles.                                                                                                                                            |
| `Copy Summary`        | Botón  | Copia el texto del resumen de problemas al portapapeles en su lugar.                                                                                                                           |
| `Export JSON...`      | Botón  | Guarda la instantánea JSON en un archivo.                                                                                                                                                      |
| `Close`               | Botón  | Cierra el diálogo.                                                                                                                                                                             |

## Qué incluye el resumen de problemas

La pestaña `Issue Summary` genera una lista con viñetas en lenguaje natural a partir de la instantánea. A partir de v0.9.4, el resumen incluye los siguientes elementos adicionales:

### Audio remoto RX (nivel de radio)

El resumen ahora informa el estado de la secuencia de audio remoto RX a nivel de radio, incluido:

- ID de secuencia, si la secuencia era esperada, si la creación está pendiente, si se ha visto un mensaje de estado, si este cliente es propietario de la secuencia y la configuración de compresión en uso.
- Una nota de enrutamiento que explica cualquier problema de enrutamiento detectado para la secuencia de audio remoto RX.

### Audio remoto RX (ruta de secuencia de radio por slice)

Para cada slice, el resumen también informa la ruta de secuencia de radio por slice para audio remoto RX, incluido:

- ID de secuencia, indicador esperado, indicador de creación pendiente, indicador de eliminación solicitada, indicador de estado visto e indicador de propiedad del cliente.

Estas entradas aparecen junto con la información existente de dispositivo de audio, DSP y enrutamiento TX ya presente en el resumen.

## Consejos

- Si desea solo un resumen de problemas en lenguaje natural en lugar del JSON completo, use `Copy Summary` en la pestaña `Issue Summary` en su lugar.
- Para obtener la instantánea más precisa, realice primero cualquier cambio de configuración del slice, luego haga clic en `Refresh Snapshot`, luego en `Copy JSON`.
- La instantánea JSON se puede pegar directamente en un asistente de IA para solucionar problemas guiado.

## Relacionado

- [Descripción general de Slice Troubleshooting](overview.md)
- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar la instantánea a un archivo para adjuntarlo a un informe de errores](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje natural de problemas de slice sospechosos](read-a-plain-language-list-of-suspected-slice-problems.md)
