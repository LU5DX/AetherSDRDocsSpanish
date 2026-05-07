# Resumen de Canales de Memoria

El diálogo Canales de Memoria le permite almacenar, organizar y recuperar frecuencias de radio junto con sus parámetros de operación asociados. Úselo para construir una biblioteca de repetidores, frecuencias de red, puntos DX o cualquier frecuencia que sintonice regularmente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo requiere una conexión de radio activa.

## Cómo funciona

Abra el diálogo con `Settings > Memory...`. El diálogo muestra todas las memorias almacenadas en la radio en una tabla desplazable. Desde aquí puede agregar nuevas memorias, editar las existentes, sintonizar una frecuencia almacenada o administrar su lista de memorias de forma masiva.

**Filtrado y búsqueda**

La parte superior del diálogo proporciona dos filtros que funcionan juntos. El campo Search: reduce la tabla a las filas cuyo nombre coincide con el texto que escribe; presione Enter o use el botón de borrar para restablecerlo. El cuadro combinado Profile: filtra por el perfil global actualmente activo. Ambos filtros se aplican simultáneamente.

**La tabla de memorias**

Cada fila representa una memoria almacenada. Las columnas son:

| Columna | Qué almacena |
|---|---|
| Group | Nombre del grupo organizativo |
| Owner | Etiqueta de propietario |
| Frequency | Frecuencia almacenada en MHz |
| Name | Etiqueta de la memoria |
| Mode | Modo de operación (ej. USB, FM, CW) |
| Step | Paso de sintonía |
| FM TX Offset Dir | Dirección de offset del repetidor FM |
| Repeater Offset | Offset del repetidor en MHz |
| Tone Mode | Modo de tono CTCSS/DCS |
| Tone Value | Frecuencia o código de tono |
| Squelch | Silenciador activado/desactivado |
| Squelch Level | Nivel de umbral del silenciador |
| RX Filter Low | Borde inferior del filtro de recepción en Hz |
| RX Filter High | Borde superior del filtro de recepción en Hz |
| RTTY Mark | Frecuencia de marca RTTY |
| RTTY Shift | Desplazamiento RTTY |
| DIGL Offset | Offset digital de banda lateral inferior |
| DIGU Offset | Offset digital de banda lateral superior |

Haga clic en un encabezado de columna para ordenar por esa columna. Haga clic de nuevo para invertir el orden de clasificación. Se pueden seleccionar varias filas usando Mayús+clic para un rango o Ctrl+clic (Comando+clic en macOS) para agregar o eliminar filas individuales. Al hacer doble clic en una fila, se sintoniza el slice activo en esa memoria inmediatamente.

**Botones**

| Botón | Qué hace |
|---|---|
| Add | Crea una nueva memoria en la frecuencia VFO actual. |
| Edit | Activa el modo de edición en línea en la fila de memoria seleccionada. |
| Tune | Sintoniza el slice activo en la memoria seleccionada. |
| Select All | Selecciona todas las filas de la tabla. |
| Import... | Importa memorias desde un archivo. |
| Export... | Exporta las memorias seleccionadas a un archivo. |
| Remove | Elimina las memorias seleccionadas después de pedir confirmación. |

El indicador de recuento de selección en la parte inferior derecha de la fila de botones muestra cuántas filas están seleccionadas actualmente.

## Consejos

- El campo Search: tiene un botón de borrar en el lado derecho; haga clic en él para eliminar el filtro sin borrar la selección de Profile:.
- La clasificación y el filtrado no eliminan ni reordenan las memorias en la radio; solo cambian lo que es visible en la tabla.

## Relacionados

- [Add a memory at current frequency](add-a-memory-at-current-frequency.md)
- [Edit a memory's name, mode or offset inline](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Tune the radio to a stored memory](tune-the-radio-to-a-stored-memory.md)
- [Delete one or more memories](delete-one-or-more-memories.md)
- [Search memories by name](search-memories-by-name.md)
- [Filter memories by profile](filter-memories-by-profile.md)
- [Import memories from a CSV/JSON file](import-memories-from-a-csv-json-file.md)
- [Export memories for backup or sharing](export-memories-for-backup-or-sharing.md)
- [Sort memory table by column header](sort-memory-table-by-column-header.md)
- [Recall an FM repeater memory and restore offset and CTCSS tone](recall-an-fm-repeater-memory-and-restore-offset-and-ctcss-tone.md)
