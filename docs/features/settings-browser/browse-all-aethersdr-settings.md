# Explorar todos los ajustes de AetherSDR

Abra el Explorador de ajustes para inspeccionar y editar cada ajuste de AetherSDR en un solo lugar, incluidas las claves de toda la aplicación, la sección de estación y los documentos de funciones por radio. Úselo para cambiar la configuración que no tiene un diálogo dedicado y para comprender qué valor tiene cada elemento almacenado.

## Antes de comenzar

- AetherSDR debe estar en ejecución. **No** se requiere una conexión de radio.
- Los ajustes editados aquí se aplican de inmediato y omiten la validación propia de cada función. Prefiera la interfaz dedicada de la función cuando exista una.

## Pasos

1. En la ventana principal, vaya a **Settings > Settings Browser...**.
2. En el panel izquierdo, seleccione un ámbito:
   - Claves de la aplicación (ajustes de toda la aplicación)
   - La sección de estación
   - Cualquier radio listada, identificada por su apodo o ID de radio
3. En el campo **Filter** en la parte superior derecha, escriba para reducir la tabla de claves/valores a las filas que coincidan. La coincidencia no distingue entre mayúsculas y minúsculas y verifica tanto claves como valores.
4. Para cambiar un valor, haga doble clic en la celda **Value** (o presione **Enter**). Los valores booleanos muestran una lista desplegable **True**/**False**; todo lo demás es texto libre.
5. Edite el valor y luego presione **Enter** o haga clic fuera para confirmar.
6. Para agregar una nueva clave, haga clic en **Add Key…**, ingrese el nombre de la clave y establezca su valor.
7. Para eliminar una clave, seleccione su fila y haga clic en **Delete**.
8. Cuando termine, haga clic en **Close**.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Notas |
| --- | --- | --- | --- |
| **Filter** (campo de texto) | Filtra la tabla de ajustes en vivo mientras escribe. Coincidencia de subcadena sin distinguir mayúsculas y minúsculas sobre claves y valores del ámbito seleccionado. | Vacío | |
| **Add Key…** (botón) | Agrega una nueva clave al ámbito seleccionado. | | |
| **Delete** (botón) | Elimina el ajuste seleccionado. | | |
| **Refresh** (botón) | Recarga el árbol desde el almacén de ajustes. | | |
| **Export Sanitized…** (botón) | Exporta un volcado de texto de diagnóstico saneado del almacén de ajustes. | | Solo salida de diagnóstico, no una copia de seguridad; los valores con forma de credencial se redactan. |
| **Close** (botón) | Cierra el diálogo. | | |

## Consejos

- El banner en la parte superior advierte que las ediciones se aplican de inmediato y omiten la validación. Si un ajuste se comporta mal, cámbielo de nuevo o use la interfaz dedicada en su lugar.
- Las filas cuyos valores contienen datos con forma de credencial (por ejemplo, contraseñas o tokens) se muestran parcialmente redactadas y son de solo lectura. Editarlas sobrescribiría el secreto real con el marcador redactado.
- Use **Refresh** después de cambiar ajustes en otro lugar de AetherSDR para asegurarse de que el explorador muestre el almacén actual.

## Solución de problemas

- **Un valor muestra `[REDACTED]` y no me deja editar** — El valor contiene datos con forma de credencial. AetherSDR lo enmascara por seguridad y evita la sobrescritura accidental. Use el diálogo de ajustes propio de la función para cambiarlo.
- **Mi edición parece no tener efecto** — El ajuste puede leerse al inicio o requerir una reconexión de radio. Consulte el diálogo de la función correspondiente para ver una nota, o reinicie AetherSDR.

## Relacionado

- [Editar un valor de ajuste desde el Explorador de ajustes](edit-a-settings-value-from-the-settings-browser.md)
- [Exportar un volcado de ajustes de diagnóstico](export-a-diagnostic-settings-dump.md)
- [Descripción general del Explorador de ajustes](overview.md)
