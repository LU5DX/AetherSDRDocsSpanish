# Descripción general de los canales de memoria

El diálogo Memory Channels permite almacenar, organizar y recuperar frecuencias de radio junto con sus parámetros de operación asociados. Úselo para crear una biblioteca de repetidoras, frecuencias de red, spots de DX o cualquier frecuencia a la que sintonice con regularidad.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo requiere una conexión de radio activa.

## Cómo funciona

Abra el diálogo con `Settings > Memory...`. El diálogo muestra todas las memorias almacenadas en la radio en una tabla desplazable. Desde aquí puede agregar nuevas memorias, editar las existentes, sintonizar una frecuencia almacenada o administrar su lista de memorias de forma masiva.

**Filtrado y búsqueda**

La parte superior del diálogo ofrece dos filtros que funcionan en conjunto. El campo Search: reduce la tabla a las filas cuyo nombre coincide con el texto que escriba; presione Enter o use el botón de borrado para reiniciarlo. El cuadro combinado Profile: filtra según el perfil global activo en ese momento. Ambos filtros se aplican simultáneamente.

**La tabla de memorias**

Cada fila representa una memoria almacenada. Las columnas son:

| Columna | Qué almacena |
|---|---|
| Group | Nombre del grupo organizativo |
| Owner | Etiqueta de propietario |
| Frequency | Frecuencia almacenada en MHz |
| Name | Etiqueta de la memoria |
| Mode | Modo de operación (p. ej., USB, FM, CW) |
| Step | Paso de sintonía |
| FM TX Offset Dir | Dirección del desplazamiento de la repetidora FM |
| Repeater Offset | Desplazamiento de la repetidora en MHz |
| Tone Mode | Modo de tono CTCSS/DCS |
| Tone Value | Frecuencia o código del tono |
| Squelch | Silenciador activado/desactivado |
| Squelch Level | Nivel de umbral del silenciador |
| RX Filter Low | Borde inferior del filtro de recepción en Hz |
| RX Filter High | Borde superior del filtro de recepción en Hz |
| RTTY Mark | Frecuencia mark de RTTY |
| RTTY Shift | Desplazamiento de RTTY |
| DIGL Offset | Desplazamiento de la banda lateral inferior digital |
| DIGU Offset | Desplazamiento de la banda lateral superior digital |

Haga clic en el encabezado de una columna para ordenar por esa columna. Haga clic de nuevo para invertir el orden. Se pueden seleccionar varias filas usando Shift-clic para un rango o Ctrl-clic (Command-clic en macOS) para agregar o quitar filas individuales. Al hacer doble clic en una fila, el slice activo se sintoniza inmediatamente a esa memoria.

**Botones**

| Botón | Qué hace |
|---|---|
| Add | Crea una nueva memoria en la frecuencia actual del VFO. |
| Edit | Activa el modo de edición en línea sobre la fila de memoria seleccionada. |
| Tune | Sintoniza el slice activo a la memoria seleccionada. |
| Select All | Selecciona todas las filas de la tabla. |
| Import... | Importa memorias desde un archivo. |
| Export... | Exporta las memorias seleccionadas a un archivo. |
| Remove | Elimina las memorias seleccionadas tras pedir confirmación. |

El indicador de conteo de selección, en la parte inferior derecha de la fila de botones, muestra cuántas filas están seleccionadas en ese momento.

## Consejos

- El campo Search: tiene un botón de borrado a la derecha; haga clic en él para eliminar el filtro sin limpiar la selección de Profile:.
- Ordenar y filtrar no elimina ni reordena las memorias en la radio; solo cambia lo que es visible en la tabla.

## Relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Editar el nombre, modo u offset de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar la radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Exportar memorias para respaldo o compartir](export-memories-for-backup-or-sharing.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
- [Recuperar una memoria de repetidora FM y restaurar el offset y el tono CTCSS](recall-an-fm-repeater-memory-and-restore-offset-and-ctcss-tone.md)
