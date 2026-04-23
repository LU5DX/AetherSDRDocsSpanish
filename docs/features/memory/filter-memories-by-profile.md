# Filtrar memorias por perfil

Use el filtro Profile en el diálogo Memory Channels para reducir la tabla de memorias a las entradas que pertenecen a un perfil global específico. Esto es útil cuando tiene una lista de memorias extensa y desea ver solo las entradas relevantes para un contexto operativo particular.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Memory Channels requiere una conexión activa con el radio.
- Debe existir al menos un perfil global en el radio. Los perfiles se administran en `Profiles > Profile Manager...`.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Localice el cuadro combinado **Profile:** en la fila de filtros en la parte superior del diálogo.
3. Haga clic en el cuadro combinado **Profile:** y seleccione el perfil por el que desea filtrar.
4. La tabla de memorias se actualiza inmediatamente para mostrar solo las memorias cuyo Group coincida con el perfil seleccionado.
5. Para eliminar el filtro y mostrar todas las memorias, abra el cuadro combinado **Profile:** y seleccione la opción en blanco o de todas las entradas en la parte superior de la lista.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **Profile:** | Filtra la tabla de memorias según el perfil global seleccionado. Solo se muestran las memorias cuyo Group coincide con el perfil. | Sin filtro (se muestran todas las memorias) | None |
| **Search:** | Filtra la tabla por nombre de memoria. Funciona junto con el filtro de perfil: ambos filtros se aplican al mismo tiempo. | Vacío | None |

## Consejos

- El filtro **Profile:** y el campo **Search:** se acumulan. Puede seleccionar un perfil en **Profile:** y luego escribir en **Search:** para reducir aún más los resultados dentro de ese perfil.
- Si el cuadro combinado **Profile:** está vacío o contiene solo una entrada en blanco, significa que aún no se han cargado perfiles globales desde el radio. Verifique la conexión con el radio y que exista al menos un perfil en `Profiles > Profile Manager...`.

## Solución de problemas

- **El cuadro combinado Profile: está vacío** — El radio no ha reportado ningún perfil global, o AetherSDR no está conectado. Verifique el estado de la conexión y asegúrese de que existan perfiles en `Profiles > Profile Manager...`.
- **Filtrar por perfil no muestra ninguna memoria** — Es posible que las memorias del radio no tengan el campo Group configurado para coincidir con el nombre del perfil seleccionado. Edite las memorias correspondientes y establezca la columna Group con el nombre de perfil correcto.

## Relacionados

- [Descripción general de Memory Channels](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Editar el nombre, modo u offset de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
