# Copiar la instantánea JSON completa al portapapeles

El cuadro de diálogo de Solución de problemas de Slices captura una instantánea JSON (esquema v3) de cada slice, panadapter, transverter, canal DAX, dispositivo de audio, estado DSP del cliente, punto de conexión de audio, enlaces de dispositivos de control (MIDI) y estado del renderizador. Esta página explica cómo copiar esa instantánea al portapapeles para poder pegarla en un ticket de soporte, publicación de foro o informe de error.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El cuadro de diálogo requiere una conexión de radio activa.
- Si el estado del slice ha cambiado desde que abrió el cuadro de diálogo por última vez, haga clic en `Refresh Snapshot` antes de copiar para asegurarse de que los datos estén actualizados.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña `JSON`.
3. Haga clic en `Copy JSON`.
4. Confirme que la etiqueta de estado muestre `Copied to clipboard`.
5. Pegue en la aplicación de destino.

## Qué hace cada control

| Control               | Tipo   | Comportamiento                                                                                                                                                                              |
|-----------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `JSON` (pestaña)      | Pestaña | Muestra la instantánea JSON completa (esquema v3) de slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, puntos de conexión de audio y estado del renderizador. |
| `Issue Summary` (pestaña) | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados, incluyendo enrutamiento de audio, DSP, estado de dispositivos de control (MIDI), propiedad de múltiples clientes, estado de conexión del panadapter y estado del punto de conexión de audio. |
| `Refresh Snapshot`    | Botón   | Vuelve a leer el estado actual del slice en la instantánea. Haga clic en este botón después de realizar cualquier cambio en slices antes de copiar.                                          |
| `Copy JSON`           | Botón   | Copia la instantánea JSON completa al portapapeles.                                                                                                                                         |
| `Copy Summary`        | Botón   | Copia el texto del resumen de problemas al portapapeles en su lugar.                                                                                                                        |
| `Export JSON...`      | Botón   | Guarda la instantánea JSON en un archivo.                                                                                                                                                   |
| `Close`               | Botón   | Cierra el cuadro de diálogo.                                                                                                                                                                |

## Qué incluye el Resumen de Problemas

La pestaña `Issue Summary` genera una lista con viñetas en lenguaje sencillo a partir de la instantánea. A partir de la v26.6.1, el resumen incluye los siguientes elementos adicionales:

### RX de audio remoto (a nivel de radio)

El resumen ahora informa el estado del flujo de RX de audio remoto a nivel de radio, incluyendo:

- ID del flujo, si se esperaba el flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si este cliente posee el flujo y la configuración de compresión en uso.
- Una nota de enrutamiento que explica cualquier problema de enrutamiento detectado para el flujo de RX de audio remoto.

### RX de audio remoto (ruta del flujo de radio por slice)

Para cada slice, el resumen también informa la ruta del flujo de radio por slice para el RX de audio remoto, incluyendo:

- ID del flujo, indicador de esperado, indicador de creación pendiente, indicador de eliminación solicitada, indicador de estado visto e indicador de propiedad nuestra.

Estas entradas aparecen junto a la información existente sobre dispositivo de audio, DSP y ruta de TX que ya estaba presente en el resumen.

### Estado de conexión del panadapter a slices

Para cada panadapter, el resumen ahora informa su estado de conexión a los slices, incluyendo:

- Estado (por ejemplo, "connected", "partially_connected"), resumen del estado de conexión, lista de IDs de slices conectados, lista de IDs de slices activos e indicación de si la conexión requiere atención.

### Estado del punto de conexión de audio

Para cada punto de conexión de audio, el resumen informa:

- Nombre, dirección (INPUT/OUTPUT), tipo, indicador operativo, indicador de ejecución, estado, error, backend, nombre del dispositivo, frecuencia de muestreo, cantidad de canales, formato de muestra, indicador de remuestreo, estadísticas del búfer (bytes del búfer, bytes pico del búfer, cantidad de subejecuciones) y cualquier nota orientada al usuario.

Estas entradas aparecen junto a la información existente sobre el dispositivo de audio y el dispositivo de control.

## Consejos

- Si solo desea un resumen de problemas en lenguaje sencillo en lugar del JSON completo, use `Copy Summary` en la pestaña `Issue Summary`.
- Para obtener la instantánea más precisa, realice primero cualquier cambio en la configuración del slice, luego haga clic en `Refresh Snapshot` y después en `Copy JSON`.
- La instantánea JSON se puede pegar directamente en un asistente de IA para obtener ayuda guiada en la solución de problemas.

## Relacionados

- [Descripción general de la solución de problemas de slices](overview.md)
- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar la instantánea a un archivo para adjuntarla a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje sencillo de problemas sospechosos del slice](read-a-plain-language-list-of-suspected-slice-problems.md)
