# Filtrar memorias por perfil

Use el filtro `Profile:` en el diálogo Memory Channels para reducir la tabla de memorias a las entradas que pertenecen a un único perfil global. Esto es útil cuando tiene una lista extensa de memorias y desea ver solo los canales relevantes para un contexto operativo particular.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Memory Channels requiere una conexión activa con la radio.
- Debe existir al menos un perfil global en la radio. Los perfiles se administran en `Profiles > Profile Manager...`.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Localice el menú desplegable `Profile:` en la parte superior del diálogo, a la derecha del campo `Search:`.
3. Haga clic en el menú desplegable `Profile:` y seleccione el perfil por el que desea filtrar.

La tabla de memorias se actualiza de inmediato para mostrar solo las memorias cuyo grupo coincide con el perfil seleccionado. Las memorias pertenecientes a otros perfiles quedan ocultas, pero no se eliminan.

4. Para quitar el filtro y mostrar todas las memorias, abra el menú desplegable `Profile:` y seleccione la entrada en blanco o la entrada de todos los perfiles.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| `Profile:` (cuadro combinado) | Filtra la tabla de memorias para mostrar solo las memorias asociadas al perfil global seleccionado. Si no se selecciona ningún perfil (entrada en blanco), se muestran todas las memorias. |
| `Search:` (campo de texto) | Aplica un filtro adicional sobre la tabla ya filtrada, por nombre de memoria. Ambos filtros se aplican de forma simultánea. |

## Consejos

- Los filtros `Search:` y `Profile:` se combinan. Puede seleccionar primero un perfil y luego escribir en el campo `Search:` para reducir aún más los resultados dentro de ese perfil.
- El botón `Export...` respeta el filtro de perfil activo. Si exporta mientras hay un perfil seleccionado, se exportarán únicamente las memorias visibles en ese momento en la tabla.

## Relacionado

- [Descripción general de Memory Channels](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Exportar memorias para respaldo o uso compartido](export-memories-for-backup-or-sharing.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
