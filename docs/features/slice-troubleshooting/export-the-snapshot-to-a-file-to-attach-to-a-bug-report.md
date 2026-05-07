# Exportar la instantánea a un archivo para adjuntar a un informe de error

Use esta página para guardar la instantánea JSON del diálogo Solución de problemas del slice en un archivo en disco, de modo que pueda adjuntarlo a una solicitud de soporte o a un informe de error.

## Antes de empezar

- AetherSDR debe estar conectado a una radio. El diálogo Solución de problemas del slice requiere una conexión activa con la radio.
- Abra el diálogo Solución de problemas del slice mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Abra el diálogo Solución de problemas del slice: `Help > Slice Troubleshooting...`
2. Haga clic en `Refresh Snapshot` para asegurarse de que la instantánea refleje el estado actual del slice.
3. Haga clic en `Export JSON...`.
4. En el diálogo de guardado de archivo que aparece, seleccione una carpeta de destino y un nombre de archivo, luego confirme el guardado.
5. Verifique la etiqueta de estado en la parte inferior del diálogo para confirmar que la exportación se realizó correctamente.
6. Adjunte el archivo guardado a su informe de error o ticket de soporte.

## Consejos

- Si ha realizado cambios en la configuración del slice desde que abrió el diálogo, haga clic en `Refresh Snapshot` nuevamente antes de exportar para capturar el estado más reciente.
- Si solo necesita pegar la instantánea en un formulario web o correo electrónico en lugar de adjuntar un archivo, use `Copy JSON` en lugar de `Export JSON...`.

## Qué incluye el Resumen del problema

La pestaña **Issue Summary** muestra una lista con viñetas en lenguaje sencillo de los problemas detectados. A partir de la versión v0.9.4, el resumen incluye dos entradas adicionales de audio RX remoto:

- **Remote audio RX** — informa el ID del flujo, si se espera un flujo, si la creación está pendiente, si se ha visto un mensaje de estado, si el flujo pertenece a este cliente y la configuración de compresión en uso.
- **Remote audio route note** — una nota de ruteo en texto libre que puede indicar por qué un flujo de audio RX remoto no funciona como se espera.

Cada sección de ruta de audio del slice ahora también incluye una línea **Radio stream route** que informa el ID del flujo de audio RX remoto junto con sus indicadores de esperado, creación pendiente, eliminación solicitada, estado visto y propiedad nuestra. Revise estas líneas primero al diagnosticar problemas de audio RX remoto antes de contactar al soporte.

## Solución de problemas

- **La etiqueta de estado no muestra confirmación después de hacer clic en `Export JSON...`** — Es posible que haya cancelado el diálogo de guardado de archivo sin seleccionar una ubicación. Haga clic en `Export JSON...` nuevamente y confirme el guardado.
- **`Export JSON...` no está disponible** — El diálogo requiere una conexión activa con la radio. Verifique que AetherSDR esté conectado a la radio antes de abrir el diálogo.
- **Los campos de audio RX remoto muestran todos marcadores de posición** — AetherSDR aún no ha recibido un mensaje de estado de la radio para ese flujo. Haga clic en `Refresh Snapshot` después de que la radio haya tenido un momento para enviar el estado del flujo, luego revise la pestaña **Issue Summary** nuevamente.

## Relacionado

- [Capture a slice snapshot for support](capture-a-slice-snapshot-for-support.md)
- [Copy the full JSON snapshot to the clipboard](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Refresh the snapshot after changing slice state](refresh-the-snapshot-after-changing-slice-state.md)
- [Read a plain-language list of suspected slice problems](read-a-plain-language-list-of-suspected-slice-problems.md)
