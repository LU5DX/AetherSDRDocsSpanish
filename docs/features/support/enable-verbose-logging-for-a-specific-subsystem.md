# Habilitar el registro detallado para un subsistema específico

El cuadro de diálogo Support & Diagnostics le permite activar el registro para subsistemas individuales. Active solo las categorías que necesite para mantener la salida del registro enfocada y más fácil de leer al diagnosticar un problema.

## Antes de comenzar

- No se requiere conexión de radio para cambiar las categorías de registro.
- Si desea un registro limpio que comience en el momento en que reproduzca un error, borre el registro primero antes de habilitar categorías.

## Pasos

1. Haga clic en `Help > Support...` para abrir el cuadro de diálogo Support & Diagnostics.
2. En el grupo **Diagnostic Logging**, busque la fila de casillas de verificación para el subsistema que desea diagnosticar.
3. Marque la casilla junto a la etiqueta de esa categoría para habilitar el registro. Desmárquela para deshabilitarlo.
4. Reproduzca el comportamiento que está investigando. La salida del registro comienza inmediatamente cuando se habilita una categoría.
5. Haga clic en **Refresh** para recargar el archivo de registro y ver las últimas entradas en el visor de registro.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Casillas de verificación de categoría | Casilla de verificación | Una fila por categoría de registro. Marque para habilitar, desmarque para deshabilitar. Los cambios surten efecto de inmediato. |
| Enable All | Botón | Activa todas las categorías de registro a la vez. |
| Disable All | Botón | Desactiva todas las categorías de registro a la vez. |
| Visor de registro | Área de texto | Vista desplazable del texto de registro más reciente. Muestra hasta 2000 líneas. |
| Refresh | Botón | Recarga el archivo de registro en el visor de registro. |
| Clear Log | Botón | Trunca el archivo de registro actual. |
| Open Log Folder | Botón | Abre el directorio de registro en el explorador de archivos del sistema operativo. |
| Etiqueta de ruta de registro | Indicador | Muestra la ruta completa del archivo de registro actual. |
| Tamaño del archivo de registro | Indicador | Muestra el tamaño actual del archivo de registro activo. |
| Reset Settings | Botón | Restablece la configuración de AetherSDR a los valores predeterminados (con confirmación). |
| File an Issue | Botón | Inicia el flujo de Informe de errores asistido por IA. |
| Close | Botón | Cierra el cuadro de diálogo. |

## Consejos

- Use **Enable All** solo cuando no esté seguro de qué subsistema está involucrado. El registro será grande. Para una investigación específica, active solo la casilla de verificación de la categoría relevante.
- Use **Disable All** después de haber capturado lo que necesita para detener el crecimiento adicional del registro.
- El visor de registro muestra un máximo de 2000 líneas. Si necesita el archivo completo, haga clic en **Open Log Folder** para acceder a él directamente en su explorador de archivos.

## Relacionado

- [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md)
- [View the live log without leaving the app](view-the-live-log-without-leaving-the-app.md)
- [Open the log folder to grab multiple files](open-the-log-folder-to-grab-multiple-files.md)
- [File an AI-assisted bug report](file-an-ai-assisted-bug-report.md)
- [Reset settings to defaults](reset-settings-to-defaults.md)
