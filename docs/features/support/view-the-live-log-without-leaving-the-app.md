# Ver el Registro en Vivo Sin Salir de la Aplicación

El cuadro de diálogo Support & Diagnostics incluye un visor de registro desplazable que le permite leer las salidas de registro recientes sin abrir un administrador de archivos o terminal. Úselo cuando desee observar lo que AetherSDR está haciendo en tiempo real o detectar rápidamente un error después de que ocurra algo inesperado.

## Antes de empezar

- No se requiere ninguna conexión de radio para abrir el cuadro de diálogo o leer el registro.
- Si desea capturar la salida para un evento específico, considere borrar el registro primero para que solo aparezcan las entradas relevantes.

## Pasos

1. Haga clic en `Help > Support...` para abrir el cuadro de diálogo Support & Diagnostics.
2. Busque el panel **Log viewer** en el centro del cuadro de diálogo. Muestra el texto de registro más reciente como una vista desplazable y de solo lectura.
3. Desplácese por el visor de registro para leer las entradas actuales. La ruta del registro se muestra en la **Log path label** sobre el visor, y el tamaño actual del archivo aparece a la derecha de esta.
4. Si ha ocurrido nueva actividad desde que abrió el cuadro de diálogo, haga clic en **Refresh** para recargar el archivo de registro y mostrar las entradas más recientes.
5. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Log path label | Indicador | Muestra la ruta completa al archivo de registro actual. |
| Log file size | Indicador | Muestra el tamaño actual del archivo de registro activo. |
| Log viewer | Campo de texto | Vista desplazable y de solo lectura del texto de registro más reciente. Muestra hasta 2000 líneas. |
| Refresh | Botón | Recarga el archivo de registro en el visor. |
| Clear Log | Botón | Trunca el archivo de registro actual. |
| Open Log Folder | Botón | Abre el directorio de registro en el explorador de archivos del sistema operativo. |

## Consejos

- El visor de registro tiene un máximo de 2000 líneas. Si el archivo de registro es grande, solo se muestra el contenido más reciente. Haga clic en **Open Log Folder** para acceder al archivo completo.
- Para controlar qué categorías aparecen en el registro, use las casillas de verificación de categorías en la sección **Diagnostic Logging** en la parte superior del cuadro de diálogo. Haga clic en **Enable All** para activar todas las categorías, o en **Disable All** para silenciarlas todas.

## Relacionado

- [Enable verbose logging for a specific subsystem](enable-verbose-logging-for-a-specific-subsystem.md)
- [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md)
- [Open the log folder to grab multiple files](open-the-log-folder-to-grab-multiple-files.md)
