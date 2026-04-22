# Limpiar el registro antes de reproducir un error

Limpiar el registro antes de provocar un error garantiza que el archivo de registro resultante contenga únicamente los eventos relacionados con ese error, lo que facilita su diagnóstico y reporte.

## Antes de comenzar

- Abra AetherSDR. No se requiere conexión a una radio para esta tarea.
- Conozca los pasos necesarios para reproducir el error, de modo que pueda provocarlo inmediatamente después de limpiar el registro.

## Pasos

1. Haga clic en `Help > Support...` para abrir el diálogo Support & Diagnostics.
2. Haga clic en `Clear Log`. Esto trunca el archivo de registro actual de inmediato — no aparece ningún mensaje de confirmación.
3. Verifique que el visor de registro esté vacío y luego reproduzca el error.
4. Haga clic en `Refresh` para recargar el archivo de registro y confirme que las nuevas entradas han sido capturadas.
5. Haga clic en `Open Log Folder` si necesita adjuntar el archivo de registro a un reporte de error.

## Consejos

- Active el registro detallado para el subsistema correspondiente antes de limpiar, de modo que la ejecución de reproducción capture información detallada. Use las casillas de categoría o haga clic en `Enable All` para activar todas las categorías de registro a la vez.
- Limpie el registro y reproduzca el error en una secuencia continua e ininterrumpida. Cualquier reinicio de AetherSDR entre la limpieza y la reproducción puede agregar entradas de inicio no relacionadas.

## Relacionados

- [Activar el registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Ver el registro en tiempo real sin salir de la aplicación](view-the-live-log-without-leaving-the-app.md)
- [Abrir la carpeta de registros para obtener múltiples archivos](open-the-log-folder-to-grab-multiple-files.md)
- [Presentar un reporte de error asistido por IA](file-an-ai-assisted-bug-report.md)
