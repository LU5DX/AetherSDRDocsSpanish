# Abrir la carpeta de registros para obtener múltiples archivos

Use esta página para abrir el directorio que contiene los archivos de registro de AetherSDR en el explorador de archivos de su sistema operativo, de modo que pueda copiar, adjuntar o archivar varios archivos de registro a la vez.

## Antes de comenzar

- No se requiere conexión de radio.
- Sepa dónde desea copiar los archivos (carpeta local, adjunto de correo electrónico, carga en un rastreador de incidencias).

## Pasos

1. Haga clic en `Help > Support...` para abrir el cuadro de diálogo Support & Diagnostics.
2. Haga clic en `Open Log Folder`.

El explorador de archivos de su sistema operativo se abrirá directamente en el directorio de registros. Desde allí, seleccione y copie los archivos que necesite.

## Consejos

- La etiqueta de ruta del registro en la parte superior del cuadro de diálogo muestra la ruta completa al archivo de registro actual, para que sepa qué directorio se abrirá antes de hacer clic.
- Si solo desea el archivo de registro actual y no toda la carpeta, consulte la etiqueta de ruta del registro y navegue hasta allí manualmente.
- Para capturar un registro limpio antes de obtener los archivos, use `Clear Log` para truncar el archivo actual, reproduzca el problema y luego haga clic en `Open Log Folder`.
- El indicador `Log file size` cerca del visor de registros muestra el tamaño actual del archivo de registro activo.

## Controles del visor de registros

El visor de registros muestra las 2000 líneas más recientes del archivo de registro activo. Use estos controles para administrar la visualización del registro:

| Control | Descripción |
|---------|-------------|
| Casillas de verificación de categoría | Active o desactive el registro por categoría. Cada categoría aparece como su propia fila de casilla de verificación. |
| Enable All | Active todas las categorías de registro. |
| Disable All | Desactive todas las categorías de registro. |
| Etiqueta de ruta del registro | Muestra la ruta del archivo de registro actual. |
| Visor de registros | Vista desplazable del texto de registro más reciente (máximo 2000 líneas). |
| Refresh | Recarga el archivo de registro. |
| Clear Log | Trunca el archivo de registro actual. |
| Open Log Folder | Abre el directorio de registros en el explorador de archivos del sistema operativo. |
| Reset Settings | Restablece la configuración de AetherSDR a los valores predeterminados (con cuadro de diálogo de confirmación). |
| File an Issue | Inicia el flujo de informe de errores asistido por IA. |
| Close | Cierra el cuadro de diálogo. |

## Relacionado

- [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md)
- [View the live log without leaving the app](view-the-live-log-without-leaving-the-app.md)
- [File an AI-assisted bug report](file-an-ai-assisted-bug-report.md)
