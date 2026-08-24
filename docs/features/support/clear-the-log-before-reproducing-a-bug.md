# Borre el registro antes de reproducir un error

Borrar el registro antes de desencadenar un problema garantiza que el archivo de registro contenga únicamente la sesión relevante, lo que facilita aislar y reportar el problema.

## Antes de comenzar

- Abra AetherSDR. No se requiere una conexión de radio para este procedimiento.
- Si desea capturar una salida detallada durante la reproducción, habilite primero las categorías de registro correspondientes. Consulte [Habilitar registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md).

## Pasos

1. Haga clic en `Help > Support & Diagnostics` para abrir el diálogo Support & Diagnostics.
2. Haga clic en `Clear Log`.
3. Confirme que el visor de registro ahora esté vacío.
4. Cierre el diálogo o déjelo abierto y, luego, realice las acciones que desencadenan el error.
5. Vuelva a `Help > Support & Diagnostics` y haga clic en `Refresh` para recargar el archivo de registro.
6. Revise el visor de registro para confirmar que se capturó la salida relevante.
7. Haga clic en `Open Log Folder` para acceder al archivo de registro en el explorador de archivos de su sistema operativo si necesita adjuntarlo a un informe.

## Consejos

- Haga clic en `Refresh` después de reproducir el error antes de leer el registro. El visor de registro no se actualiza automáticamente.
- Si tiene previsto presentar un informe inmediatamente después de capturar el registro, haga clic en `Help > File an Issue` para iniciar el flujo de informe de errores asistido por IA. Consulte [Presentar un informe de errores asistido por IA](file-an-ai-assisted-bug-report.md).

## Solución de problemas

- **El visor de registro sigue mostrando entradas antiguas después de hacer clic en `Clear Log`** — Haga clic en `Refresh` para recargar el archivo truncado. El visor no limpia su pantalla automáticamente al truncarse.

## Relacionados

- [Habilitar registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Ver el registro en vivo sin salir de la aplicación](view-the-live-log-without-leaving-the-app.md)
- [Presentar un informe de errores asistido por IA](file-an-ai-assisted-bug-report.md)
- [Abrir la carpeta de registro para obtener múltiples archivos](open-the-log-folder-to-grab-multiple-files.md)
