# Copiar la instantánea JSON completa al portapapeles

El diálogo Solución de problemas de Slice captura una instantánea JSON (esquema v3) de cada slice, panadapter, transverter, canal DAX, dispositivo de audio, estado DSP del cliente, punto final de audio, enlaces de dispositivos de control (MIDI) y estado del renderizador. Esta página explica cómo copiar esa instantánea al portapapeles para poder pegarla en un ticket de soporte, publicación en un foro o informe de error.

## Antes de empezar

- AetherSDR debe estar conectado a una radio. El diálogo requiere una conexión activa con la radio.
- Si el estado del slice ha cambiado desde que abrió el diálogo por última vez, haga clic en `Refresh Snapshot` antes de copiar para asegurarse de que los datos estén actualizados.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña `JSON`.
3. Haga clic en `Copy JSON`.
4. Confirme que la etiqueta de estado muestre `Copied to clipboard`.
5. Péguelo en su aplicación de destino.

## Función de cada control

| Control               | Tipo     | Comportamiento                                                                                                                                                                                                                 |
|-----------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `JSON` (pestaña)      | Pestaña  | Muestra la instantánea JSON completa (esquema v3) de slices, canales DAX, dispositivos de audio, estado DSP del cliente, dispositivos de control, puntos finales de audio y estado del renderizador.                            |
| `Issue Summary` (pestaña) | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados, que incluye el enrutamiento de audio, el estado DSP y de dispositivos de control (MIDI), la propiedad de múltiples clientes, el estado de conexión del panadapter y el estado del punto final de audio. |
| `Refresh Snapshot`    | Botón   | Vuelve a leer el estado actual del slice en la instantánea. Haga clic aquí después de realizar cualquier cambio en los slices antes de copiar.                                                                                 |
| `Copy JSON`           | Botón   | Copia la instantánea JSON completa al portapapeles.                                                                                                                                                                            |
| `Copy Summary`        | Botón   | Copia el texto del resumen de problemas al portapapeles en su lugar.                                                                                                                                                          |
| `Export JSON...`      | Botón   | Guarda la instantánea JSON en un archivo.                                                                                                                                                                                      |
| `Close`               | Botón   | Cierra el diálogo.                                                                                                                                                                                                            |

## Qué incluye el Resumen de problemas

La pestaña `Issue Summary` genera una lista con viñetas en lenguaje sencillo a partir de la instantánea. A partir de la versión v26.7.4, el resumen incluye los siguientes elementos adicionales:

### RX de audio remoto (nivel de radio)

El resumen ahora informa el estado del flujo RX de audio remoto a nivel de radio, incluyendo:

- ID del flujo, si se esperaba el flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si este cliente posee el flujo y la configuración de compresión en uso.
- Una nota de enrutamiento que explica cualquier problema de enrutamiento detectado para el flujo RX de audio remoto.

### RX de audio remoto (ruta del flujo de radio por slice)

Para cada slice, el resumen también informa la ruta del flujo de radio por slice para el RX de audio remoto, incluyendo:

- ID del flujo, indicador de esperado, indicador de creación pendiente, indicador de eliminación solicitada, indicador de estado visto e indicador de propiedad por nuestro cliente.

Estas entradas aparecen junto a la información existente de dispositivo de audio, DSP y ruta TX ya presente en el resumen.

### Estado de conexión del panadapter a los slices

Para cada panadapter, el resumen ahora informa su estado de conexión a los slices, incluyendo:

- Estado (p. ej., "connected", "partially_connected"), resumen del estado de conexión, lista de IDs de slices conectados, lista de IDs de slices activos y si la conexión requiere atención.

### Estado del punto final de audio

Para cada punto final de audio, el resumen informa:

- Nombre, dirección (INPUT/OUTPUT), tipo, indicador operativo, indicador de ejecución, estado, error, backend, nombre del dispositivo, frecuencia de muestreo, número de canales, formato de muestra, indicador de remuestreo, estadísticas del búfer (bytes del búfer, pico de bytes del búfer, conteo de subejecuciones) y cualquier nota dirigida al usuario.

Estas entradas aparecen junto a la información existente de dispositivo de audio y dispositivo de control.

### Configuración NR2 del DSP del cliente

El resumen ahora incluye la configuración completa de reducción de ruido NR2 leída desde el `Nr2SettingsModel`, incluyendo:

- Método de ganancia y nombre del método, método NPE y nombre del método, filtro AE habilitado/deshabilitado, ganancia máxima, ganancia mínima, suavizado de ganancia, Qspp, e indicador de mapeo de geometría y ganancia heredado.

Anteriormente estos valores se leían desde `AppSettings`; ahora se leen desde el modelo centralizado de configuración NR2 para mantener la coherencia con el estado real del DSP.

## Consejos

- Si solo desea un resumen de problemas en lenguaje sencillo en lugar del JSON completo, use `Copy Summary` en la pestaña `Issue Summary`.
- Para obtener la instantánea más precisa, realice primero los cambios de configuración de los slices, luego haga clic en `Refresh Snapshot` y luego en `Copy JSON`.
- La instantánea JSON se puede pegar directamente en un asistente de IA para una resolución de problemas guiada.

## Relacionados

- [Descripción general de Solución de problemas de Slice](overview.md)
- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje sencillo de posibles problemas del slice](read-a-plain-language-list-of-suspected-slice-problems.md)
