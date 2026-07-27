# Ver el registro en vivo sin salir de la aplicación

El cuadro de diálogo de Soporte y diagnóstico incluye un visor de registros desplazable que le permite leer la salida de registros recientes sin abrir un administrador de archivos o terminal. Úselo cuando desee observar lo que AetherSDR está haciendo en tiempo real o detectar rápidamente un error después de que ocurra algo inesperado.

## Antes de comenzar

- No se requiere conexión de radio para abrir el cuadro de diálogo ni leer el registro.
- Si desea capturar la salida para un evento específico, considere limpiar el registro primero para que solo aparezcan las entradas relevantes.

## Pasos

1. Haga clic en `Help > Support...` para abrir el cuadro de diálogo Soporte y diagnóstico.
2. Busque el panel **Log viewer** en el centro del cuadro de diálogo. Muestra el texto del registro más reciente como una vista desplazable y de solo lectura.
3. Desplácese por el visor de registros para leer las entradas actuales. La ruta del registro se muestra en la etiqueta **Log path label** sobre el visor, y el tamaño actual del archivo aparece a la derecha de la misma.
4. Si ha ocurrido nueva actividad desde que abrió el cuadro de diálogo, haga clic en **Refresh** para recargar el archivo de registro y mostrar las últimas entradas.
5. Para gestionar qué categorías de registro aparecen, use las **Category checkboxes** en la sección **Diagnostic Logging** en la parte superior. Haga clic en **Enable All** para activar todas las categorías, o **Disable All** para silenciarlas todas.
6. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Category checkboxes | Casilla de verificación | Activar/desactivar registro por categoría, una fila por categoría. |
| Enable All | Botón | Activa todas las categorías de registro. |
| Disable All | Botón | Desactiva todas las categorías de registro. |
| Log path label | Indicador | Muestra la ruta completa al archivo de registro actual. |
| Log file size | Indicador | Muestra el tamaño actual del archivo de registro activo. |
| Log viewer | Campo de texto | Vista desplazable y de solo lectura del texto de registro más reciente. Muestra hasta 2000 líneas. |
| Refresh | Botón | Recarga el archivo de registro en el visor. |
| Clear Log | Botón | Trunca el archivo de registro actual. |
| Open Log Folder | Botón | Abre el directorio de registros en el explorador de archivos del sistema operativo. |
| Reset Settings | Botón | Restablece la configuración de AetherSDR a los valores predeterminados (con confirmación). Elimina la configuración local y la caché de sabiduría NR2. La configuración de la radio permanece en la radio. |
| File an Issue | Botón | Inicia el flujo de Informe de errores asistido por IA. Consulte la sección **File an Issue** a continuación. |
| Close | Botón | Cierra el cuadro de diálogo. |

## File an Issue

El botón **File an Issue** inicia un proceso de Informe de errores asistido por IA.

1. Haga clic en **File an Issue**.
2. En el cuadro de diálogo que aparece, describa el problema que está experimentando.
3. Haga clic en uno de los botones de servicio de IA proporcionados para abrir la herramienta de IA con un mensaje previamente rellenado que incluye su información del sistema y la descripción del error.
4. La IA generará un informe de error completo de GitHub. Siga las instrucciones de la IA para enviarlo en `https://github.com/aethersdr/AetherSDR/issues/new`.

## Consejos

- El visor de registros tiene un máximo de 2000 líneas. Si el archivo de registro es grande, solo se muestra el contenido más reciente. Haga clic en **Open Log Folder** para acceder al archivo completo.
- Para controlar qué categorías aparecen en el registro, use las casillas de categoría en la sección **Diagnostic Logging** en la parte superior del cuadro de diálogo. Haga clic en **Enable All** para activar todas las categorías, o **Disable All** para silenciarlas todas.
- El cuadro de diálogo recuerda su posición y tamaño entre sesiones.

## Relacionado

- [Enable verbose logging for a specific subsystem](enable-verbose-logging-for-a-specific-subsystem.md)
- [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md)
- [Open the log folder to grab multiple files](open-the-log-folder-to-grab-multiple-files.md)
