# Filtrar memorias por perfil

Use el filtro `Profile:` en el diálogo Memory Channels para reducir la tabla de memorias a las entradas que pertenecen a un perfil global específico. Esto resulta útil cuando tiene una lista de memorias extensa y desea ver únicamente los canales relevantes para su contexto operativo actual.

## Antes de comenzar

- La radio debe estar conectada. El diálogo Memory Channels requiere una conexión de radio activa.
- Debe existir al menos un perfil global en la radio. El cuadro combinado `Profile:` se llena a partir de los perfiles globales activos de la radio.

## Pasos

1. Abra `Settings > Memory...`.
2. Localice el cuadro combinado `Profile:` en la fila de filtros en la parte superior del diálogo.
3. Haga clic en el cuadro combinado `Profile:` y seleccione el perfil por el que desea filtrar.
4. La tabla de memorias se actualiza de inmediato para mostrar solo las entradas que coinciden con el perfil seleccionado.

Para borrar el filtro y mostrar todas las memorias, seleccione la entrada en blanco o predeterminada en la parte superior del cuadro combinado `Profile:`.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Cuadro combinado `Profile:` | Filtra la tabla de memorias según el perfil global seleccionado. Se llena a partir de los perfiles globales activos de la radio. |
| Tabla de memorias | Muestra únicamente las filas cuyo grupo coincide con el perfil seleccionado mientras el filtro está activo. |

## Consejos

- El filtrado por perfil y la búsqueda por nombre (`Search:`) funcionan en conjunto. Puede seleccionar un perfil en `Profile:` y escribir en `Search:` para reducir aún más los resultados por nombre de memoria.
- El botón `Export...` respeta el filtro de perfil activo: solo se exportan las memorias visibles bajo el filtro activo.

## Relacionado

- [Descripción general de Memory Channels](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Exportar memorias para respaldo o uso compartido](export-memories-for-backup-or-sharing.md)
