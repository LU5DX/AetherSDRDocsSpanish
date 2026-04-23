# Eliminar una o varias memorias

Use esta página para eliminar una memoria o un lote de memorias del radio. Las memorias eliminadas se borran del radio de forma permanente tras la confirmación.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Memory Channels requiere una conexión activa con el radio.
- Abra el diálogo mediante `Settings > Memory...`.

## Pasos

1. Abra `Settings > Memory...`.
2. Seleccione la memoria o memorias que desea eliminar.
   - Haga clic en una fila para seleccionarla.
   - Use Shift-clic para seleccionar un rango contiguo.
   - En Linux y Windows, use Ctrl-clic para agregar o quitar filas individuales de la selección. En macOS, use Command-clic.
   - Para seleccionar todas las filas, haga clic en **Select All**.
   - Para reducir la lista antes de seleccionar, use el campo **Search:** o el cuadro combinado **Profile:**. Consulte [Buscar memorias por nombre](search-memories-by-name.md) y [Filtrar memorias por perfil](filter-memories-by-profile.md).
3. Confirme que el contador de selección (por ejemplo, "3 selected") corresponde a su intención.
4. Haga clic en **Remove**.
5. Cuando aparezca el diálogo de confirmación, confirme la eliminación.

Las memorias seleccionadas se eliminan del radio.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Select All** | Selecciona todas las filas visibles en ese momento en la tabla. |
| **Remove** | Elimina todas las filas seleccionadas. Presenta un aviso de confirmación antes de borrar. |
| **Search:** | Filtra la tabla por nombre de memoria, reduciendo las filas disponibles para la selección. |
| **Profile:** | Filtra la tabla para mostrar solo las memorias que pertenecen al perfil global elegido. |
| Contador de selección | Muestra el número de filas seleccionadas en ese momento como "N selected". |

## Consejos

- Use **Select All** después de filtrar con **Search:** o **Profile:** para seleccionar rápidamente un subconjunto con nombre antes de hacer clic en **Remove**.
- La indicación debajo de la tabla sirve como recordatorio: "Tip: Double-click tunes. Shift-click selects a range. Ctrl-click adds or removes rows." (En macOS, Ctrl-clic aparece como Command-clic.) Úsela para construir su selección con precisión antes de eliminar.

## Solución de problemas

- **Remove no está disponible o no tiene efecto** — Debe haber al menos una fila seleccionada. Haga clic en una fila de la tabla y luego en **Remove**.
- **La memoria que desea eliminar no es visible** — Es posible que un término de búsqueda o un filtro de perfil la esté ocultando. Borre el campo **Search:** y restablezca **Profile:** a su estado sin filtro; luego localice la fila.

## Relacionado

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Exportar memorias para respaldo o uso compartido](export-memories-for-backup-or-sharing.md)
