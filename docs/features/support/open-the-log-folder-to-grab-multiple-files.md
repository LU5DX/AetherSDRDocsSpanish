# Abrir la carpeta de registros para obtener varios archivos

Use esta página para abrir el directorio que contiene los archivos de registro de AetherSDR en el explorador de archivos de su sistema operativo, de modo que pueda copiar, adjuntar o archivar varios archivos de registro a la vez.

## Antes de comenzar

- No se requiere conexión de radio.
- Sepa dónde desea copiar los archivos (carpeta local, adjunto de correo electrónico, carga en un rastreador de incidencias).

## Pasos

1. Haga clic en `Help > Support...` para abrir el diálogo Support & Diagnostics.
2. Haga clic en `Open Log Folder`.

El explorador de archivos de su sistema operativo se abre directamente en el directorio de registros. Desde allí, seleccione y copie los archivos que necesite.

## Consejos

- La etiqueta de ruta de registro en la parte superior del diálogo muestra la ruta completa al archivo de registro actual, por lo que sabrá qué directorio se abrirá antes de hacer clic.
- Si solo desea el archivo de registro actual en lugar de toda la carpeta, consulte la etiqueta de ruta de registro y navegue allí manualmente.
- Para capturar un registro limpio antes de obtener archivos, use `Clear Log` para truncar el archivo actual, reproduzca el problema y luego haga clic en `Open Log Folder`.
- El indicador `Log file size` junto al visor de registros muestra el tamaño actual del archivo de registro activo.

## Controles del visor de registros

El visor de registros muestra las 2000 líneas más recientes del archivo de registro activo. Use estos controles para gestionar la visualización del registro:

| Control                               | Descripción                                                                                                                                                    | Notas                                                                                                                                     |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| Category checkboxes                   | Activa o desactiva el registro por categoría. Cada categoría aparece como su propia fila de casilla de verificación.                                                                         |                                                                                                                                           |
| Enable All                            | Activa todas las categorías de registro.                                                                                                                                |                                                                                                                                           |
| Disable All                           | Desactiva todas las categorías de registro.                                                                                                                               |                                                                                                                                           |
| Log path label                        | Muestra la ruta del archivo de registro actual.                                                                                                                               |                                                                                                                                           |
| Log viewer                            | Vista desplazable del texto de registro más reciente (máximo 2000 líneas).                                                                                              |                                                                                                                                           |
| Refresh                               | Recarga el archivo de registro.                                                                                                                                          |                                                                                                                                           |
| Clear Log                             | Trunca el archivo de registro actual.                                                                                                                                |                                                                                                                                           |
| Open Log Folder                       | Abre el directorio de registros en el explorador de archivos del sistema operativo.                                                                                                                |                                                                                                                                           |
| Close                                 | Cierra el diálogo.                                                                                                                                             |                                                                                                                                           |
| Instructions (report-an-issue how-to) | Bloque de texto enriquecido que indica al usuario que use `Help > File an Issue` para informar errores una vez que las categorías de registro relevantes estén activadas y el problema se haya reproducido. | Nuevo en v26.8.4: los botones `Reset Settings` y `File an Issue` se eliminaron de este diálogo (ahora se encuentran directamente en el menú Help). |

## Relacionados

- [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md)
- [View the live log without leaving the app](view-the-live-log-without-leaving-the-app.md)
- [File an AI-assisted bug report](file-an-ai-assisted-bug-report.md)
