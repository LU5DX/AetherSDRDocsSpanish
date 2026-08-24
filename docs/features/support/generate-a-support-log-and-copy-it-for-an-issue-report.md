# Generar un registro de soporte y copiarlo para un informe de incidencia

Genere un registro de soporte con las categorías de registro adecuadas activadas y luego cópielo o adjúntelo a un informe de incidencia de GitHub para que los desarrolladores de AetherSDR puedan diagnosticar su problema.

## Antes de comenzar

- Ha reproducido el problema o conoce los pasos para reproducirlo.
- Sabe qué subsistema está involucrado (por ejemplo, audio, conexión de radio, CW, DAX) para seleccionar la categoría de registro relevante.

## Pasos

1. Abra Support & Diagnostics mediante `Help > Support...`.
2. En el grupo Diagnostic Logging, marque la casilla junto a la categoría relevante (por ejemplo, el subsistema relacionado con su problema). Si no está seguro, haga clic en **Enable All** para activar todas las categorías.
3. Haga clic en **Close**.
4. **Reinicie AetherSDR** — los cambios de registro solo surten efecto en el próximo inicio.
5. Reproduzca el problema.
6. Abra Support & Diagnostics nuevamente mediante `Help > Support...`.
7. Revise el visor de registro. Haga clic en **Refresh** para recargar el archivo de registro y asegurarse de que contenga las entradas más recientes.
8. Haga clic en **Open Log Folder** para revelar el archivo de registro en el explorador de archivos de su sistema operativo.
9. Copie o arrastre el archivo de registro a su informe de incidencia:
   - Desde el explorador de archivos, copie el archivo `.log`.
   - Vaya a `Help > File an Issue...` para abrir el formulario de incidencia de GitHub.
   - Pegue el contenido del registro o arrastre el archivo de registro al formulario.

## Qué hace cada control

| Control | Comportamiento |
| --- | --- |
| Casillas de categoría | Activan o desactivan el registro por categoría. Cada fila corresponde a una categoría de registro; pase el cursor sobre ella para ver su descripción. |
| **Enable All** | Activa todas las categorías de registro. |
| **Disable All** | Desactiva todas las categorías de registro. |
| Etiqueta de ruta de registro | Muestra la ruta completa del archivo de registro activo. |
| Tamaño del archivo de registro | Muestra el tamaño actual del archivo de registro activo. |
| Visor de registro | Vista desplazable y de solo lectura del texto de registro más reciente (hasta 2000 líneas o 200 KB). |
| **Refresh** | Recarga el contenido del archivo de registro y se desplaza hasta el final. |
| **Clear Log** | Trunca el archivo de registro actual y actualiza el visor. |
| **Open Log Folder** | Abre el directorio de registro en el explorador de archivos del sistema operativo. |
| **Close** | Cierra el diálogo. |

## Consejos

- Borrar el registro antes de reproducir un error produce un archivo de registro más pequeño y enfocado, más fácil de revisar para los desarrolladores. Consulte [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md).
- Cuando informe una incidencia mediante `Help > File an Issue...`, AetherSDR recopila automáticamente la información de la radio (modelo, número de serie, firmware, versión del protocolo, indicativo, IP) y la adjunta al registro si hay una radio conectada.
- El bloque de instrucciones dentro del propio diálogo de Support refleja estos pasos: active el registro relevante, reinicie, reproduzca y luego use `Help > File an Issue...`.

## Solución de problemas

- **El archivo de registro está vacío** — El registro puede estar desactivado para la categoría relevante. Abra Support & Diagnostics, marque la casilla de la categoría relevante (o haga clic en **Enable All**), haga clic en **Close** y reinicie AetherSDR antes de reproducir la incidencia.
- **El visor de registro muestra "(unable to open log file)"** — El archivo de registro puede estar bloqueado por otro proceso o faltar. Haga clic en **Open Log Folder** para inspeccionar si el archivo de registro existe; si no, reinicie AetherSDR para recrearlo.
- **El registro contiene muy poca información** — Active más categorías mediante **Enable All**, reinicie y reproduzca la incidencia nuevamente. El registro solo captura eventos de categorías que estaban activadas en el momento en que ocurrió el problema.

## Relacionados

- [Support & Diagnostics overview](overview.md)
- [Enable verbose logging for a specific subsystem](enable-verbose-logging-for-a-specific-subsystem.md)
- [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md)
- [Open the log folder to grab multiple files](open-the-log-folder-to-grab-multiple-files.md)
