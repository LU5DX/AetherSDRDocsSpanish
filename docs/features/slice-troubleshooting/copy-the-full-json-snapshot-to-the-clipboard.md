# Solución de problemas de Slice

El cuadro de diálogo de Solución de problemas de Slice captura una instantánea JSON (esquema v3) de cada slice, panadapter, transverter, canal DAX, dispositivo de audio, estado de DSP del cliente, punto final de audio, enlaces de dispositivos de control (MIDI) y estado del renderizador, y resume los problemas probables (audio faltante, silencio atascado, antena faltante, validez de XVTR) en lenguaje sencillo. Esta página explica cómo capturar y compartir esa instantánea para soporte.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El cuadro de diálogo requiere una conexión de radio activa.
- Si el estado del slice ha cambiado desde la última vez que abrió el cuadro de diálogo, haga clic en `Refresh Snapshot` antes de copiar para asegurarse de que los datos estén actualizados.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Revise la pestaña `Issue Summary` para obtener una lista en lenguaje sencillo de los problemas detectados, o haga clic en la pestaña `JSON` para ver la instantánea completa.
3. Haga clic en `Copy Summary` para copiar el resumen de problemas al portapapeles, o `Copy JSON` para copiar la instantánea JSON completa.
4. Confirme que la etiqueta de estado indique `Copied to clipboard`.
5. Pegue en su aplicación de destino.

## Funciones de cada control

| Control                 | Tipo        | Comportamiento                                                                                                                  |
|-------------------------|-------------|---------------------------------------------------------------------------------------------------------------------------------|
| `Issue Summary` (pestaña) | Pestaña     | Muestra una lista con viñetas en lenguaje sencillo de los problemas detectados.                                                  |
| `JSON` (pestaña)          | Pestaña     | Muestra la instantánea JSON completa (esquema v3) de slices, canales DAX, dispositivos de audio, estado de DSP del cliente, dispositivos de control, puntos finales de audio y estado del renderizador. |
| `Refresh Snapshot`      | Botón       | Vuelve a leer el estado actual del slice en la instantánea. Haga clic en esto después de realizar cualquier cambio en los slices antes de copiar. |
| `Copy Summary`          | Botón       | Copia el texto del resumen de problemas al portapapeles.                                                                         |
| `Copy JSON`             | Botón       | Copia la instantánea JSON completa al portapapeles.                                                                              |
| `Export JSON...`        | Botón       | Guarda la instantánea JSON en un archivo.                                                                                        |
| `Find:`                 | Campo de texto| Resalta las coincidencias del término ingresado en la pestaña activa (Issue Summary o JSON). Tiene botón de borrar y texto de marcador de posición 'Search snapshot...'. Enter salta a la siguiente coincidencia; el intercambio de pestañas actualiza los recuentos de resaltado. La etiqueta de estado muestra '<N> match(es) in current tab.' |
| `Find Next`             | Botón       | Salta a la siguiente coincidencia del término de búsqueda en la pestaña activa. Rodea dentro de la pestaña actual. Un término vacío no produce coincidencias. |
| `Close`                 | Botón       | Cierra el cuadro de diálogo.                                                                                                     |

## Qué incluye el Resumen de problemas

La pestaña `Issue Summary` genera una lista con viñetas en lenguaje sencillo a partir de la instantánea. A partir de v26.8.4, el resumen incluye lo siguiente:

### Frescura del medidor TX

El resumen ahora informa si los medidores TX están en vivo. Si la muestra del medidor TX está desactualizada, el resumen muestra:

- Una advertencia de que los medidores TX NO están en vivo, con la antigüedad de la última muestra (o una nota de que no se ha recibido ninguna muestra del medidor TX en esta sesión).
- Una explicación de que la potencia directa TX mostrada es el último valor recibido, no una lectura actual, y que la ROE TX se omite en lugar de mostrarse desactualizada.

Esto evita diagnósticos erróneos donde una potencia plausible junto a una ROE ausente podría llevar al lector a concluir que la antena es el problema.

### Estado del punto final de audio

Para cada punto final de audio, el resumen informa:

- Nombre, dirección (ENTRADA/SALIDA), tipo, indicador operativo, indicador de ejecución, estado, error, backend, nombre del dispositivo, tasa de muestreo, número de canales, formato de muestra, indicador de remuestreo y estadísticas del búfer (bytes del búfer, bytes máximos del búfer, recuento de underrun).
- Cuando corresponde, normalización de entrada de voz a 48 kHz, remuestreo de salida de voz a 24 kHz y remuestreo RADE a 24 kHz.
- Cualquier nota dirigida al usuario.

### RX de audio remoto (a nivel de radio)

El resumen informa el estado del flujo de RX de audio remoto a nivel de radio, incluyendo:

- ID del flujo, si se esperaba el flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si este cliente es propietario del flujo y la configuración de compresión en uso.
- Una nota de enrutamiento que explica cualquier problema de enrutamiento detectado para el flujo de RX de audio remoto.

### RX de audio remoto (ruta del flujo de radio por slice)

Para cada slice, el resumen también informa la ruta del flujo de radio por slice para el RX de audio remoto, incluyendo:

- ID del flujo, indicador de esperado, indicador de creación pendiente, indicador de eliminación solicitada, indicador de estado visto e indicador de propiedad nuestra.

### Estado de conexión de slices del panadapter

Para cada panadapter, el resumen informa su estado de conexión a los slices, incluyendo:

- Estado (por ejemplo, "connected", "partially_connected"), resumen del estado de conexión, lista de IDs de slices conectados, lista de IDs de slices activos y si la conexión requiere atención.

### Configuración NR2 del DSP del cliente

El resumen incluye la configuración completa de reducción de ruido NR2 leída del `Nr2SettingsModel`, incluyendo:

- Método de ganancia y nombre del método, método NPE y nombre del método, filtro AE habilitado/deshabilitado, ganancia máxima, ganancia mínima, suavizado de ganancia y Qspp.

## Consejos

- Use el campo `Find:` para buscar términos específicos dentro de la pestaña activa. La etiqueta de estado muestra el recuento de coincidencias y `Find Next` salta a la siguiente ocurrencia (rodeando dentro de la pestaña actual).
- Si desea solo un resumen de problemas en lenguaje sencillo en lugar del JSON completo, use `Copy Summary` en la pestaña `Issue Summary`.
- Para obtener la instantánea más precisa, realice primero cualquier cambio en la configuración de los slices, luego haga clic en `Refresh Snapshot` y después en `Copy JSON`.
- La instantánea JSON se puede pegar directamente en un asistente de IA para una solución de problemas guiada.

## Relacionado

- [Descripción general de Solución de problemas de Slice](overview.md)
- [Capturar una instantánea de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Exportar la instantánea a un archivo para adjuntarlo a un informe de error](export-the-snapshot-to-a-file-to-attach-to-a-bug-report.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje sencillo de problemas sospechosos de slice](read-a-plain-language-list-of-suspected-slice-problems.md)
