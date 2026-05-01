# Exportar la snapshot a un archivo para adjuntar a un informe de fallo

Utilice esta página para guardar la snapshot JSON del diálogo Slice Troubleshooting en un archivo en disco, de modo que pueda adjuntarlo a una solicitud de soporte o informe de fallo.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo Slice Troubleshooting requiere una conexión activa con la radio.
- Abra el diálogo Slice Troubleshooting mediante `Help > Slice Troubleshooting...` si no está ya abierto.

## Pasos

1. Abra el diálogo Slice Troubleshooting: `Help > Slice Troubleshooting...`
2. Haga clic en `Refresh Snapshot` para asegurar que la snapshot refleje el estado actual de la slice.
3. Haga clic en `Export JSON...`.
4. En el diálogo de guardado de archivo que aparece, elija una carpeta de destino y nombre de archivo, luego confirme el guardado.
5. Compruebe la etiqueta de estado en la parte inferior del diálogo para confirmar que la exportación fue exitosa.
6. Adjunte el archivo guardado a su informe de fallo o ticket de soporte.

## Consejos

- Si ha realizado cambios en la configuración de la slice desde que abrió el diálogo, haga clic en `Refresh Snapshot` nuevamente antes de exportar para capturar el estado más reciente.
- Si solo necesita pegar la snapshot en un formulario web o correo electrónico en lugar de adjuntar un archivo, use `Copy JSON` en lugar de `Export JSON...`.

## Lo que incluye el Resumen de problemas

La pestaña **Issue Summary** muestra una lista con viñetas en lenguaje natural de los problemas detectados. A partir de v0.9.4, el resumen incluye dos entradas adicionales de RX de audio remoto:

- **Remote audio RX** — reporta el ID de stream, si se espera un stream, si la creación está pendiente, si se ha visto un mensaje de estado, si el stream es propiedad de este cliente, y la configuración de compresión en uso.
- **Remote audio route note** — una nota de enrutamiento de texto libre que puede indicar por qué un stream de RX de audio remoto no está funcionando como se esperaba.

Cada sección de ruta de audio de slice también incluye ahora una línea **Radio stream route** que reporta el ID de stream de RX de audio remoto junto con sus indicadores expected, create-pending, remove-requested, status-seen y owned-by-us. Revise estas líneas primero al diagnosticar problemas de RX de audio remoto antes de contactar al soporte.

## Solución de problemas

- **La etiqueta de estado no muestra confirmación después de hacer clic en `Export JSON...`** — Es posible que haya cancelado el diálogo de guardado de archivo sin elegir una ubicación. Haga clic en `Export JSON...` nuevamente y confirme el guardado.
- **`Export JSON...` no está disponible** — El diálogo requiere una conexión activa con la radio. Verifique que AetherSDR esté conectado a la radio antes de abrir el diálogo.
- **Los campos de RX de audio remoto muestran todos placeholders** — AetherSDR aún no ha recibido un mensaje de estado de la radio para ese stream. Haga clic en `Refresh Snapshot` después de dar a la radio un momento para enviar el estado del stream, luego compruebe la pestaña **Issue Summary** nuevamente.

## Relacionado

- [Capturar una snapshot de slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Copiar la snapshot JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Actualizar la snapshot después de cambiar el estado de la slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje natural de problemas sospechosos de la slice](read-a-plain-language-list-of-suspected-slice-problems.md)
