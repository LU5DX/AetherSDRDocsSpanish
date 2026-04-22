# Activar el registro detallado para un subsistema específico

Use el diálogo Support & Diagnostics para activar el registro de subsistemas individuales. Habilitar solo las categorías que necesita mantiene el registro legible y facilita el aislamiento de un problema.

## Antes de comenzar

- Reproduzca el problema después de activar el registro, no antes: el visor de registros muestra únicamente las entradas recientes.
- Si desea una captura limpia, borre el registro antes de reproducir el problema.

## Pasos

1. Haga clic en `Help > Support...` para abrir el diálogo Support & Diagnostics.
2. En el grupo **Diagnostic Logging**, busque la fila con la casilla de verificación correspondiente al subsistema que desea rastrear.
3. Marque la casilla junto a esa categoría. La etiqueta de la casilla identifica el subsistema. El registro de esa categoría se activa de inmediato — no es necesario aplicar cambios ni reiniciar.
4. Reproduzca la condición que está diagnosticando.
5. Haga clic en **Refresh** para recargar el visor de registros con las entradas más recientes.
6. Revise el resultado en el **Log viewer**.

Para deshabilitar la categoría cuando termine, desmarque la misma casilla.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Casillas de categoría | Casilla de verificación (una por subsistema) | Activa o desactiva el registro de esa categoría específica. Los cambios surten efecto de inmediato. |
| Enable All | Botón | Activa todas las categorías de registro a la vez. |
| Disable All | Botón | Desactiva todas las categorías de registro a la vez. |
| Log viewer | Área de texto desplazable | Muestra las entradas de registro más recientes (hasta 2000 líneas). |
| Refresh | Botón | Recarga el archivo de registro en el visor de registros. |
| Etiqueta de ruta del registro | Indicador | Muestra la ruta del archivo de registro activo. |
| Tamaño del archivo de registro | Indicador | Muestra el tamaño actual del archivo de registro activo. |

## Consejos

- Use **Disable All** primero y luego marque solo la categoría que necesita. Esto reduce el ruido en el registro cuando está rastreando un problema específico.
- Use **Enable All** cuando no esté seguro de qué subsistema está involucrado y desee la captura más amplia posible.
- El visor de registros admite un máximo de 2000 líneas. Para sesiones más largas, haga clic en **Open Log Folder** para acceder al archivo completo en el disco.

## Relacionados

- [Borrar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Ver el registro en vivo sin salir de la aplicación](view-the-live-log-without-leaving-the-app.md)
- [Abrir la carpeta de registros para obtener varios archivos](open-the-log-folder-to-grab-multiple-files.md)
- [Presentar un informe de error asistido por IA](file-an-ai-assisted-bug-report.md)
