# Filtrar memorias por perfil

Use el filtro de Perfil en el diálogo de Canales de Memoria para reducir la tabla de memorias a las entradas que pertenecen a un perfil global específico. Esto es útil cuando tiene una lista de memorias extensa y desea ver solo los canales relevantes para su contexto operativo actual.

## Antes de comenzar

- La radio debe estar conectada. El diálogo de Canales de Memoria requiere una conexión de radio activa.
- Al menos un perfil global debe existir en la radio. El cuadro combinado `Profile:` se llena desde los perfiles globales activos de la radio.

## Pasos

1. Abra `Settings > Memory...`.
2. Localice el cuadro combinado `Profile:` en la fila de filtro en la parte superior del diálogo.
3. Haga clic en el cuadro combinado `Profile:` y seleccione el perfil por el que desea filtrar.
4. La tabla de memorias se actualiza inmediatamente para mostrar solo las entradas que coinciden con el perfil seleccionado.

Para limpiar el filtro y mostrar todas las memorias, seleccione la entrada en blanco o predeterminada en la parte superior del cuadro combinado `Profile:`.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Cuadro combinado `Profile:` | Filtra la tabla de memorias por el perfil global seleccionado. Se llena desde los perfiles globales activos de la radio. |
| Tabla de memorias | Muestra solo las filas cuyo Grupo coincide con el perfil seleccionado mientras el filtro está activo. |

## Consejos

- El filtrado por perfil y la búsqueda por nombre (`Search:`) funcionan juntos. Puede seleccionar un perfil en `Profile:` y escribir en `Search:` para reducir aún más los resultados por nombre de memoria.
- El botón `Export...` respeta el filtro de perfil actual; solo se exportan las memorias visibles bajo el filtro activo.

## Relacionados

- [Información general de Canales de Memoria](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Exportar memorias para respaldo o compartir](export-memories-for-backup-or-sharing.md)
