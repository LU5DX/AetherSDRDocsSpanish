# Exportar la instantánea a un archivo para adjuntar a un informe de errores

Use esta página para guardar la instantánea JSON del diálogo Slice Troubleshooting en un archivo en disco y así adjuntarla a una solicitud de soporte o informe de errores.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo Slice Troubleshooting requiere una conexión de radio activa.
- Abra el diálogo Slice Troubleshooting mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Abra el diálogo Slice Troubleshooting: `Help > Slice Troubleshooting...`
2. Haga clic en `Refresh Snapshot` para asegurarse de que la instantánea refleja el estado actual del slice.
3. Haga clic en `Export JSON...`.
4. En el diálogo de guardar archivo que aparece, elija una carpeta de destino y un nombre de archivo, luego confirme el guardado.
5. Revise la etiqueta de estado en la parte inferior del diálogo para confirmar que la exportación fue exitosa.
6. Adjunte el archivo guardado a su informe de errores o ticket de soporte.

## Consejos

- Si realizó cambios en la configuración del slice desde que abrió el diálogo, haga clic en `Refresh Snapshot` nuevamente antes de exportar para capturar el estado más reciente.
- Si solo necesita pegar la instantánea en un formulario web o correo electrónico en lugar de adjuntar un archivo, use `Copy JSON` en vez de `Export JSON...`.

## Qué incluye el resumen de problemas

La pestaña **Issue Summary** muestra una lista con viñetas en lenguaje simple de los problemas detectados. A partir de la v0.9.4, el resumen incluye dos entradas adicionales de audio RX remoto:

- **Remote audio RX** — informa el ID de flujo, si se espera un flujo, si la creación está pendiente, si se ha recibido un mensaje de estado, si el flujo pertenece a este cliente y la configuración de compresión en uso.
- **Remote audio route note** — una nota de enrutamiento en texto libre que puede indicar por qué un flujo de audio RX remoto no funciona como se espera.

Cada sección de ruta de audio de slice ahora también incluye una línea **Radio stream route** que informa el ID del flujo de audio RX remoto junto con sus indicadores de esperado, creación pendiente, eliminación solicitada, estado recibido y propiedad del cliente. Revise estas líneas primero al diagnosticar problemas de audio RX remoto antes de contactar al soporte.

## Solución de problemas

- **La etiqueta de estado no muestra confirmación después de hacer clic en `Export JSON...`** — Es posible que haya cancelado el diálogo de guardar archivo sin elegir una ubicación. Haga clic en `Export JSON...` nuevamente y confirme el guardado.
- **`Export JSON...` no está disponible** — El diálogo requiere una conexión de radio activa. Verifique que AetherSDR esté conectado a la radio antes de abrir el diálogo.
- **Los campos de audio RX remoto muestran todos marcadores de posición** — AetherSDR aún no ha recibido un mensaje de estado de la radio para ese flujo. Haga clic en `Refresh Snapshot` después de que la radio haya tenido un momento para enviar el estado del flujo, luego revise nuevamente la pestaña **Issue Summary**.

## Relacionados

- [Capturar una instantánea del slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje simple de problemas detectados en el slice](read-a-plain-language-list-of-suspected-slice-problems.md)
