# Activar el registro detallado para un subsistema específico

El cuadro de diálogo Support & Diagnostics permite activar el registro para subsistemas individuales. Active únicamente las categorías que necesite para mantener la salida del registro enfocada y más fácil de leer al diagnosticar un problema.

## Antes de comenzar

- No se requiere conexión con la radio para cambiar las categorías de registro.
- Si desea un registro limpio que comience en el momento en que reproduce un error, borre el registro primero antes de activar las categorías.

## Pasos

1. Haga clic en `Help > Support...` para abrir el cuadro de diálogo Support & Diagnostics.
2. En el grupo **Diagnostic Logging**, busque la fila con casilla de verificación correspondiente al subsistema que desea diagnosticar.
3. Marque la casilla junto a la etiqueta de esa categoría para activar su registro. Desmarque la casilla para desactivarlo.
4. Reproduzca el comportamiento que está investigando. La salida del registro comienza de inmediato cuando se activa una categoría.
5. Haga clic en **Refresh** para recargar el archivo de registro y ver las entradas más recientes en el visor de registro.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Casillas de categoría | Casilla de verificación | Una fila por cada categoría de registro. Marque para activar, desmarque para desactivar. Los cambios surten efecto de inmediato. |
| Enable All | Botón | Activa todas las categorías de registro a la vez. |
| Disable All | Botón | Desactiva todas las categorías de registro a la vez. |
| Visor de registro | Área de texto | Vista desplazable del texto de registro más reciente. Muestra hasta 2000 líneas. |
| Refresh | Botón | Recarga el archivo de registro en el visor de registro. |
| Etiqueta de ruta del registro | Indicador | Muestra la ruta completa del archivo de registro actual. |
| Tamaño del archivo de registro | Indicador | Muestra el tamaño actual del archivo de registro activo. |

## Consejos

- Use **Enable All** solo cuando no esté seguro de qué subsistema está involucrado. El registro será de gran tamaño. Para una investigación específica, active únicamente la casilla de la categoría relevante.
- Use **Disable All** después de haber capturado lo que necesita para detener el crecimiento adicional del registro.
- El visor de registro muestra un máximo de 2000 líneas. Si necesita el archivo completo, haga clic en **Open Log Folder** para acceder a él directamente en su explorador de archivos.

## Relacionados

- [Borrar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Ver el registro en vivo sin salir de la aplicación](view-the-live-log-without-leaving-the-app.md)
- [Abrir la carpeta de registros para obtener múltiples archivos](open-the-log-folder-to-grab-multiple-files.md)
- [Presentar un informe de error asistido por IA](file-an-ai-assisted-bug-report.md)
