# Ver el registro en vivo sin salir de la aplicación

El cuadro de diálogo Support & Diagnostics incluye un visor de registro con desplazamiento que le permite leer la salida reciente del registro sin abrir un administrador de archivos ni una terminal. Úselo cuando desee observar lo que AetherSDR está haciendo en tiempo real o identificar rápidamente un error después de que ocurra algo inesperado.

## Antes de comenzar

- No se requiere conexión de radio para abrir el cuadro de diálogo ni para leer el registro.
- Si desea capturar la salida de un evento específico, considere borrar el registro primero para que solo aparezcan las entradas relevantes.

## Pasos

1. Haga clic en `Help > Support...` para abrir el cuadro de diálogo Support & Diagnostics.
2. Ubique el panel **Log viewer** en el centro del cuadro de diálogo. Muestra el texto más reciente del registro en una vista de solo lectura con desplazamiento.
3. Desplácese por el **Log viewer** para leer las entradas actuales. La ruta del registro se muestra en la etiqueta **Log path label** sobre el visor, y el tamaño actual del archivo aparece a su derecha.
4. Si se ha producido nueva actividad desde que abrió el cuadro de diálogo, haga clic en **Refresh** para recargar el archivo de registro y mostrar las entradas más recientes.
5. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Log path label | Indicador | Muestra la ruta completa al archivo de registro actual. |
| Log file size | Indicador | Muestra el tamaño actual del archivo de registro activo. |
| Log viewer | Campo de texto | Vista de solo lectura con desplazamiento del texto más reciente del registro. Muestra hasta 2000 líneas. |
| Refresh | Botón | Recarga el archivo de registro en el visor. |
| Clear Log | Botón | Trunca el archivo de registro actual. |
| Open Log Folder | Botón | Abre el directorio de registros en el explorador de archivos del sistema operativo. |

## Consejos

- El **Log viewer** admite un máximo de 2000 líneas. Si el archivo de registro es grande, solo se muestra el contenido más reciente. Haga clic en **Open Log Folder** para acceder al archivo completo.
- Para controlar qué categorías aparecen en el registro, utilice las casillas de verificación de categoría en la sección **Diagnostic Logging** en la parte superior del cuadro de diálogo. Haga clic en **Enable All** para activar todas las categorías, o en **Disable All** para silenciarlas todas.

## Relacionados

- [Habilitar el registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Borrar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Abrir la carpeta de registros para obtener múltiples archivos](open-the-log-folder-to-grab-multiple-files.md)
