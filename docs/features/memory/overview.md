# Descripción general de los canales de memoria

El diálogo Memory Channels permite almacenar, organizar y recuperar frecuencias de radio junto con sus ajustes de modo y filtro asociados. Úselo para crear una lista de canales personal, sintonizar rápidamente frecuencias guardadas y compartir o respaldar sus memorias mediante importación y exportación.

## Antes de comenzar

- Se requiere una conexión de radio. El diálogo no se poblará sin una conexión activa al FLEX-8600.
- Abra el diálogo mediante `Settings > Memory...`.

## Cómo funciona

AetherSDR almacena las memorias en la radio. Cada memoria contiene una frecuencia y un conjunto de parámetros operativos. Al abrir `Settings > Memory...`, el diálogo obtiene la lista de memorias actual de la radio y la muestra en una tabla. Los cambios que realice —agregar, editar o eliminar memorias— se envían a la radio de inmediato.

La tabla admite selecciones múltiples simultáneas. Use Shift-clic para seleccionar un rango y Ctrl-clic (Command-clic en macOS) para agregar o quitar filas individuales. Al hacer doble clic en cualquier fila, se sintoniza el slice activo a esa memoria directamente, sin necesidad de presionar Tune.

Puede reducir la lista usando el campo Search, el filtro Profile, o haciendo clic en el encabezado de una columna para ordenar. Estos filtros solo afectan lo que se muestra; no modifican las memorias almacenadas.

## Qué hace cada control

| Control | Función |
|---|---|
| **Search:** | Filtra la tabla para mostrar solo las memorias cuyo nombre coincide con el texto ingresado. Presione Enter para confirmar, o use el botón de borrado para restablecer. |
| **Profile:** | Filtra la tabla para mostrar solo las memorias pertenecientes al perfil global seleccionado. |
| **Memory table** | Muestra todas las memorias almacenadas. Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. Admite selección extendida (múltiples filas) y edición en línea. |
| **Add** | Crea una nueva memoria usando la frecuencia y los ajustes actuales del VFO. |
| **Edit** | Activa el modo de edición en línea en la fila de memoria seleccionada, lo que permite cambiar cualquier campo directamente en la tabla. |
| **Tune** | Sintoniza el slice activo a la frecuencia y el modo de la memoria seleccionada. |
| **Select All** | Selecciona todas las filas de la tabla. |
| **Import...** | Importa memorias desde un archivo hacia la radio. |
| **Export...** | Exporta las memorias seleccionadas a un archivo para respaldo o para compartir. |
| **Remove** | Elimina las memorias seleccionadas después de solicitar confirmación. |
| **Selection count** | Muestra el número de filas actualmente seleccionadas como `<N> selected`. |

## Consejos

- Al hacer doble clic en una fila de la tabla de memorias, se sintoniza el slice activo de inmediato, sin necesidad de presionar Tune.
- Es posible ordenar la tabla haciendo clic en los encabezados de columna. Haga clic en el mismo encabezado nuevamente para invertir el orden.
- El campo Search actualiza la tabla mientras escribe, por lo que no es necesario presionar Enter para filtrar; Enter activa la fila actualmente resaltada.

## Temas relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Editar el nombre, modo u offset de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar la radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Exportar memorias para respaldo o para compartir](export-memories-for-backup-or-sharing.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
