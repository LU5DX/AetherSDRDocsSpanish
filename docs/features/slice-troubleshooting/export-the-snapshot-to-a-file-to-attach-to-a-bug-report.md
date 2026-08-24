# Exportar la instantánea a un archivo para adjuntarla a un informe de error

Use esta página para guardar la instantánea JSON del diálogo Slice Troubleshooting en un archivo en el disco, de modo que pueda adjuntarla a una solicitud de soporte o a un informe de error.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo Slice Troubleshooting requiere una conexión de radio activa.
- Abra el diálogo Slice Troubleshooting mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Abra el diálogo Slice Troubleshooting: `Help > Slice Troubleshooting...`
2. Haga clic en `Refresh Snapshot` para asegurarse de que la instantánea refleje el estado actual del slice.
3. Haga clic en `Export JSON...`.
4. En el diálogo de guardado de archivo que aparece, elija una carpeta de destino y un nombre de archivo, y luego confirme el guardado.
5. Verifique la etiqueta de estado en la parte inferior del diálogo para confirmar que la exportación se realizó correctamente.
6. Adjunte el archivo guardado a su informe de error o ticket de soporte.

## Consejos

- Si ha realizado cambios en la configuración del slice desde que abrió el diálogo, haga clic en `Refresh Snapshot` nuevamente antes de exportar para capturar el estado más reciente.
- Si solo necesita pegar la instantánea en un formulario web o correo electrónico en lugar de adjuntar un archivo, use `Copy JSON` en lugar de `Export JSON...`.
- Para compartir los problemas detectados en lenguaje sencillo en lugar de datos sin procesar, haga clic en `Copy Summary` para copiar el contenido de la pestaña de resumen de problemas al portapapeles.
- Para buscar dentro de la pestaña actual, escriba un término en el campo `Find:`. Haga clic en `Find Next` para saltar a la siguiente coincidencia. La etiqueta de estado muestra el número de coincidencias en la pestaña actual.
- El diálogo recuerda la posición y el tamaño de su ventana. Una sesión futura reutilizará esa configuración de geometría.

## Qué incluye el Issue Summary

La pestaña **Issue Summary** muestra una lista con viñetas en lenguaje sencillo de los problemas detectados. A partir de la v26.8.4, el resumen incluye estas secciones:

- **Slices** — enumera cada slice por índice, frecuencia, modo, ancho de banda del filtro, dispositivo de audio, antena RX y estado de silencio. También incluye el estado de conexión del slice que muestra los ID de slices conectados y activos, y si se requiere atención.
- **Panadapters** — enumera cada panadapter por ID, frecuencia central, ancho de banda, ganancia RF, estado del preamplificador, WNB activo/inactivo e ID del waterfall. Cuando los datos de estado de conexión del slice están disponibles, muestra el resumen del estado de conexión, los ID de slices conectados y los ID de slices activos, con un marcador de (atención) si la radio indica un problema.
- **Transverters** — enumera cada transverter por nombre, rango de frecuencia, frecuencia FI y validez.
- **DAX channels** — enumera cada canal DAX por índice, nombre, frecuencia, modo y nivel de squelch.
- **Audio endpoints** — informa el estado operativo y de ejecución, la frecuencia de muestreo, el número de canales, el formato de muestra, el estado de remuestreo, las estadísticas de búfer y el contador de underrun para cada endpoint de audio. Cuando esté disponible, los detalles del endpoint de audio también incluyen las marcas de normalización de entrada de voz a 48 kHz, remuestreo de salida de voz a 24 kHz y remuestreo RADE a 24 kHz.
- **Remote audio RX** — informa el ID de la transmisión, si se espera una transmisión, si la creación está pendiente, si se ha visto un mensaje de estado, si la transmisión pertenece a este cliente y la configuración de compresión en uso.
- **Remote audio route note** — una nota de ruta de texto libre que puede indicar por qué una transmisión de audio RX remota no funciona como se espera.
- **Client DSP snapshot** — informa la configuración de reducción de ruido NR2, incluidos el filtro AE, la ganancia máxima, el nivel mínimo de ganancia, la suavización de ganancia y QSPP. También informa el estado habilitado de reducción de ruido NR4 y el método de estimación de ruido.
- **TX meters** — cuando los datos del medidor TX no están en vivo, el resumen incluye una línea de advertencia que indica que la potencia directa TX es el último valor recibido en lugar de una lectura actual, y que la ROE TX se omite. La línea incluye la antigüedad de la última muestra cuando se conoce.

Cada sección de ruta de audio de slice ahora también incluye una línea **Radio stream route** que informa el ID de la transmisión de audio RX remota junto con sus marcas de esperado, creación pendiente, eliminación solicitada, estado visto y propiedad nuestra. Revise estas líneas primero al diagnosticar problemas de audio RX remoto antes de contactar al soporte.

## Uso de Find dentro del diálogo

El diálogo incluye un campo `Find:` que busca en la pestaña activa (**Issue Summary** o **JSON**):

1. Haga clic en la pestaña que desea buscar (**Issue Summary** o **JSON**).
2. Escriba un término de búsqueda en el campo `Find:`. El campo tiene un texto de marcador de posición "Search snapshot..." y un botón de borrado.
3. Mientras escribe, las coincidencias se resaltan y la etiqueta de estado muestra el número de coincidencias encontradas en la pestaña actual.
4. Presione Enter o haga clic en `Find Next` para saltar a la siguiente coincidencia. La búsqueda se envuelve dentro de la pestaña actual.
5. Haga clic en el botón de borrado del campo `Find:` para limpiar la búsqueda.

## Solución de problemas

- **La etiqueta de estado no muestra confirmación después de hacer clic en `Export JSON...`** — Es posible que haya cancelado el diálogo de guardado de archivo sin elegir una ubicación. Haga clic en `Export JSON...` nuevamente y confirme el guardado.
- **`Export JSON...` no está disponible** — El diálogo requiere una conexión de radio activa. Verifique que AetherSDR esté conectado a la radio antes de abrir el diálogo.
- **Los campos de audio RX remoto muestran todos marcadores de posición** — AetherSDR aún no ha recibido un mensaje de estado de la radio para esa transmisión. Haga clic en `Refresh Snapshot` después de que la radio haya tenido un momento para enviar el estado de la transmisión y luego revise la pestaña **Issue Summary** nuevamente.
- **Las viñetas de panadapter muestran "Slice link state unavailable."** — La radio no proporcionó datos de estado de conexión del slice para ese panadapter. Esto puede ser normal en versiones de firmware más antiguas o durante el inicio. Haga clic en `Refresh Snapshot` para intentar nuevamente.
- **El Issue Summary muestra una advertencia de que los medidores TX no están en vivo** — Esto indica que la radio no está proporcionando datos frescos del medidor TX en ese momento. La potencia directa TX muestra el último valor recibido en lugar de una lectura actual, y la ROE TX se omite en lugar de mostrarse desactualizada. Esta advertencia es esperada cuando el transmisor está inactivo o durante ciertos estados de la radio.

## Relacionados

- [Capture a slice snapshot for support](capture-a-slice-snapshot-for-support.md)
- [Copy the full JSON snapshot to the clipboard](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Refresh the snapshot after changing slice state](refresh-the-snapshot-after-changing-slice-state.md)
- [Read a plain-language list of suspected slice problems](read-a-plain-language-list-of-suspected-slice-problems.md)
- Copiar el resumen de problemas al portapapeles.
