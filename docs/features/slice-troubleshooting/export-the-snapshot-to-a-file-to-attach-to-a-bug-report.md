# Exportar la instantánea a un archivo para adjuntar a un informe de error

Utilice esta página para guardar la instantánea JSON del diálogo Slice Troubleshooting en un archivo en disco, de modo que pueda adjuntarlo a una solicitud de soporte o a un informe de error.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo Slice Troubleshooting requiere una conexión activa a la radio.
- Abra el diálogo Slice Troubleshooting mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Abra el diálogo Slice Troubleshooting: `Help > Slice Troubleshooting...`
2. Haga clic en `Refresh Snapshot` para asegurarse de que la instantánea refleje el estado actual del slice.
3. Haga clic en `Export JSON...`.
4. En el diálogo de guardado de archivo que aparece, elija una carpeta de destino y un nombre de archivo, luego confirme el guardado.
5. Verifique la etiqueta de estado en la parte inferior del diálogo para confirmar que la exportación se haya realizado correctamente.
6. Adjunte el archivo guardado a su informe de error o ticket de soporte.

## Consejos

- Si ha realizado cambios en la configuración del slice después de abrir el diálogo, haga clic en `Refresh Snapshot` nuevamente antes de exportar para capturar el estado más reciente.
- Si solo necesita pegar la instantánea en un formulario web o correo electrónico en lugar de adjuntar un archivo, use `Copy JSON` en lugar de `Export JSON...`.
- Para compartir los problemas detectados en lenguaje sencillo en lugar de datos sin procesar, haga clic en `Copy Summary` para copiar el contenido de la pestaña de resumen de incidencias al portapapeles.

## Qué incluye el Issue Summary

La pestaña **Issue Summary** muestra una lista con viñetas en lenguaje sencillo de los problemas detectados. A partir de la v26.6.1, el resumen incluye estas secciones:

- **Slices** — enumera cada slice por índice, frecuencia, modo, ancho de banda del filtro, dispositivo de audio, antena RX y estado de silencio. También incluye el estado de conexión del slice que muestra los IDs de slice conectados y activos, y si se requiere atención.
- **Panadapters** — enumera cada panadapter por ID, frecuencia central, ancho de banda, ganancia RF, estado del preamplificador, WNB activo/inactivo e ID del waterfall. Cuando los datos de estado de conexión del slice están disponibles, muestra el resumen del estado de conexión, los IDs de slice conectados y los IDs de slice activos, con un marcador de (atención) si la radio indica un problema.
- **Transverters** — enumera cada transverter por nombre, rango de frecuencia, frecuencia FI y validez.
- **DAX channels** — enumera cada canal DAX por índice, nombre, frecuencia, modo y nivel de squelch.
- **Audio endpoints** — informa el estado operativo y de ejecución, la tasa de muestreo, el número de canales, el formato de muestra, el estado de remuestreo, las estadísticas del búfer y el conteo de underruns para cada endpoint de audio.
- **Remote audio RX** — informa el ID del flujo, si se espera un flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si el flujo es propiedad de este cliente y la configuración de compresión en uso.
- **Remote audio route note** — una nota de enrutamiento en texto libre que puede indicar por qué un flujo de audio RX remoto no funciona como se espera.

Cada sección de ruta de audio del slice también incluye ahora una línea **Radio stream route** que informa el ID del flujo de audio RX remoto junto con sus banderas de esperado, creación pendiente, eliminación solicitada, estado visto y propiedad nuestra. Revise estas líneas primero al diagnosticar problemas de audio RX remoto antes de contactar al soporte.

## Solución de problemas

- **La etiqueta de estado no muestra confirmación después de hacer clic en `Export JSON...`** — Es posible que haya cancelado el diálogo de guardado de archivo sin elegir una ubicación. Haga clic en `Export JSON...` nuevamente y confirme el guardado.
- **`Export JSON...` no está disponible** — El diálogo requiere una conexión activa a la radio. Verifique que AetherSDR esté conectado a la radio antes de abrir el diálogo.
- **Todos los campos de audio RX remoto muestran marcadores de posición** — AetherSDR aún no ha recibido un mensaje de estado de la radio para ese flujo. Haga clic en `Refresh Snapshot` después de que la radio haya tenido un momento para enviar el estado del flujo, luego verifique nuevamente la pestaña **Issue Summary**.
- **Las viñetas del panadapter muestran "Slice link state unavailable."** — La radio no proporcionó datos de estado de conexión del slice para ese panadapter. Esto puede ser normal para versiones de firmware más antiguas o durante el inicio. Haga clic en `Refresh Snapshot` para intentarlo nuevamente.

## Relacionados

- [Capture a slice snapshot for support](capture-a-slice-snapshot-for-support.md)
- [Copy the full JSON snapshot to the clipboard](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Refresh the snapshot after changing slice state](refresh-the-snapshot-after-changing-slice-state.md)
- [Read a plain-language list of suspected slice problems](read-a-plain-language-list-of-suspected-slice-problems.md)
- [Copy the issue summary to the clipboard](copy-the-issue-summary-to-the-clipboard.md)
