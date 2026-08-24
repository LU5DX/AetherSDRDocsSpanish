# Resumen del Explorador de Configuración

El Explorador de Configuración le ofrece una vista completa y buscable de todas las opciones de AetherSDR en un solo lugar, incluidos los árboles agrupados por ámbito para la aplicación, la estación y los documentos de funciones de cada radio. Es principalmente una herramienta de diagnóstico y edición avanzada para opciones que no tienen una interfaz dedicada, que le permite inspeccionar y cambiar valores directamente con filtrado en vivo y una exportación saneada para soporte.

## Cómo funciona

El Explorador de Configuración se abre mediante **Settings > Settings Browser...** y presenta un árbol de ámbitos a la izquierda (configuración de la aplicación, la sección de la estación y los documentos de funciones de cada radio conectada), con una tabla de clave-valor para el ámbito seleccionado a la derecha.

Es una herramienta avanzada:

- Las ediciones se aplican inmediatamente y omiten la validación propia de cada función.
- Prefiera la interfaz dedicada de la función cuando exista una.
- Los valores con forma de credencial (contraseñas, tokens) están enmascarados y son de solo lectura, por lo que no puede sobrescribir accidentalmente un secreto con un marcador de posición redactado.

El diálogo incluye un banner de advertencia en la parte superior para recordarle esto.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Filter** | Coincidencia de subcadena en vivo, sin distinción de mayúsculas y minúsculas, sobre las claves y valores del ámbito seleccionado. | Se muestra en la parte superior del panel derecho. |
| **Add Key…** | Agrega una nueva clave de configuración al ámbito seleccionado. | No se permiten valores vacíos. |
| **Delete** | Elimina la opción seleccionada. | Solo está habilitado cuando se selecciona una fila que no es de solo lectura. |
| **Refresh** | Reconstruye el árbol de ámbitos para reflejar cualquier opción que la radio u otros procesos hayan cambiado debajo del diálogo. | Útil después de modificaciones externas. |
| **Export Sanitized…** | Escribe un volcado de texto de diagnóstico con secretos redactados del almacén de configuración a un archivo. | Solo salida de diagnóstico: no es una copia de seguridad restaurable. |
| **Close** | Cierra el diálogo. | |

En la tabla de valores, los valores booleanos (`True`/`False`) se editan con una lista desplegable de dos entradas para evitar errores tipográficos como `Ture`. Haga doble clic en un valor (o seleccione una fila y presione **Enter**) para editarlo; las filas de documentos de funciones abren un diálogo de visor en lugar de edición en línea.

## Consejos

- Use **Filter** para encontrar una clave rápidamente: busca tanto en claves como en valores, por lo que puede escribir parte de un valor para localizar la opción que lo contiene.
- Las radios se muestran por su apodo de **Identity** cuando se ha configurado uno; los valores predeterminados de toda la familia aparecen como `(family-wide defaults)`.
- El diálogo recuerda su tamaño de ventana y posición entre sesiones.
- Si corrige un error tipográfico, presione **Refresh** para volver a leer el estado actual del almacén.

## Solución de problemas

- **No puedo editar una opción que esperaba poder cambiar** — Los valores con forma de credencial son intencionalmente de solo lectura y están enmascarados. Realice el cambio desde la interfaz propia de la función.
- **Un documento de funciones muestra `(corrupt)`** — El JSON almacenado no se pudo analizar. El valor sin procesar aún se muestra para diagnóstico; puede sobrescribirlo con un documento válido mediante **Add Key…**.

## Relacionado

- [Examinar todas las opciones de AetherSDR](browse-all-aethersdr-settings.md)
- [Editar un valor de configuración desde el Explorador de Configuración](edit-a-settings-value-from-the-settings-browser.md)
- [Exportar un volcado de configuración de diagnóstico](export-a-diagnostic-settings-dump.md)
