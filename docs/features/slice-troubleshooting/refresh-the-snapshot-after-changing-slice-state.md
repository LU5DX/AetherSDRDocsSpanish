# Actualizar la instantánea después de cambiar el estado del slice

Después de modificar la configuración del slice —como ajustar el enrutamiento de audio, activar o desactivar el silencio, o cambiar las antenas— el cuadro de diálogo de Solución de problemas del slice no se actualiza automáticamente. Utilice **Actualizar instantánea** para volver a leer el estado actual del slice, de modo que el Resumen de incidencias y el JSON reflejen sus cambios.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El cuadro de diálogo de Solución de problemas del slice requiere una conexión activa con el equipo.
- Abra el cuadro de diálogo mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Realice el cambio de estado del slice que desea capturar (por ejemplo, reactivar el audio de un slice, reasignar una antena o ajustar un canal DAX).
2. En el cuadro de diálogo de Solución de problemas del slice, haga clic en **Actualizar instantánea**.
3. El cuadro de diálogo vuelve a leer todo el estado del slice, panadaptador, transvertor, canal DAX, dispositivo de audio, DSP del cliente, enlace de dispositivo de control (MIDI), punto final de audio, renderizador, RX de audio remoto y conexión del slice del panadaptador.
4. Revise los resultados actualizados en la pestaña **Resumen de incidencias** o en la pestaña **JSON**.

## Función de cada control

| Control                     | Tipo   | Comportamiento                                                                                                                                                                      |
|-----------------------------|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Actualizar instantánea**  | Botón  | Vuelve a leer el estado del slice en la instantánea. Utilícelo tras cualquier cambio de configuración del slice.                                                                     |
| **Resumen de incidencias** (pestaña) | Pestaña | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados según la instantánea actual, incluyendo enrutamiento de audio, DSP, estado del dispositivo de control (MIDI), propiedad multi-cliente, enrutamiento RX de audio remoto, estado del punto final de audio, estado del renderizador y estado de conexión del slice del panadaptador. |
| **JSON** (pestaña)          | Pestaña | Muestra la instantánea JSON completa (versión 3 del esquema) de los slices, canales DAX, dispositivos de audio, DSP del cliente, dispositivos de control, puntos finales de audio, renderizadores, ajustes de banda TX, estado RX de audio remoto y estado de conexión del slice del panadaptador. |
| **Copiar resumen**          | Botón  | Copia el resumen de incidencias al portapapeles.                                                                                                                                     |
| **Copiar JSON**             | Botón  | Copia el JSON completo al portapapeles.                                                                                                                                              |
| **Exportar JSON...**        | Botón  | Guarda el JSON en un archivo.                                                                                                                                                        |
| **Cerrar**                  | Botón  | Cierra el cuadro de diálogo.                                                                                                                                                         |

## Qué informa el Resumen de incidencias

La pestaña **Resumen de incidencias** incluye las siguientes categorías de información. Cada elemento aparece como una viñeta en lenguaje sencillo en el resumen.

### Estado de audio y hardware a nivel de equipo

- Ganancia de auriculares, silencio de auriculares y estado de silencio del altavoz frontal.
- Configuración del oscilador, estado de bloqueo, referencia externa y estado del TCXO.

### Estado RX de audio remoto

El resumen incluye dos viñetas para RX de audio remoto:

- **RX de audio remoto:** Informa el ID del flujo, si se espera un flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si este cliente posee el flujo y la configuración de compresión en uso.
- **Nota de ruta RX de audio remoto:** Una nota en lenguaje sencillo sobre el estado de enrutamiento RX de audio remoto, si está disponible.

### Enrutamiento de audio por slice

Para cada slice, el resumen informa:

- Volumen RX del motor, estado de silencio y si el audio RX está en transmisión.
- **Ruta de flujo del equipo:** Informa el ID del flujo RX de audio remoto, si se espera el flujo, si la creación o eliminación está pendiente, si se ha visto un mensaje de estado y si este cliente posee el flujo.
- Ruta de entrada TX, selección de micrófono, modo TX DAX y ajustes relacionados.

### Estado del punto final de audio

Para cada punto final de audio, el resumen informa:

- Nombre, dirección (INPUT o OUTPUT) y tipo (tipo de punto final).
- Backend, nombre del dispositivo, frecuencia de muestreo, cantidad de canales, formato de muestra y si el remuestreo está activo.
- Estado operativo y de ejecución, estado del flujo e información de errores.
- Estadísticas del búfer (bytes del búfer, bytes pico y cantidad de subejecuciones) si están disponibles.
- Cualquier nota adicional sobre el punto final.

### Estado del renderizador

Para cada renderizador en el motor de audio, el resumen informa el nombre del renderizador, un identificador del backend, la frecuencia de muestreo y si el audio está actualmente activo.

### Estado de conexión del slice del panadaptador

Para cada panadaptador, el resumen informa:

- El estado de conexión del slice, un resumen legible del estado del enlace, la lista de IDs de slice conectados, la lista de IDs de slice activos y si la conexión requiere atención.

### Enlaces del dispositivo de control (MIDI)

El resumen informa cada dispositivo de control y los enlaces MIDI asociados, incluyendo el alcance, los detalles de mapeo y las condiciones de error.

## Indicador de estado

Después de hacer clic en **Copiar resumen**, **Copiar JSON** o **Exportar JSON...**, una etiqueta de estado debajo de los botones muestra el resultado de la operación (por ejemplo, *Copiado al portapapeles*).

## Consejos

- Después de hacer clic en **Actualizar instantánea**, revise tanto la pestaña **Resumen de incidencias** como la pestaña **JSON** para confirmar que el cambio realizado se refleja antes de compartir la instantánea con el soporte técnico.
- Si planea exportar o copiar la instantánea para un informe de error, haga siempre clic en **Actualizar instantánea** primero para asegurarse de que los datos estén actualizados.
- La nota de ruta RX de audio remoto en el Resumen de incidencias es un indicador inicial útil de problemas de propiedad o creación del flujo al solucionar problemas de audio que no llegan al cliente.
- El estado de conexión del slice del panadaptador y los detalles del punto final de audio pueden ayudar a identificar problemas de conectividad o estado del flujo que podrían no aparecer en otro lugar.

## Relacionados

- [Descripción general de Solución de problemas del slice](overview.md)
- [Capturar una instantánea del slice para soporte técnico](capture-a-slice-snapshot-for-support.md)
- [Leer una lista en lenguaje sencillo de problemas sospechosos del slice](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Exportar la instantánea a un archivo para adjuntar a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
