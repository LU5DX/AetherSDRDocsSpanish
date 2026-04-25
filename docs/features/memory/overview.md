# Descripción general de los canales de memoria

El cuadro de diálogo de canales de memoria almacena, organiza y recupera frecuencias junto con sus parámetros de operación asociados. Úselo para crear una lista de canales personal, sintonizar la radio rápidamente en una frecuencia guardada, o intercambiar datos de memoria con otros operadores.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El cuadro de diálogo requiere una conexión de radio activa.

## Cómo funciona

Abra el cuadro de diálogo con `Settings > Memory...`. El cuadro de diálogo muestra una tabla con todas las memorias almacenadas en la radio. Puede filtrar, ordenar, agregar, editar, sintonizar y eliminar memorias, o moverlas hacia y desde archivos.

Cada fila de memoria contiene un conjunto completo de parámetros de operación. Las columnas de la tabla son:

| Columna | Qué almacena |
|---|---|
| Group | Categoría o nombre de grupo para la memoria |
| Owner | Etiqueta de propietario para la memoria |
| Frequency | Frecuencia de recepción en MHz |
| Name | Etiqueta asignada por el usuario |
| Mode | Modo de operación (p. ej., USB, CW, FM) |
| Step | Tamaño del paso de sintonización |
| FM TX Offset Dir | Dirección del desplazamiento de transmisión FM |
| Repeater Offset | Valor del desplazamiento del repetidor FM |
| Tone Mode | Modo de tono CTCSS/DCS |
| Tone Value | Frecuencia o código de tono |
| Squelch | Squelch habilitado o deshabilitado |
| Squelch Level | Nivel de umbral del squelch |
| RX Filter Low | Borde inferior del filtro de recepción |
| RX Filter High | Borde superior del filtro de recepción |
| RTTY Mark | Frecuencia de marca RTTY |
| RTTY Shift | Valor de desplazamiento RTTY |
| DIGL Offset | Desplazamiento de banda lateral inferior digital |
| DIGU Offset | Desplazamiento de banda lateral superior digital |

Haga clic en cualquier encabezado de columna ordenable para ordenar la tabla. Haga clic en el mismo encabezado nuevamente para invertir el orden.

Al hacer doble clic en una fila, se sintoniza el slice activo en esa memoria de inmediato.

## Qué hace cada control

| Control | Qué hace |
|---|---|
| Search: | Filtra la tabla para mostrar las filas cuyo nombre coincide con el texto escrito. Tiene un botón para borrar; presione Enter para confirmar. |
| Profile: | Filtra la tabla para mostrar las memorias pertenecientes al perfil global seleccionado. |
| Memory table | Muestra todas las memorias que coinciden con el filtro actual. Admite selección de rango con Shift-clic y alternancia de filas individuales con Ctrl-clic (Command-clic en macOS). |
| Add | Crea una nueva memoria usando la frecuencia y configuración actuales del VFO. |
| Edit | Activa el modo de edición en línea sobre la fila de memoria seleccionada. |
| Tune | Sintoniza el slice activo en la memoria seleccionada. |
| Select All | Selecciona todas las filas en la vista filtrada actual. |
| Import... | Importa memorias desde un archivo hacia la radio. |
| Export... | Exporta las memorias seleccionadas a un archivo. |
| Remove | Elimina las memorias seleccionadas tras solicitar confirmación. |
| Selection count | Muestra cuántas filas están seleccionadas actualmente (se muestra como `N selected`). |

## Consejos

- Para encontrar una memoria rápidamente, presione el atajo estándar de búsqueda de su plataforma: el cursor salta a Search: y selecciona cualquier texto existente.
- Para agregar una nueva memoria desde el teclado, presione el atajo estándar de nuevo elemento de su plataforma mientras el cuadro de diálogo está abierto.
- Los nombres de los archivos exportados incluyen la fecha, la hora y el número de versión de AetherSDR, y se guardan en la carpeta Documentos de manera predeterminada.

## Temas relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Editar el nombre, modo u offset de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar la radio en una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Exportar memorias para respaldo o compartir](export-memories-for-backup-or-sharing.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
