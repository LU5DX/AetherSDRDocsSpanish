# Resumen de Atajos de Teclado

AetherSDR le permite asignar atajos de teclado a acciones de la aplicación y editar esas asignaciones en cualquier momento. Use el diálogo de Atajos de Teclado para ver, reasignar, limpiar o restablecer asignaciones sin reiniciar la aplicación.

## Antes de comenzar

- No se requiere conexión de radio para abrir o usar el editor de atajos.
- El procesamiento de atajos de teclado debe estar habilitado. Confirme que `View > Keyboard Shortcuts` esté marcado.

## Cómo funciona

Abra el editor en `View > Configure Shortcuts...`. El diálogo tiene dos áreas principales: un mapa de teclado visual en la parte superior y una tabla de acciones filtrable debajo.

**Mapa de teclado** — Una disposición QWERTY que muestra todas las teclas. Las teclas con acciones asignadas están codificadas por color según su categoría. Una leyenda debajo del mapa muestra qué color corresponde a cada categoría. Haga clic en cualquier tecla para seleccionarla; el panel debajo del mapa se actualiza para mostrar lo que está asignado a esa tecla.

**Panel de tecla seleccionada** — Aparece entre el mapa de teclado y la tabla de acciones. Cuando se selecciona una tecla:

- `Key:` muestra el nombre de la tecla seleccionada. Valor predeterminado: `(none)` cuando no hay nada seleccionado.
- `Action:` es un cuadro combinado. Elija una acción de la lista para asignarla a la tecla seleccionada.
- `Category` muestra la categoría de la acción actualmente asignada.
- Haga clic en `Clear` para eliminar la asignación de la tecla seleccionada.
- Haga clic en `Reset to Default` para restaurar la tecla predeterminada de la acción asignada a la tecla seleccionada.

Si asigna una tecla que ya está vinculada a una acción diferente, AetherSDR le solicitará confirmar la reasignación antes de realizar el cambio.

**Tabla de acciones** — Enumera todas las acciones disponibles. Las columnas son Action, Category, Current Key y Default Key. Haga clic en una fila para seleccionarla y reflejar esa acción en el panel de tecla seleccionada.

- `Filter:` limita la tabla escribiendo cualquier parte del nombre de una acción o categoría.
- `Category:` filtra la tabla a una sola categoría. La selección predeterminada es `All`.

**Controles inferiores**

- `Import...` — Abre un diálogo de archivos para importar una copia de seguridad CSV de atajos de teclado. Seleccione un archivo CSV existente. Después de la importación, la tabla de acciones y la información de tecla seleccionada se actualizan para reflejar las asignaciones importadas. AetherSDR muestra un resumen de la importación, incluyendo el conteo de acciones importadas, acciones desconocidas omitidas y asignaciones locales desplazadas por los atajos importados.
- `Export...` — Abre un diálogo de archivos para exportar los atajos de teclado a una copia de seguridad CSV portátil. Elija una ubicación y nombre de archivo. La exportación guarda todas las asignaciones de teclas actuales en el archivo CSV especificado.
- `Reset All to Defaults` — Restablece cada asignación a su tecla predeterminada. AetherSDR solicita confirmación antes de proceder.
- `Close` — Cierra el diálogo.

Los diálogos de importación y exportación recuerdan el último directorio utilizado, manteniéndolo entre sesiones.

## Consejos

- La tabla de acciones siempre muestra tanto la tecla actual como la predeterminada para cada acción, para que pueda ver de un vistazo qué se ha cambiado.
- Seleccionar una fila en la tabla de acciones y seleccionar una tecla en el mapa de teclado son operaciones independientes. Asigne una vinculación seleccionando primero una tecla en el mapa y luego eligiendo la acción del cuadro combinado `Action:`.
- Use `Import...` para restaurar atajos desde otra instalación de AetherSDR o desde una copia de seguridad anterior. Use `Export...` para crear una copia de seguridad portátil que pueda compartir o guardar.

## Relacionados

- [Reasignar un atajo de teclado](rebind-a-keyboard-shortcut.md)
- [Restablecer un atajo a su tecla predeterminada](reset-one-shortcut-to-its-default-key.md)
- [Restablecer todos los atajos a sus valores predeterminados](reset-every-shortcut-back-to-defaults.md)
- [Encontrar todas las acciones en una categoría](find-all-actions-in-a-category.md)
- [Ver la tecla predeterminada de cualquier acción](see-the-default-key-for-any-action.md)
- Importar atajos de teclado desde un archivo
- Exportar atajos de teclado a un archivo
