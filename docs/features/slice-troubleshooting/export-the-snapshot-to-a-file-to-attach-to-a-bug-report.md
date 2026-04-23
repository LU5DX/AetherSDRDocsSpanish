# Exportar el snapshot a un archivo para adjuntarlo a un reporte de error

Guarde el snapshot actual de diagnóstico del slice (instantánea del estado del slice) como un archivo JSON para adjuntarlo a un issue de GitHub o a una solicitud de soporte.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo requiere una conexión de radio activa.
- Abra el diálogo Slice Troubleshooting mediante `Help > Slice Troubleshooting...`.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en la pestaña `JSON` para confirmar que el snapshot contiene datos.
3. Si el snapshot está desactualizado, haga clic en `Refresh Snapshot` para releer el estado actual del slice.
4. Haga clic en `Export JSON...`.
5. En el diálogo de archivo, confirme o cambie el nombre del archivo y el destino. El nombre de archivo predeterminado es `aethersdr-slice-troubleshooting-YYYYMMDD-HHmmss.json` en su directorio de inicio.
6. Haga clic en Save.
7. Revise la etiqueta de estado en la parte inferior del diálogo. Una exportación exitosa no muestra ningún error. Si el archivo no pudo escribirse, la etiqueta de estado muestra `Unable to write '<path>'`.
8. Adjunte el archivo `.json` guardado a su reporte de error.

## Consejos

- El nombre de archivo predeterminado incluye una marca de tiempo, por lo que las exportaciones repetidas no se sobreescriben entre sí.
- Si solo necesita el texto y no desea un archivo, use `Copy JSON` para colocar el snapshot en el portapapeles.

## Solución de problemas

- **La etiqueta de estado muestra `Unable to write '<path>'`** — La ruta seleccionada no tiene permisos de escritura. Seleccione un directorio donde tenga permiso de escritura, como su directorio de inicio o el Escritorio.
- **El snapshot parece desactualizado** — Haga clic en `Refresh Snapshot` antes de hacer clic en `Export JSON...`. El diálogo no vuelve a consultar la radio automáticamente después de abrirse.

## Relacionados

- [Descripción general de Slice Troubleshooting](overview.md)
- [Actualizar el snapshot después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Copiar el snapshot JSON completo al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Capturar un snapshot del slice para soporte](capture-a-slice-snapshot-for-support.md)
