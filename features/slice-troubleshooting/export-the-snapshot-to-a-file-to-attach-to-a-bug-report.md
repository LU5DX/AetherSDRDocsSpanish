# Exportar la instantánea a un archivo para adjuntar a un reporte de error

Guarde la instantánea de diagnóstico del slice (receptor virtual) actual como un archivo JSON en disco para adjuntarlo a un issue de GitHub o a una solicitud de soporte.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo requiere una conexión activa con el radio.
- Abra el diálogo de diagnóstico del slice mediante `Help > Slice Troubleshooting...`.

## Pasos

1. Abra `Help > Slice Troubleshooting...`.
2. Haga clic en `JSON` para confirmar que la instantánea contiene datos actuales. Si el estado parece desactualizado, haga clic primero en `Refresh Snapshot`.
3. Haga clic en `Export JSON...`.
4. En el diálogo de guardar archivo, elija una carpeta de destino y confirme o edite el nombre del archivo. El nombre predeterminado es `aethersdr-slice-troubleshooting-YYYYMMDD-HHmmss.json`, ubicado en su directorio de inicio.
5. Haga clic en Save.
6. Revise la etiqueta de estado en la parte inferior del diálogo. Si la exportación fue exitosa, la etiqueta muestra el resultado. Si la escritura falló, la etiqueta muestra `Unable to write` seguido de la ruta — verifique que la carpeta de destino exista y que usted tenga permiso de escritura, luego intente de nuevo.

## Consejos

- El nombre de archivo predeterminado incluye una marca de tiempo, por lo que exportar múltiples instantáneas antes y después de un cambio de configuración no sobreescribirá los archivos anteriores.
- Si no puede adjuntar un archivo JSON directamente (por ejemplo, en un foro que bloquea archivos `.json`), use `Copy JSON` en su lugar y pegue el texto en un bloque de código en su reporte.

## Solución de problemas

- **La etiqueta de estado muestra "Unable to write `<path>`"** — No fue posible crear el archivo. Verifique que la carpeta de destino exista y que su cuenta de usuario tenga permiso de escritura en ella. Intente guardar en su directorio de inicio.

## Relacionados

- [Capturar una instantánea del slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Actualizar la instantánea después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
