# Editar un valor de configuración desde el Examinador de configuraciones

En esta página se explica cómo editar cualquier valor de configuración de AetherSDR directamente desde el Examinador de configuraciones, algo útil para parámetros que no tienen una interfaz dedicada.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El Examinador de configuraciones funciona sin conexión a la radio.
- Usted tiene en mente una clave específica de AppSettings, o puede localizarla mediante el filtro.

## Pasos

1. Abra el Examinador de configuraciones: `Settings > Settings Browser...`.
2. En el panel izquierdo, seleccione el ámbito que contiene el valor: aplicación, estación o una radio específica (identificada por apodo o número de serie).
3. En el campo **Filter**, escriba parte de la clave o del valor para reducir la lista. El árbol se filtra en tiempo real mientras escribe.
4. Localice la fila que desea editar. La clave está en la columna izquierda; el valor está en la columna derecha.
5. Haga doble clic en la celda del valor, o seleccione la fila y presione **Enter** (o **Return**).
6. Edite el valor:
   - Los valores booleanos (mostrados como `True` o `False`) presentan una lista desplegable con solo dos opciones.
   - Todos los demás valores son de texto libre. Escriba el nuevo valor.
7. Presione **Enter** o haga clic en otro lugar para confirmar el cambio.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Árbol de ámbitos (panel izquierdo) | Enumera los ámbitos de configuración: claves de la aplicación, sección de la estación y los documentos de funciones de cada radio. | Los ámbitos de radio muestran el apodo cuando existe un documento de identidad (Identity). |
| **Filter** | Coincidencia de subcadena sin distinción de mayúsculas o minúsculas sobre las claves y valores del ámbito seleccionado. | No es un valor persistente. |
| Tabla de valores | Muestra los pares clave/valor del ámbito seleccionado. La edición está habilitada. | Los valores con forma de credencial están enmascarados y son de solo lectura. |
| **Add Key…** | Añade una nueva clave al ámbito seleccionado. | Úselo solo si conoce el nombre exacto de la clave y el formato esperado. |
| **Delete** | Elimina el valor seleccionado. | El borrado es inmediato. |
| **Refresh** | Recarga el árbol de configuraciones desde el almacén. | Úselo después de cambios externos. |
| **Export Sanitized…** | Genera un volcado de diagnóstico con los secretos redactados. | No es una copia de seguridad restaurable; los valores con forma de credencial están redactados. |
| **Close** | Cierra el diálogo. | |

## Consejos

- Las ediciones se aplican de inmediato y omiten la validación propia de cada función. Prefiera la interfaz propia de la función cuando exista.
- Un banner amarillo en la parte superior del diálogo advierte sobre este comportamiento. Téngalo en cuenta antes de cambiar valores.
- Los valores booleanos se almacenan como las cadenas literales `True` y `False`. La lista desplegable evita errores de escritura como `Ture`.

## Solución de problemas

- **La celda del valor no entra en modo de edición** — La fila es de solo lectura porque el valor tiene forma de credencial (contiene una contraseña, clave o token) o porque es un documento de función. Los documentos de función se abren en un visor; los valores con forma de credencial no pueden editarse aquí.
- **Cambié un valor y ahora una función se comporta mal** — El Examinador de configuraciones omite la validación. Use **Refresh** (o vuelva a abrir el diálogo) para confirmar el valor almacenado y luego corríjalo o restáurelo a partir del valor anterior, ya sea de memoria o de una copia de seguridad.

## Relacionados

- [Información general del Examinador de configuraciones](overview.md)
- [Examinar todas las configuraciones de AetherSDR](browse-all-aethersdr-settings.md)
- [Exportar un volcado de configuración de diagnóstico](export-a-diagnostic-settings-dump.md)
