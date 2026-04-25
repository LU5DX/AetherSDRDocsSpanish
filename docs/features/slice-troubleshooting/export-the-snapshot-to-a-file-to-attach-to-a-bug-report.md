# Exportar la instantánea a un archivo para adjuntar a un informe de error

Guarde la instantánea (snapshot) actual del slice como archivo JSON para adjuntarla a un issue de GitHub o a una solicitud de soporte.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El diálogo requiere una conexión de radio activa.
- Abra el diálogo Slice Troubleshooting mediante `Help > Slice Troubleshooting...`.

## Pasos

1. Haga clic en `Help > Slice Troubleshooting...` para abrir el diálogo Slice Troubleshooting.
2. Haga clic en `Refresh Snapshot` para asegurarse de que la instantánea refleje el estado actual de la radio.
3. Haga clic en `Export JSON...`.
4. En el diálogo de guardado de archivo que aparece, elija una carpeta de destino y un nombre de archivo, luego confirme el guardado.
5. Adjunte el archivo guardado a su informe de error o issue de GitHub.

La etiqueta de estado en la parte inferior del diálogo confirma el resultado de la exportación.

## Consejos

- Si acaba de cambiar la configuración del slice (modo, antena, estado de silencio), haga clic en `Refresh Snapshot` antes de exportar para que el archivo refleje el estado más reciente.
- La pestaña `JSON (tab)` muestra exactamente lo que se guardará. Revísela antes de exportar si desea confirmar el contenido de la instantánea.
- Si solo necesita pegar los datos en lugar de adjuntar un archivo, use `Copy JSON` en su lugar.

## Relacionado

- [Capturar una instantánea del slice para soporte](capture-a-slice-snapshot-for-support.md)
- [Copiar la instantánea JSON completa al portapapeles](copy-the-full-json-snapshot-to-the-clipboard.md)
- [Actualizar la instantánea tras cambiar el estado del slice](refresh-the-snapshot-after-changing-slice-state.md)
- [Leer una lista en lenguaje sencillo de los problemas sospechados del slice](read-a-plain-language-list-of-suspected-slice-problems.md)
