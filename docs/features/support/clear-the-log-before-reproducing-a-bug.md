# Limpiar el registro antes de reproducir un error

Limpiar el registro antes de desencadenar un problema asegura que el archivo de registro contenga únicamente la sesión relevante, facilitando el aislamiento y la notificación del problema.

## Antes de comenzar

- Abra AetherSDR. No se requiere una conexión de radio para este procedimiento.
- Si desea capturar una salida detallada durante la reproducción, habilite primero las categorías de registro correspondientes. Consulte [Enable verbose logging for a specific subsystem](enable-verbose-logging-for-a-specific-subsystem.md).

## Pasos

1. Haga clic en `Help > Support...` para abrir el cuadro de diálogo Support & Diagnostics.
2. Haga clic en `Clear Log`.
3. Confirme que el visor de registro ahora está vacío.
4. Cierre el cuadro de diálogo o déjelo abierto, luego realice las acciones que desencadenan el error.
5. Vuelva a `Help > Support...` y haga clic en `Refresh` para recargar el archivo de registro.
6. Revise el visor de registro para confirmar que se capturó la salida relevante.
7. Haga clic en `Open Log Folder` para acceder al archivo de registro en el explorador de archivos de su sistema operativo si necesita adjuntarlo a un informe.

## Consejos

- Haga clic en `Refresh` después de reproducir el error antes de leer el registro. El visor de registro no se actualiza automáticamente.
- Si tiene la intención de presentar un informe inmediatamente después de capturar el registro, haga clic en `File an Issue` para iniciar el flujo de notificación de errores asistido por IA. Consulte [File an AI-assisted bug report](file-an-ai-assisted-bug-report.md).

## Solución de problemas

- **El visor de registro aún muestra entradas antiguas después de hacer clic en `Clear Log`** — Haga clic en `Refresh` para recargar el archivo truncado. El visor no limpia su pantalla automáticamente al truncar el archivo.

## Relacionados

- [Enable verbose logging for a specific subsystem](enable-verbose-logging-for-a-specific-subsystem.md)
- [View the live log without leaving the app](view-the-live-log-without-leaving-the-app.md)
- [File an AI-assisted bug report](file-an-ai-assisted-bug-report.md)
- [Open the log folder to grab multiple files](open-the-log-folder-to-grab-multiple-files.md)
