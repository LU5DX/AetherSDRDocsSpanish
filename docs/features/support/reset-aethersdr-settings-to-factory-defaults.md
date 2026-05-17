# Restaurar la configuración predeterminada de fábrica de AetherSDR

Utilice este procedimiento para eliminar la configuración almacenada localmente de AetherSDR y la caché de conocimiento NR2, restaurando los valores predeterminados de fábrica. La configuración almacenada en la radio no se ve afectada.

## Antes de comenzar

- Cierre cualquier transmisión activa o flujo de audio antes de restablecer.
- Anote cualquier configuración personalizada que desee restaurar después; el restablecimiento no se puede deshacer.

## Pasos

1. Abra `Help > Support...` para abrir el diálogo Support & Diagnostics.
2. Haga clic en `Reset Settings`.
3. Cuando aparezca el mensaje de confirmación, confirme la acción.
4. Reinicie AetherSDR para que el restablecimiento surta efecto por completo.

## Función de cada control

| Control | Descripción |
|---|---|
| Category checkboxes | Activa o desactiva el registro por categoría. Cada categoría tiene su propia casilla de verificación. |
| Enable All | Activa todas las categorías de registro. |
| Disable All | Desactiva todas las categorías de registro. |
| Log path label | Muestra la ruta actual del archivo de registro. |
| Log viewer | Vista desplazable del texto de registro más reciente. |
| Refresh | Vuelve a cargar el archivo de registro. |
| Clear Log | Trunca el archivo de registro actual. |
| Open Log Folder | Abre el directorio de registro en el explorador de archivos del sistema operativo. |
| Reset Settings | Elimina la configuración local de AetherSDR y la caché de conocimiento NR2. La configuración almacenada en la radio FLEX-8600 no se modifica. Se muestra un mensaje de confirmación antes de eliminar cualquier dato. |
| File an Issue | Inicia el flujo de informe de errores asistido por IA. Esto abre un informe de error en GitHub en https://github.com/aethersdr/AetherSDR/issues/new con la etiqueta "bug" preseleccionada. |
| Close | Cierra el diálogo. |

## Indicadores

| Indicador | Descripción |
|---|---|
| Log file size | Tamaño actual del archivo de registro activo. |

## Consejos

- La configuración del lado de la radio (perfiles, diseño de panadapter almacenado en la radio, configuración de banda de TX) permanece intacta después de un restablecimiento. Solo se eliminan los AppSettings persistentes de AetherSDR y los datos DSP almacenados en caché.
- Si está restableciendo para resolver un problema reproducible, considere capturar un registro primero. Consulte [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md).
- El informe de error asistido por IA incluye información del sistema (versión de AetherSDR, versión de Qt, sistema operativo y tipo de radio) y hace referencia al contexto del proyecto en https://raw.githubusercontent.com/aethersdr/AetherSDR/main/CLAUDE.md.

## Relacionados

- [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md)
- [File an AI-assisted bug report](file-an-ai-assisted-bug-report.md)
- [Support & Diagnostics overview](overview.md)
