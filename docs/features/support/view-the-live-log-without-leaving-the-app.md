# Ver el registro en tiempo real sin salir de la aplicación

El diálogo Support & Diagnostics incluye un visor de registro integrado que permite leer la salida del registro en tiempo real sin necesidad de abrir una terminal ni un explorador de archivos externo. Úselo cuando desee observar lo que hace AetherSDR mientras reproduce un problema.

## Antes de comenzar

- No se requiere conexión de radio. El visor de registro funciona independientemente de si AetherSDR está conectado a un FLEX-8600.
- Si desea capturar un rastreo limpio de un problema específico, considere borrar el registro antes de reproducir el problema.

## Pasos

1. Haga clic en `Help > Support...` para abrir el diálogo Support & Diagnostics.
2. Localice el **Log viewer** — el área de texto oscura y amplia en el centro del diálogo. Muestra las entradas de registro más recientes automáticamente al abrir el diálogo.
3. Desplácese por el **Log viewer** para leer las entradas recientes. El visor almacena hasta 2000 líneas.
4. Si se ha generado nueva actividad en el registro desde que abrió el diálogo, haga clic en **Refresh** para recargar el archivo de registro y mostrar las entradas más recientes.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Log viewer | Área de texto desplazable | Muestra las entradas de registro más recientes. Solo lectura. Almacena hasta 2000 líneas. |
| Refresh | Botón | Recarga el archivo de registro desde el disco y actualiza el visor. |
| Log path label | Indicador | Muestra la ruta completa del archivo de registro actual. |
| Log file size | Indicador | Muestra el tamaño actual del archivo de registro activo. |
| Clear Log | Botón | Trunca el archivo de registro. El visor quedará vacío tras borrar. |
| Open Log Folder | Botón | Abre el directorio de registros en el explorador de archivos del sistema operativo. |

## Consejos

- El **Log viewer** se carga automáticamente cada vez que abre el diálogo. No es necesario hacer clic en **Refresh** la primera vez.
- Si las entradas dejan de aparecer, haga clic en **Refresh** — el visor no sigue el archivo de forma continua.
- Para aumentar el nivel de detalle capturado en el registro, habilite categorías adicionales mediante las casillas de verificación de categorías o haga clic en **Enable All** antes de reproducir el problema.
- El **Log path label** muestra exactamente dónde se encuentra el archivo si necesita abrirlo en un editor externo.

## Temas relacionados

- [Borrar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Habilitar el registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Abrir la carpeta de registros para obtener varios archivos](open-the-log-folder-to-grab-multiple-files.md)
