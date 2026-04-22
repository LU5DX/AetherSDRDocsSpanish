# Filtrar memorias por perfil

Use el filtro de perfil en Memory Channels para reducir la tabla a las memorias que pertenecen a un perfil global específico. Esto es útil cuando tiene una lista de memorias extensa y desea ver solo las entradas asociadas a una configuración de operación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Memory Channels requiere una conexión de radio activa.
- Debe existir al menos un perfil global en la radio. El filtro de perfil muestra únicamente los perfiles que la radio ha reportado. Para crear perfiles, use `Profiles > Profile Manager...`.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Localice el cuadro combinado `Profile:` en la fila de filtros en la parte superior del diálogo.
3. Haga clic en el cuadro combinado `Profile:` y seleccione el perfil por el que desea filtrar.

La tabla de memorias se actualiza de inmediato para mostrar solo las memorias cuyo Group coincide con el perfil seleccionado. Las memorias que pertenecen a otros perfiles quedan ocultas, pero no se eliminan.

4. Para quitar el filtro y mostrar todas las memorias, abra el cuadro combinado `Profile:` y seleccione la entrada en blanco o "all" al principio de la lista.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Cuadro combinado `Profile:` | Filtra la tabla de memorias para mostrar solo las memorias asociadas al perfil global seleccionado. La lista se completa con los perfiles reportados por la radio conectada. |
| Tabla de memorias | Muestra el resultado filtrado. Las columnas incluyen Group, Owner, Frequency, Name, Mode y otras. La columna Group refleja la asociación de perfil utilizada para el filtrado. |

## Consejos

- El filtro `Profile:` y el campo de texto `Search:` funcionan en conjunto. Puede seleccionar un perfil y escribir un nombre en `Search:` para reducir aún más la tabla.
- Cuando use `Export...` con un filtro de perfil activo, solo las memorias que coinciden con el perfil del filtro actual se incluyen en el archivo de exportación.

## Solución de problemas

- **El cuadro combinado `Profile:` está vacío o no muestra perfiles** — La radio no ha reportado ningún perfil global. Verifique que la conexión de radio esté activa y que exista al menos un perfil. Use `Profiles > Profile Manager...` para crear perfiles.
- **Las memorias esperadas no aparecen al seleccionar un perfil** — Es posible que el campo Group de la memoria no coincida exactamente con el nombre del perfil. Abra la memoria para editarla con Edit y revise el valor de la columna Group.

## Relacionado

- [Descripción general de Memory Channels](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Exportar memorias para respaldo o uso compartido](export-memories-for-backup-or-sharing.md)
