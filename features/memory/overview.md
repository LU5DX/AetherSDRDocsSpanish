# Descripción general de los canales de memoria

El diálogo Memory Channels le permite almacenar, organizar y recuperar frecuencias en su FLEX-8600. Úselo para guardar una frecuencia junto con su modo, filtro, tono y configuración de desplazamiento asociados, de modo que pueda volver a sintonizarla al instante sin necesidad de volver a introducir los valores.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El diálogo requiere una conexión de radio activa.

## Cómo funciona

Abra el diálogo con `Settings > Memory...`. El diálogo muestra una tabla con todos los canales de memoria almacenados. Puede filtrar lo que se muestra, agregar nuevas memorias, editar las existentes, sintonizar el slice activo a cualquier memoria almacenada, e importar o exportar la lista para respaldo o compartir.

**Filtrar la tabla**

El campo Search y el cuadro combinado Profile trabajan juntos para acotar la tabla. Al escribir en Search, las filas se filtran por nombre de memoria a medida que escribe; al presionar Enter se activa la fila resaltada en ese momento. El cuadro combinado Profile filtra las filas según el perfil global activo. Cualquiera de los dos filtros puede usarse de forma independiente o en conjunto.

**La tabla de memorias**

Cada fila corresponde a una memoria almacenada. La tabla admite selección de múltiples filas (Shift-clic para un rango; Ctrl-clic o Command-clic en macOS para agregar o quitar filas individuales). Hacer doble clic en una fila sintoniza el slice activo a esa memoria. Hacer clic en el encabezado de una columna ordena la tabla por esa columna; hacer clic de nuevo invierte el orden.

La tabla contiene las siguientes columnas:

| Columna | Qué almacena |
|---|---|
| Group | Nombre del grupo o categoría |
| Owner | Etiqueta del propietario |
| Frequency | Frecuencia almacenada (MHz) |
| Name | Nombre de la memoria |
| Mode | Modo de operación (p. ej., USB, CW, FM) |
| Step | Paso de sintonía |
| FM TX Offset Dir | Dirección del desplazamiento del repetidor FM |
| Repeater Offset | Valor del desplazamiento del repetidor |
| Tone Mode | Modo de tono CTCSS/DCS |
| Tone Value | Frecuencia o código del tono |
| Squelch | Indicador de silenciador activado |
| Squelch Level | Nivel umbral del silenciador |
| RX Filter Low | Borde inferior del filtro de recepción |
| RX Filter High | Borde superior del filtro de recepción |
| RTTY Mark | Frecuencia de marca RTTY |
| RTTY Shift | Desplazamiento RTTY |
| DIGL Offset | Desplazamiento digital inferior |
| DIGU Offset | Desplazamiento digital superior |

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Search | Filtra las filas de la tabla por nombre de memoria. Tiene un botón para limpiar el campo. Presione Enter para activar la fila resaltada. |
| Profile | Filtra las filas de la tabla según el perfil global activo. |
| Memory table | Muestra y edita todas las memorias almacenadas. Admite selección de múltiples filas y edición en línea mediante teclado. |
| Add | Crea una nueva memoria en la frecuencia VFO actual. |
| Edit | Activa el modo de edición en línea en la fila de memoria seleccionada. |
| Tune | Sintoniza el slice activo a la memoria seleccionada. |
| Select All | Selecciona todas las filas de la tabla. |
| Import... | Importa memorias desde un archivo. |
| Export... | Exporta las memorias seleccionadas a un archivo. |
| Remove | Elimina las memorias seleccionadas tras una confirmación. |
| Selection count | Muestra el número de filas seleccionadas actualmente como `<N> selected`. |

Ninguno de estos controles guarda configuraciones en claves de AppSettings; todos los datos de memoria se almacenan en el radio.

## Consejos

- Hacer doble clic en una fila es un atajo para Tune: sintoniza el slice activo a esa memoria sin necesidad de usar el botón Tune.
- Use el cuadro combinado Profile junto con Export... para exportar únicamente las memorias pertenecientes a un grupo específico.
- El nombre del archivo de exportación se genera automáticamente usando la fecha actual y la versión de AetherSDR, y se guarda de forma predeterminada en la carpeta Documents.

## Relacionado

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Editar el nombre, modo u offset de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar el radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Eliminar una o varias memorias](delete-one-or-more-memories.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Exportar memorias para respaldo o compartir](export-memories-for-backup-or-sharing.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
