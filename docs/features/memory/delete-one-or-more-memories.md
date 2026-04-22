# Eliminar uno o más canales de memoria

Use esta página para eliminar de forma permanente uno o más canales de memoria almacenados en su radio. La eliminación requiere una radio conectada y no se puede deshacer.

## Antes de comenzar

- AetherSDR debe estar conectado a su FLEX-8600. Memory Channels requiere una conexión de radio activa.
- Identifique los canales de memoria que desea eliminar. Use `Search:` o `Profile:` para reducir la lista si es necesario.

## Pasos

1. Abra `Settings > Memory...`.
2. En la tabla de memoria, seleccione la fila o las filas que desea eliminar.
   - Haga clic en una sola fila para seleccionarla.
   - Use Shift-click para seleccionar un rango contiguo.
   - Use Ctrl-click (Command-click en macOS) para agregar o quitar filas individuales de la selección.
   - Para eliminar todos los canales de memoria visibles, haga clic en `Select All`.
3. Confirme su selección. El indicador en la parte inferior derecha del diálogo muestra cuántas filas están seleccionadas actualmente (por ejemplo, `3 selected`).
4. Haga clic en `Remove`.
5. Confirme la eliminación cuando aparezca el diálogo de confirmación.

Los canales de memoria seleccionados se eliminan de la radio.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| `Search:` | Filtra la tabla por nombre de canal de memoria. Úselo para localizar entradas específicas antes de seleccionarlas. |
| `Profile:` | Filtra la tabla para mostrar solo los canales de memoria que pertenecen al perfil global seleccionado. |
| Tabla de memoria | Muestra todos los canales de memoria. Admite selección extendida: clic, Shift-click y Ctrl-click (Command-click en macOS). |
| `Select All` | Selecciona todas las filas visibles actualmente en la tabla. |
| Contador de selección | Muestra `<N> selected` en el área inferior derecha del diálogo, reflejando la selección actual. |
| `Remove` | Elimina todas las filas seleccionadas tras la confirmación. |

## Consejos

- Si solo desea eliminar los canales de memoria que pertenecen a un grupo, establezca `Profile:` en ese grupo primero y luego haga clic en `Select All` antes de hacer clic en `Remove`. Esto limita la selección a las filas filtradas.
- Si no está seguro de qué canales de memoria eliminar, exporte una copia de seguridad antes de borrar cualquier elemento.

## Resolución de problemas

- **`Remove` no tiene efecto o no está disponible** — Asegúrese de que al menos una fila esté seleccionada en la tabla. El botón requiere una selección activa.
- **Los canales de memoria reaparecen después de la eliminación** — Es posible que la conexión con la radio se haya interrumpido y resincronizado con datos desactualizados. Verifique el estado de su conexión e inténtelo de nuevo.

## Relacionados

- [Descripción general de Memory Channels](overview.md)
- [Buscar canales de memoria por nombre](search-memories-by-name.md)
- [Filtrar canales de memoria por perfil](filter-memories-by-profile.md)
- [Exportar canales de memoria para respaldo o intercambio](export-memories-for-backup-or-sharing.md)
