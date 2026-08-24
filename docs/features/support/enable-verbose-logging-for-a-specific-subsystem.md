# Habilitar registro detallado para un subsistema específico

El diálogo Support & Diagnostics le permite activar el registro para subsistemas individuales. Active únicamente las categorías que necesite para mantener la salida del registro enfocada y más fácil de leer al diagnosticar un problema.

## Antes de comenzar

- No se requiere conexión de radio para cambiar las categorías de registro.
- Si desea un registro limpio que comience en el momento en que reproduce un error, borre el registro primero antes de habilitar las categorías.

## Pasos

1. Haga clic en `Help > Support...` para abrir el diálogo Support & Diagnostics.
2. En el grupo **Diagnostic Logging**, busque la fila de casillas de verificación correspondiente al subsistema que desea diagnosticar.
3. Marque la casilla junto a la etiqueta de esa categoría para habilitar el registro. Desmárquela para deshabilitarlo.
4. Reproduzca el comportamiento que está investigando. La salida del registro comienza inmediatamente cuando se habilita una categoría.
5. Haga clic en **Refresh** para recargar el archivo de registro y ver las entradas más recientes en el visor de registro.

## Qué hace cada control

| Control                               | Tipo                                                                                                                                                           | Comportamiento                                                                                                                            |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| Casillas de verificación de categoría | Casilla de verificación                                                                                                                                        | Una fila por categoría de registro. Márquela para habilitar, desmárquela para deshabilitar. Los cambios se aplican de inmediato.          |
| Enable All                            | Botón                                                                                                                                                          | Activa todas las categorías de registro a la vez.                                                                                         |
| Disable All                           | Botón                                                                                                                                                          | Desactiva todas las categorías de registro a la vez.                                                                                      |
| Visor de registro                     | Área de texto                                                                                                                                                  | Vista desplazable del texto de registro más reciente. Muestra hasta 2000 líneas.                                                          |
| Refresh                               | Botón                                                                                                                                                          | Recarga el archivo de registro en el visor de registro.                                                                                   |
| Clear Log                             | Botón                                                                                                                                                          | Trunca el archivo de registro actual.                                                                                                     |
| Open Log Folder                       | Botón                                                                                                                                                          | Abre el directorio de registro en el explorador de archivos del sistema operativo.                                                        |
| Etiqueta de ruta de registro          | Indicador                                                                                                                                                      | Muestra la ruta completa del archivo de registro actual.                                                                                  |
| Tamaño del archivo de registro        | Indicador                                                                                                                                                      | Muestra el tamaño actual del archivo de registro activo.                                                                                  |
| Close                                 | Botón                                                                                                                                                          | Cierra el diálogo.                                                                                                                        |
| Instrucciones (cómo informar un problema) | Bloque de texto enriquecido que indica al usuario usar `Help > File an Issue` para informar errores una vez que las categorías de registro relevantes se hayan habilitado y el problema se haya reproducido. | Nuevo en v26.8.4: los botones **Reset Settings** y **File an Issue** se eliminaron de este diálogo (ahora viven directamente en el menú `Help`, bajo `Help > Reset Settings` y `Help > File an Issue`, respectivamente). |

**Nota:** El botón **Reset Settings** se ha eliminado del diálogo Support & Diagnostics. Para restablecer la configuración específica de la aplicación de AetherSDR, use `Help > Reset Settings` en su lugar.

## Consejos

- Use **Enable All** únicamente cuando no esté seguro de qué subsistema está involucrado. El registro será extenso. Para una investigación específica, habilite solo la casilla de la categoría relevante.
- Use **Disable All** después de haber capturado lo que necesita para detener el crecimiento adicional del registro.
- El visor de registro muestra un máximo de 2000 líneas. Si necesita el archivo completo, haga clic en **Open Log Folder** para acceder a él directamente en su explorador de archivos.

## Relacionado

- [Borrar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Ver el registro en vivo sin salir de la aplicación](view-the-live-log-without-leaving-the-app.md)
- [Abrir la carpeta de registro para tomar varios archivos](open-the-log-folder-to-grab-multiple-files.md)
- [Informar un error con asistencia de IA](file-an-ai-assisted-bug-report.md)
