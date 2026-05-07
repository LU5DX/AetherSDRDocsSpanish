# Habilitar el registro verbose para un subsistema específico

El cuadro de diálogo de Soporte y Diagnóstico le permite activar el registro para subsistemas individuales. Active solo las categorías que necesite para mantener la salida del registro enfocada y más fácil de leer al diagnosticar un problema.

## Antes de comenzar

- No se requiere conexión de radio para cambiar las categorías de registro.
- Si desea un registro limpio que comience en el momento en que reproduzca un error, borre primero el registro antes de habilitar las categorías.

## Pasos

1. Haga clic en `Help > Support...` para abrir el cuadro de diálogo de Soporte y Diagnóstico.
2. En el grupo **Diagnostic Logging**, busque la fila de casillas de verificación para el subsistema que desea diagnosticar.
3. Marque la casilla junto a la etiqueta de esa categoría para habilitar el registro. Desmárquela para deshabilitarlo.
4. Reproduzca el comportamiento que está investigando. La salida del registro comienza inmediatamente cuando se activa una categoría.
5. Haga clic en **Refresh** para recargar el archivo de registro y ver las entradas más recientes en el visor de registro.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Casillas de verificación de categoría | Casilla de verificación | Una fila por categoría de registro. Marque para habilitar, desmarque para deshabilitar. Los cambios surten efecto inmediatamente. |
| Enable All | Botón | Activa todas las categorías de registro a la vez. |
| Disable All | Botón | Desactiva todas las categorías de registro a la vez. |
| Log viewer | Área de texto | Vista desplazable del texto de registro más reciente. Muestra hasta 2000 líneas. |
| Refresh | Botón | Recarga el archivo de registro en el visor de registro. |
| Log path label | Indicador | Muestra la ruta completa del archivo de registro actual. |
| Log file size | Indicador | Muestra el tamaño actual del archivo de registro activo. |

## Consejos

- Use **Enable All** solo cuando no esté seguro de qué subsistema está involucrado. El registro será grande. Para una investigación dirigida, active solo la casilla de verificación de la categoría relevante.
- Use **Disable All** después de haber capturado lo que necesita para detener el crecimiento adicional del registro.
- El visor de registro muestra un máximo de 2000 líneas. Si necesita el archivo completo, haga clic en **Open Log Folder** para acceder a él directamente en su explorador de archivos.

## Relacionado

- [Borrar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Ver el registro en vivo sin salir de la aplicación](view-the-live-log-without-leaving-the-app.md)
- [Abrir la carpeta de registro para tomar varios archivos](open-the-log-folder-to-grab-multiple-files.md)
- [Presentar un informe de error asistido por IA](file-an-ai-assisted-bug-report.md)
