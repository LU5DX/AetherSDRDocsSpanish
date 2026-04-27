# Exportar el snapshot a un archivo para adjuntar a un informe de error

Use esta página para guardar el snapshot JSON del diálogo Slice Troubleshooting en un archivo en disco, de modo que pueda adjuntarlo a una solicitud de soporte o a un informe de error.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo Slice Troubleshooting requiere una conexión de radio activa.
- Abra el diálogo Slice Troubleshooting mediante `Help > Slice Troubleshooting...` si aún no está abierto.

## Pasos

1. Abra el diálogo Slice Troubleshooting: `Help > Slice Troubleshooting...`
2. Haga clic en `Refresh Snapshot` para asegurarse de que el snapshot refleje el estado actual del slice.
3. Haga clic en `Export JSON...`.
4. En el diálogo de guardar archivo que aparece, elija una carpeta de destino y un nombre de archivo, luego confirme el guardado.
5. Revise la etiqueta de estado en la parte inferior del diálogo para confirmar que la exportación fue exitosa.
6. Adjunte el archivo guardado a su informe de error o ticket de soporte.

## Consejos

- Si realizó cambios en la configuración del slice desde que abrió el diálogo, haga clic en `Refresh Snapshot` nuevamente antes de exportar para capturar el estado más reciente.
- Si solo necesita pegar el snapshot en un formulario web o correo electrónico en lugar de adjuntar un archivo, use `Copy JSON` en vez de `Export JSON...`.

## Resolución de problemas

- **La etiqueta de estado no muestra confirmación después de hacer clic en `Export JSON...`** — Es posible que haya cancelado el diálogo de guardar archivo sin elegir una ubicación. Haga clic en `Export JSON...` nuevamente y confirme el guardado.
- **`Export JSON...` no está disponible** — El diálogo requiere una conexión de radio activa. Verifique que AetherSDR esté conectado a la radio antes de abrir el diálogo.

## Relacionado

- [Capturar un snapshot del slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Copiar el snapshot JSON completo al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Actualizar el snapshot después de cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje sencillo de posibles problemas del slice](read-a-plain-language-list-of-suspected-slice-problems.md)
