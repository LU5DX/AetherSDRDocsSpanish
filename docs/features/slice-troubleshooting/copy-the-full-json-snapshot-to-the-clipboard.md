# Copiar la instantánea JSON completa al portapapeles

El cuadro de diálogo de Solución de problemas de Slices captura una instantánea JSON (esquema v3) de todos los slices, panadapters, transverters, canales DAX, dispositivos de audio, estado DSP del cliente y enlaces de dispositivos de control (MIDI). Esta página explica cómo copiar esa instantánea al portapapeles para pegarla en un ticket de soporte, publicación en un foro o informe de error.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo requiere una conexión de radio activa.
- Si el estado del slice ha cambiado desde que abrió el diálogo, haga clic en `Refresh Snapshot` antes de copiar para asegurarse de que los datos estén actualizados.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña `JSON`.
3. Haga clic en `Copy JSON`.
4. Confirme que la etiqueta de estado muestra `Copied to clipboard`.
5. Pegue en su aplicación de destino.

## Qué hace cada control

| Control               | Tipo    | Comportamiento                                                                                                                                                                            |
|-----------------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `JSON` (pestaña)      | Pestaña | Muestra la instantánea JSON completa (esquema v3) de slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control y configuraciones de banda TX.            |
| `Issue Summary` (pestaña) | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados, incluyendo enrutamiento de audio, DSP, estado de dispositivos de control (MIDI) y propiedad multi-cliente. |
| `Refresh Snapshot`    | Botón   | Vuelve a leer el estado actual del slice en la instantánea. Haga clic aquí después de realizar cualquier cambio en los slices antes de copiar.                                           |
| `Copy JSON`           | Botón   | Copia la instantánea JSON completa al portapapeles.                                                                                                                                       |
| `Copy Summary`        | Botón   | Copia el texto del resumen de problemas al portapapeles en su lugar.                                                                                                                      |
| `Export JSON...`      | Botón   | Guarda la instantánea JSON en un archivo.                                                                                                                                                 |
| `Close`               | Botón   | Cierra el cuadro de diálogo.                                                                                                                                                              |

## Qué incluye el Resumen de problemas

La pestaña `Issue Summary` genera una lista con viñetas en lenguaje sencillo a partir de la instantánea. A partir de v0.9.4, el resumen incluye los siguientes elementos adicionales:

### RX de audio remoto (nivel de radio)

El resumen ahora reporta el estado del flujo RX de audio remoto a nivel de radio, incluyendo:

- ID del flujo, si se esperaba el flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si este cliente posee el flujo y la configuración de compresión en uso.
- Una nota de enrutamiento que explica cualquier problema de enrutamiento detectado para el flujo RX de audio remoto.

### RX de audio remoto (ruta de flujo de radio por slice)

Para cada slice, el resumen también reporta la ruta de flujo de radio por slice para RX de audio remoto, incluyendo:

- ID del flujo, bandera de esperado, bandera de creación pendiente, bandera de eliminación solicitada, bandera de estado visto y bandera de propiedad nuestra.

Estas entradas aparecen junto con la información existente del dispositivo de audio, DSP y ruta TX ya presente en el resumen.

## Consejos

- Si solo desea un resumen de problemas en lenguaje sencillo en lugar del JSON completo, use `Copy Summary` en la pestaña `Issue Summary`.
- Para obtener la instantánea más precisa, realice primero los cambios de configuración del slice, luego haga clic en `Refresh Snapshot` y después en `Copy JSON`.
- La instantánea JSON se puede pegar directamente en un asistente de IA para obtener ayuda guiada con la solución de problemas.

## Relacionados

- [Descripción general de Solución de problemas de Slices](overview.md)
- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje sencillo de posibles problemas del slice](read-a-plain-language-list-of-suspected-slice-problems.md)
