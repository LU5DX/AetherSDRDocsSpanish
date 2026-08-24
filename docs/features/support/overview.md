# Información general de Soporte y Diagnóstico

El diálogo de Soporte y Diagnóstico le ofrece un único lugar para controlar el registro de diagnóstico e inspeccionar el registro en vivo. Ábralo desde `Help > Support...`. No se requiere conexión de radio.

## Cómo funciona

El diálogo tiene tres áreas: un panel de control de registro en la parte superior, un visor de registro en el medio y una fila de botones de acción en la parte inferior.

**Panel de Registro de Diagnóstico**

El grupo superior, etiquetado "Diagnostic Logging", enumera cada categoría de registro disponible como una casilla de verificación. Cada casilla activa o desactiva los mensajes de ese subsistema mientras AetherSDR se ejecuta. Los cambios surten efecto de inmediato: no es necesario reiniciar.

**Visor de registro**

Debajo del panel de categorías, un área de texto de solo lectura muestra las entradas de registro más recientes. La ruta del archivo de registro se muestra arriba; el tamaño actual del archivo se muestra a la derecha de la misma fila. El visor contiene hasta 2000 líneas. Use Refresh para recargar el archivo bajo demanda.

**Botones de acción**

La fila de botones en la parte inferior ofrece los siguientes controles:

| Botón             | Qué hace                                                                                                                                                   | Notas                                                                                                                                    |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Enable All        | Activa todas las categorías de registro a la vez.                                                                                                          |                                                                                                                                          |
| Disable All       | Desactiva todas las categorías de registro a la vez.                                                                                                       |                                                                                                                                          |
| Refresh           | Recarga el archivo de registro en el visor.                                                                                                                |                                                                                                                                          |
| Clear Log         | Trunca el archivo de registro actual. Esta acción no se puede deshacer.                                                                                    |                                                                                                                                          |
| Open Log Folder   | Abre el directorio de registro en el explorador de archivos de su sistema operativo para que pueda copiar o adjuntar varios archivos.                       |                                                                                                                                          |
| Close             | Cierra el diálogo.                                                                                                                                         |                                                                                                                                          |

**Indicadores**

| Indicador                               | Qué muestra                                                                                                                                                 | Notas                                                                                                                                    |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Tamaño del archivo de registro          | Tamaño actual del archivo de registro activo, mostrado a la derecha de la etiqueta de ruta del registro.                                                    |                                                                                                                                          |
| Instrucciones (cómo informar un problema) | Bloque de texto enriquecido que dirige al usuario a `Help > File an Issue` para informar errores una vez que las categorías de registro relevantes se hayan activado y el problema se haya reproducido. | Nuevo en v26.8.4: los botones Reset Settings y File an Issue se eliminaron de este diálogo; ahora viven directamente en el menú **Help**. |

## Consejos

- Active solo las categorías relevantes al problema que está investigando para mantener el registro legible.
- Haga clic en **Clear Log** inmediatamente antes de reproducir un error para que el registro contenga solo la secuencia de eventos relevante.
- Si usa **File an Issue** (ahora en el menú **Help**), el mensaje de diagnóstico se rellena previamente con la información de su sistema y se crea un paquete de soporte automáticamente. Péguelo en cualquier asistente de IA listado en el diálogo de seguimiento, describa qué salió mal y use la salida de la IA como el cuerpo de su issue de GitHub.
- La carpeta de registro abierta por **Open Log Folder** es la misma carpeta donde se guardan los paquetes de soporte cuando usa **File an Issue**, de modo que puede arrastrar tanto el registro como el paquete a un issue de GitHub en un solo paso.

## Relacionados

- [Habilitar registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Ver el registro en vivo sin salir de la aplicación](view-the-live-log-without-leaving-the-app.md)
- [Borrar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Abrir la carpeta de registro para obtener varios archivos](open-the-log-folder-to-grab-multiple-files.md)
- [Informar un error con asistencia de IA](file-an-ai-assisted-bug-report.md)
- Categorías de registro de diagnóstico
- Cómo entender el visor de registro
- Cómo restablecer la configuración de forma segura
