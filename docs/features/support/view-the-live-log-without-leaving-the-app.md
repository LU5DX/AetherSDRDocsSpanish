# Vea el registro en vivo sin salir de la aplicación

El diálogo **Support & Diagnostics** incluye un visor de registro desplazable que le permite leer la salida de registro reciente sin abrir un administrador de archivos o una terminal. Úselo cuando quiera observar lo que AetherSDR está haciendo en tiempo real o detectar rápidamente un error después de que algo inesperado ocurra.

## Antes de comenzar

- No se requiere conexión de radio para abrir el diálogo o leer el registro.
- Si desea capturar la salida para un evento específico, considere limpiar el registro primero para que solo aparezcan las entradas relevantes.

## Pasos

1. Abra el menú **Help**.
2. Seleccione **File an Issue** solo si desea reportar un error; el diálogo en sí se abre mediante **Support...**.
3. En el diálogo **Support & Diagnostics**, busque el panel **Log viewer** en el centro. Muestra el texto de registro más reciente como una vista desplazable y de solo lectura.
4. Desplácese por el visor de registro para leer las entradas actuales. La ruta del registro se muestra en el **Log path label** sobre el visor, y el tamaño actual del archivo aparece a la derecha del mismo.
5. Si ha habido actividad nueva desde que abrió el diálogo, haga clic en **Refresh** para recargar el archivo de registro y mostrar las entradas más recientes.
6. Para gestionar qué categorías de registro aparecen, use las **Category checkboxes** en la sección **Diagnostic Logging** en la parte superior. Haga clic en **Enable All** para activar todas las categorías, o en **Disable All** para silenciarlas todas.
7. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Control                               | Tipo          | Comportamiento                                                                                                                          |
|---------------------------------------|---------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| Category checkboxes                   | Casilla de verificación | Habilitación/deshabilitación de registro por categoría, una fila por categoría.                                                          |
| Enable All                            | Botón         | Activa todas las categorías de registro.                                                                                                |
| Disable All                           | Botón         | Desactiva todas las categorías de registro.                                                                                             |
| Log path label                        | Indicador     | Muestra la ruta completa al archivo de registro actual.                                                                                 |
| Log file size                         | Indicador     | Muestra el tamaño actual del archivo de registro activo.                                                                                |
| Log viewer                            | Campo de texto | Vista desplazable y de solo lectura del texto de registro más reciente. Muestra hasta 2000 líneas.                                      |
| Refresh                               | Botón         | Recarga el archivo de registro en el visor.                                                                                             |
| Clear Log                             | Botón         | Trunca el archivo de registro actual.                                                                                                   |
| Open Log Folder                       | Botón         | Abre el directorio de registro en el explorador de archivos del sistema operativo.                                                      |
| Close                                 | Botón         | Cierra el diálogo.                                                                                                                      |
| Instructions (report-an-issue how-to) | Texto enriquecido | Indica al usuario que use **Help > File an Issue** para reportar errores una vez que las categorías de registro relevantes hayan sido habilitadas y el problema haya sido reproducido. |

> **Nota (v26.8.4):** Los botones **Reset Settings** y **File an Issue** fueron eliminados de este diálogo en v26.8.4. Ambas acciones ahora se encuentran directamente en el menú **Help**.

## File an Issue

La entrada **File an Issue** en el menú **Help** inicia un proceso de reporte de errores asistido por IA.

1. Haga clic en **Help > File an Issue**.
2. En el diálogo que aparece, describa el problema que está experimentando.
3. Haga clic en uno de los botones de servicio de IA proporcionados para abrir la herramienta de IA con un mensaje precargado que incluye su información del sistema y la descripción del error.
4. La IA generará un reporte de error completo de GitHub. Siga las instrucciones de la IA para enviarlo en `https://github.com/aethersdr/AetherSDR/issues/new`.

## Reset Settings

La entrada **Reset Settings** en el menú **Help** elimina solo los ajustes específicos de la aplicación de AetherSDR. No cambia los ajustes almacenados en la radio.

1. Haga clic en **Help > Reset Settings**.
2. Aparece un diálogo de confirmación que lista los archivos que se eliminarán. Antes de eliminar cualquier cosa, se escribe una copia de seguridad de los ajustes actuales en el directorio de copias de seguridad (mostrado en el mensaje).
3. Haga clic en **Yes** para continuar. AetherSDR se cerrará inmediatamente después del restablecimiento para que los archivos de ajustes no se vuelvan a crear.

## Consejos

- El visor de registro admite un máximo de 2000 líneas. Si el archivo de registro es grande, solo se muestra el contenido más reciente. Haga clic en **Open Log Folder** para acceder al archivo completo.
- Para controlar qué categorías aparecen en el registro, use las casillas de categoría en la sección **Diagnostic Logging** en la parte superior del diálogo. Haga clic en **Enable All** para activar todas las categorías, o en **Disable All** para silenciarlas todas.
- El diálogo recuerda su posición y tamaño entre sesiones.

## Relacionado

- [Habilitar registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Abrir la carpeta de registro para tomar varios archivos](open-the-log-folder-to-grab-multiple-files.md)
