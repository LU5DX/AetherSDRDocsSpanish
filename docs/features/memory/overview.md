# Descripción general de los canales de memoria

El diálogo Memory Channels le permite almacenar, organizar y recuperar frecuencias en su radio Flex. Úselo para guardar frecuencias de uso frecuente junto con sus ajustes de modo, filtro y repetidor, y luego sintonice cualquier slice a una memoria almacenada con un solo clic.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. Memory Channels requiere una conexión de radio activa.

## Cómo funciona

Abra el diálogo en `Settings > Memory...`. El diálogo muestra una tabla con todas las memorias almacenadas en la radio. Puede filtrar la tabla, editar entradas directamente en línea, sintonizar un slice a cualquier memoria, e importar o exportar memorias como archivos.

**Filtrado y búsqueda**

El campo Search: y el cuadro combinado Profile: se encuentran sobre la tabla. Al escribir en Search: se filtra la tabla de inmediato para mostrar solo las filas cuyo nombre coincide. Al seleccionar un perfil en Profile: se restringe la tabla a las memorias que pertenecen a ese perfil global. Ambos filtros pueden estar activos al mismo tiempo.

**La tabla de memorias**

Cada fila representa una memoria almacenada. La tabla tiene 18 columnas:

| Columna | Qué almacena |
|---|---|
| Group | Nombre del grupo lógico de la memoria |
| Owner | Etiqueta de propietario |
| Frequency | Frecuencia almacenada en MHz |
| Name | Etiqueta legible por el usuario |
| Mode | Modo de operación (p. ej., USB, CW, FM) |
| Step | Paso de sintonía |
| FM TX Offset Dir | Dirección del desplazamiento del repetidor |
| Repeater Offset | Valor del desplazamiento del repetidor |
| Tone Mode | Modo de tono CTCSS/DCS |
| Tone Value | Frecuencia o código del tono |
| Squelch | Silenciador activado/desactivado |
| Squelch Level | Umbral del silenciador |
| RX Filter Low | Borde inferior del filtro de recepción |
| RX Filter High | Borde superior del filtro de recepción |
| RTTY Mark | Frecuencia de marca RTTY |
| RTTY Shift | Desplazamiento RTTY |
| DIGL Offset | Desplazamiento de banda lateral inferior digital |
| DIGU Offset | Desplazamiento de banda lateral superior digital |

Haga clic en el encabezado de una columna para ordenar por esa columna. Haga clic de nuevo para invertir el orden.

La tabla admite selección extendida: Shift-clic selecciona un rango; Ctrl-clic (Command-clic en macOS) agrega o quita filas individuales. Hacer doble clic en una fila sintoniza el slice activo a esa memoria de inmediato.

**Botones**

| Botón | Qué hace |
|---|---|
| Add | Crea una nueva memoria usando la frecuencia y los ajustes actuales del VFO. |
| Edit | Activa el modo de edición en línea en la fila de memoria seleccionada. |
| Tune | Sintoniza el slice activo a la memoria seleccionada. |
| Select All | Selecciona todas las filas de la tabla. |
| Import... | Importa memorias desde un archivo a la radio. |
| Export... | Exporta las memorias seleccionadas a un archivo. |
| Remove | Elimina las memorias seleccionadas tras una confirmación. |

**Contador de selección**

El indicador a la izquierda de Remove muestra cuántas filas están seleccionadas actualmente, en el formato `<N> selected`.

## Relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Editar el nombre, modo u offset de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar la radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Exportar memorias para respaldo o compartir](export-memories-for-backup-or-sharing.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
