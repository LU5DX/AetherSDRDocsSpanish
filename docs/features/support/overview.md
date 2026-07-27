# Resumen de Soporte y Diagnóstico

El diálogo de Soporte y Diagnóstico le ofrece un único lugar para controlar el registro de diagnóstico, inspeccionar el registro en vivo y reportar errores. Ábralo desde `Help > Support...`. No se requiere conexión de radio.

## Cómo funciona

El diálogo tiene tres áreas: un panel de control de registro en la parte superior, un visor de registro en el medio y una fila de botones de acción en la parte inferior.

**Panel de Registro de Diagnóstico**

El grupo superior, etiquetado "Diagnostic Logging", enumera cada categoría de registro disponible como una casilla de verificación. Cada casilla habilita o deshabilita los mensajes de ese subsistema mientras AetherSDR se ejecuta. Los cambios surten efecto inmediatamente — no es necesario reiniciar.

**Visor de registro**

Debajo del panel de categorías, un área de texto de solo lectura muestra las entradas de registro más recientes. La ruta del archivo de registro se muestra encima; el tamaño actual del archivo se muestra a la derecha de la misma fila. El visor admite hasta 2000 líneas. Use Refresh para recargar el archivo bajo demanda.

**Botones de acción**

La fila de botones en la parte inferior proporciona los siguientes controles:

| Botón | Qué hace |
|---|---|
| Enable All | Activa todas las categorías de registro a la vez. |
| Disable All | Desactiva todas las categorías de registro a la vez. |
| Refresh | Recarga el archivo de registro en el visor. |
| Clear Log | Trunca el archivo de registro actual. Esta acción no se puede deshacer. |
| Open Log Folder | Abre el directorio de registro en el explorador de archivos de su sistema operativo para que pueda copiar o adjuntar varios archivos. |
| File an Issue | Inicia el flujo de reporte de errores asistido por IA. Recopila un paquete de soporte y luego abre un diálogo que le permite abrir un asistente de IA de su elección. Pegue el mensaje de diagnóstico prellenado en el asistente, describa su problema y luego use la salida de la IA como cuerpo de su issue de GitHub. |
| Close | Cierra el diálogo. |

**Nota:** El botón **Reset Settings** se ha eliminado en esta versión. Para restablecer la configuración de AetherSDR a los valores predeterminados, elimine o renombre el archivo de configuración manualmente. La ubicación depende de su sistema operativo:
- Linux: `~/.config/AetherSDR/AetherSDR.ini`
- macOS: `~/Library/Preferences/com.aethersdr.AetherSDR.plist`
- Windows: `%APPDATA%\AetherSDR\AetherSDR.ini`

La configuración de radio almacenada en el FlexRadio nunca se ve afectada por ningún restablecimiento de configuración local.

**Indicadores**

El diálogo muestra el siguiente indicador:

| Indicador | Qué muestra |
|---|---|
| Log file size | Tamaño actual del archivo de registro activo, mostrado a la derecha de la etiqueta de ruta del registro. |

## Consejos

- Habilite solo las categorías relevantes para el problema que está investigando para mantener el registro legible.
- Haga clic en Clear Log inmediatamente antes de reproducir un error para que el registro contenga solo la secuencia relevante de eventos.
- Si usa File an Issue, el mensaje de diagnóstico se prellena con la información de su sistema y se crea un paquete de soporte automáticamente. Péguelo en cualquier asistente de IA listado en el diálogo de seguimiento, describa lo que salió mal y luego use la salida de la IA como cuerpo de su issue de GitHub.
- La carpeta de registro abierta por Open Log Folder es la misma carpeta donde se guardan los paquetes de soporte cuando usa File an Issue, por lo que puede arrastrar tanto el registro como el paquete a un issue de GitHub en un solo paso.

## Relacionado

- [Enable verbose logging for a specific subsystem](enable-verbose-logging-for-a-specific-subsystem.md)
- [View the live log without leaving the app](view-the-live-log-without-leaving-the-app.md)
- [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md)
- [Open the log folder to grab multiple files](open-the-log-folder-to-grab-multiple-files.md)
- [File an AI-assisted bug report](file-an-ai-assisted-bug-report.md)
- Categorías de registro de diagnóstico
- Comprensión del visor de registro
- Restablecimiento seguro de la configuración
