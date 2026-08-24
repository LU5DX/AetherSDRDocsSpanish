# Restablecer la Configuración de AetherSDR a los Valores Predeterminados de Fábrica

Use este procedimiento para borrar la configuración almacenada localmente de AetherSDR y la caché de sabiduría NR2 para restaurarlas a sus valores predeterminados de fábrica. La configuración almacenada en la propia radio no se ve afectada.

## Antes de comenzar

- Cierre cualquier transmisión activa o flujo de audio antes de restablecer.
- Anote cualquier configuración personalizada que desee restaurar después; el restablecimiento no se puede deshacer.

## Pasos

1. Abra `Help > Reset Settings`.
2. Cuando aparezca la solicitud de confirmación, confirme la acción.
3. Reinicie AetherSDR para que el restablecimiento surta efecto por completo.

## Qué hace cada control

| Control | Descripción | Notas |
|---|---|---|
| Casillas de categoría | Permite o deshabilita el registro por categoría. Cada categoría tiene su propia casilla. | |
| Enable All | Activa todas las categorías de registro. | |
| Disable All | Desactiva todas las categorías de registro. | |
| Etiqueta de ruta de registro | Muestra la ruta actual del archivo de registro. | |
| Visor de registro | Vista desplazable del texto de registro más reciente. | |
| Refresh | Recarga el archivo de registro. | |
| Clear Log | Trunca el archivo de registro actual. | |
| Open Log Folder | Abre el directorio de registro en el explorador de archivos del sistema operativo. | |
| Close | Cierra el diálogo. | |
| Instrucciones (guía para informar un problema) | Bloque de texto enriquecido que indica al usuario que use `Help > File an Issue` para informar errores una vez que las categorías de registro relevantes hayan sido habilitadas y el problema haya sido reproducido. | Nuevo en v26.8.4: los botones 'Reset Settings' y 'File an Issue' fueron eliminados de este diálogo (ahora se encuentran directamente en el menú Help). |

## Indicadores

| Indicador | Descripción |
|---|---|
| Tamaño del archivo de registro | Tamaño actual del archivo de registro activo. |

## Qué elimina el restablecimiento

El restablecimiento elimina los siguientes archivos:

- La base de datos principal de configuración.
- El registro de escritura anticipada de SQLite y los archivos satélite de memoria compartida (`-wal`, `-shm`).
- La instantánea de configuración XML anterior a SQLite, incluidos sus archivos hermanos `.bak`, `.tmp` y `.corrupt`.
- El archivo de caché de sabiduría NR2.
- Copias de seguridad automáticas rotativas (`*-auto.db`, `*-postmigration.db`) en el directorio de copias de seguridad.
- Almacenes de configuración corruptos en cuarentena.
- En macOS, el archivo de preferencias `com.aethersdr.AetherSDR.plist`.

Se escribe una copia de seguridad de la configuración actual en el directorio de copias de seguridad de AetherSDR antes de eliminar cualquier cosa, por lo que un restablecimiento se puede recuperar. La copia de seguridad previa al restablecimiento se escribe en una ubicación que la purga no toca.

## Consejos

- La configuración del lado de la radio (perfiles, diseño del panadapter almacenado en la radio, configuraciones de banda de TX) permanece intacta después de un restablecimiento. Solo se eliminan las AppSettings persistentes propias de AetherSDR y los datos DSP en caché.
- Si está restableciendo para resolver un problema reproducible, considere capturar un registro primero. Consulte [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md).
- El informe de errores asistido por IA incluye información del sistema (versión de AetherSDR, versión de Qt, sistema operativo y tipo de radio) y hace referencia al contexto del proyecto en https://raw.githubusercontent.com/aethersdr/AetherSDR/main/CLAUDE.md.

## Relacionado

- [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md)
- [File an AI-assisted bug report](file-an-ai-assisted-bug-report.md)
- [Support & Diagnostics overview](overview.md)
