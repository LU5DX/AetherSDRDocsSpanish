# Resumen de Soporte y Diagnóstico

El diálogo Support & Diagnostics le ofrece un único lugar para controlar el registro de diagnóstico, inspeccionar el registro en tiempo real y reportar errores. Ábralo desde `Help > Support...`. No se requiere conexión a la radio.

## Cómo funciona

El diálogo tiene tres áreas: un panel de control de registro en la parte superior, un visor de registro en el centro y una fila de botones de acción en la parte inferior.

**Panel Diagnostic Logging**

El grupo superior, etiquetado como "Diagnostic Logging", enumera todas las categorías de registro disponibles como casillas de verificación. Cada casilla habilita o deshabilita los mensajes de ese subsistema mientras AetherSDR está en ejecución. Los cambios surten efecto de inmediato — no es necesario reiniciar.

**Visor de registro**

Debajo del panel de categorías, un área de texto de solo lectura muestra las entradas de registro más recientes. La ruta del archivo de registro se muestra encima; el tamaño actual del archivo se muestra a la derecha de la misma fila. El visor admite hasta 2000 líneas. Use Refresh para recargar el archivo cuando lo necesite.

**Botones de acción**

La fila de botones en la parte inferior ofrece los siguientes controles:

| Botón | Qué hace |
|---|---|
| Enable All | Activa todas las categorías de registro a la vez. |
| Disable All | Desactiva todas las categorías de registro a la vez. |
| Refresh | Recarga el archivo de registro en el visor. |
| Clear Log | Trunca el archivo de registro actual. Esta acción no se puede deshacer. |
| Open Log Folder | Abre el directorio de registros en el explorador de archivos del sistema operativo para que pueda copiar o adjuntar varios archivos. |
| Reset Settings | Restablece la configuración de AetherSDR a los valores predeterminados tras solicitar confirmación. La configuración de la radio almacenada en el equipo no se ve afectada. |
| File an Issue | Inicia el flujo de reporte de errores asistido por IA. Copia un prompt de diagnóstico (con su versión de AetherSDR, versión de Qt, sistema operativo y detalles de la radio conectada) al portapapeles, y luego lo guía para abrir un asistente de IA y enviar un issue en GitHub. |
| Close | Cierra el diálogo. |

## Consejos

- Habilite solo las categorías relevantes para el problema que está investigando, a fin de mantener el registro legible.
- Haga clic en Clear Log inmediatamente antes de reproducir un error, de modo que el registro contenga únicamente la secuencia de eventos relevante.
- Si usa File an Issue, el prompt de diagnóstico se rellena previamente con la información de su sistema. Péguelo en cualquier asistente de IA indicado en el diálogo de seguimiento, describa lo que salió mal y luego use la respuesta de la IA como cuerpo de su issue en GitHub.
- La carpeta de registros que abre Open Log Folder es la misma carpeta donde se guardan los paquetes de soporte cuando usa File an Issue, por lo que puede arrastrar tanto el registro como el paquete a un issue de GitHub en un solo paso.

## Relacionado

- [Habilitar el registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Ver el registro en tiempo real sin salir de la aplicación](view-the-live-log-without-leaving-the-app.md)
- [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Abrir la carpeta de registros para obtener varios archivos](open-the-log-folder-to-grab-multiple-files.md)
- [Enviar un reporte de error asistido por IA](file-an-ai-assisted-bug-report.md)
- [Restablecer la configuración de AetherSDR a los valores de fábrica](reset-aethersdr-settings-to-factory-defaults.md)
