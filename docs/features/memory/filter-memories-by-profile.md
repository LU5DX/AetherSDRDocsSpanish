# Filtrar memorias por perfil

Use el filtro **Profile:** en el diálogo Memory Channels para limitar la tabla de memorias a las entradas que pertenecen a un perfil global específico. Esto es útil cuando tiene una lista de memorias extensa y desea ver únicamente las memorias asociadas a una configuración de operación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Memory Channels requiere una conexión activa con la radio.
- Debe existir al menos un perfil global en la radio. Los perfiles se cargan dinámicamente desde la radio.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Localice el cuadro combinado **Profile:** en la fila de filtros en la parte superior del diálogo.
3. Haga clic en **Profile:** y seleccione el perfil por el que desea filtrar. La tabla de memorias se actualiza de inmediato para mostrar únicamente las memorias cuyo Group coincide con el perfil seleccionado.
4. Para quitar el filtro y mostrar todas las memorias, abra nuevamente el cuadro combinado **Profile:** y seleccione la entrada en blanco o "all" al inicio de la lista.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **Profile:** | Filtra la tabla de memorias según el perfil global seleccionado. Solo se muestran las memorias cuyo Group coincide con el perfil. | Ninguno (se muestran todas las memorias) | Ninguno |
| **Search:** | Filtra la tabla por nombre de memoria. Puede usarse al mismo tiempo que el filtro de perfil. | Vacío | Ninguno |

## Consejos

- El filtro **Profile:** y el campo **Search:** funcionan de manera conjunta. Puede seleccionar un perfil y luego escribir en **Search:** para reducir los resultados dentro de ese perfil.
- El botón **Export...** respeta el filtro de perfil activo. Si exporta mientras hay un perfil seleccionado, se exportarán únicamente las memorias visibles en la vista filtrada actual.

## Relacionado

- [Descripción general de Memory Channels](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Exportar memorias para respaldo o intercambio](export-memories-for-backup-or-sharing.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
