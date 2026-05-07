# Soporte y diagnóstico: visión general

El diálogo de Soporte y diagnóstico le ofrece un lugar único para controlar el registro de diagnóstico, inspeccionar el registro en vivo y reportar fallos. Ábralo desde `Help > Support...`. No se requiere conexión de radio.

## Cómo funciona

El diálogo tiene tres áreas: un panel de control de registro en la parte superior, un visor de registro en el medio y una fila de botones de acción en la parte inferior.

**Panel de Registro de diagnóstico**

El grupo superior, etiquetado como "Diagnostic Logging", enumera cada categoría de registro disponible como una casilla de verificación. Cada casilla habilita o deshabilita los mensajes de ese subsistema mientras AetherSDR se ejecuta. Los cambios surten efecto de inmediato; no es necesario reiniciar.

**Visor de registro**

Debajo del panel de categorías, un área de texto de solo lectura muestra las entradas de registro más recientes. La ruta del archivo de registro se muestra arriba; el tamaño actual del archivo se muestra a la derecha de la misma fila. El visor admite hasta 2000 líneas. Use Refresh para recargar el archivo bajo demanda.

**Botones de acción**

La fila de botones en la parte inferior proporciona los siguientes controles:

| Botón | Qué hace |
|---|---|
| Enable All | Activa todas las categorías de registro a la vez. |
| Disable All | Desactiva todas las categorías de registro a la vez. |
| Refresh | Recarga el archivo de registro en el visor. |
| Clear Log | Trunca el archivo de registro actual. Esta acción no se puede deshacer. |
| Open Log Folder | Abre el directorio de registro en el explorador de archivos de su sistema operativo para que pueda copiar o adjuntar varios archivos. |
| Reset Settings | Restablece la configuración de AetherSDR a los valores predeterminados después de solicitar confirmación. La configuración de radio almacenada en el equipo no se ve afectada. |
| File an Issue | Inicia el flujo de reporte de fallos asistido por IA. Copia un prompt de diagnóstico (con su versión de AetherSDR, versión de Qt, sistema operativo y detalles de la radio conectada) al portapapeles, luego le guía para abrir un asistente de IA y enviar un issue a GitHub. |
| Close | Cierra el diálogo. |

## Consejos

- Habilite solo las categorías relevantes para el problema que está investigando a fin de mantener el registro legible.
- Haga clic en Clear Log inmediatamente antes de reproducir un fallo para que el registro contenga solo la secuencia de eventos relevante.
- Si usa File an Issue, el prompt de diagnóstico se rellena previamente con la información de su sistema. Péguelo en cualquier asistente de IA listado en el diálogo posterior, describa lo que salió mal y luego use la salida de la IA como el cuerpo de su issue en GitHub.
- La carpeta de registro abierta por Open Log Folder es la misma carpeta donde se guardan los paquetes de soporte cuando usa File an Issue, por lo que puede arrastrar tanto el registro como el paquete a un issue de GitHub en un solo paso.

## Relacionado

- [Enable verbose logging for a specific subsystem](enable-verbose-logging-for-a-specific-subsystem.md)
- [View the live log without leaving the app](view-the-live-log-without-leaving-the-app.md)
- [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md)
- [Open the log folder to grab multiple files](open-the-log-folder-to-grab-multiple-files.md)
- [File an AI-assisted bug report](file-an-ai-assisted-bug-report.md)
- [Reset AetherSDR settings to factory defaults](reset-aethersdr-settings-to-factory-defaults.md)
