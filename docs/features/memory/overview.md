# Resumen de Canales de Memoria

El diálogo de Canales de Memoria le permite almacenar, organizar y recuperar frecuencias de radio junto con sus parámetros operativos asociados. Úselo para crear una biblioteca de repetidores, frecuencias de red, spots de DX o cualquier frecuencia que sintonice regularmente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo requiere una conexión activa con la radio.

## Cómo funciona

Abra el diálogo con `Settings > Memory...`. El diálogo muestra todas las memorias almacenadas en la radio en una tabla desplazable. Desde aquí puede agregar nuevas memorias, editar las existentes, sintonizar una frecuencia almacenada o administrar su lista de memorias en lote.

**Filtrado y búsqueda**

La parte superior del diálogo proporciona dos filtros que funcionan juntos. El campo Search: reduce la tabla a las filas cuyo nombre coincide con el texto que escribe; presione Enter o use el botón de borrar para restablecerlo. El cuadro combinado Profile: filtra por el perfil global o de transmisión activo actualmente. Ambos filtros se aplican simultáneamente.

**La tabla de memorias**

Cada fila representa una memoria almacenada. Las columnas son:

| Columna                     | Qué almacena                                                                                               | Notas                                                                                                 |
|-----------------------------|------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Group                       | Nombre del grupo organizativo                                                                              |                                                                                                       |
| Owner                       | Etiqueta del propietario                                                                                   |                                                                                                       |
| Frequency                   | Frecuencia almacenada en MHz                                                                               |                                                                                                       |
| Name                        | Etiqueta de la memoria                                                                                     |                                                                                                       |
| Mode                        | Modo de operación (ej. USB, FM, CW)                                                                        |                                                                                                       |
| Step                        | Paso de sintonía                                                                                           |                                                                                                       |
| FM TX Offset Dir            | Dirección del desplazamiento del repetidor FM                                                              |                                                                                                       |
| Repeater Offset             | Desplazamiento del repetidor en MHz                                                                        |                                                                                                       |
| Tone Mode                   | Modo de tono CTCSS/DCS                                                                                     |                                                                                                       |
| Tone Value                  | Frecuencia o código de tono                                                                                |                                                                                                       |
| Squelch                     | Squelch activado/desactivado                                                                               |                                                                                                       |
| Squelch Level               | Nivel de umbral del squelch                                                                                |                                                                                                       |
| RX Filter Low               | Borde inferior del filtro de recepción en Hz                                                               |                                                                                                       |
| RX Filter High              | Borde superior del filtro de recepción en Hz                                                               |                                                                                                       |
| RTTY Mark                   | Frecuencia de marca RTTY                                                                                   |                                                                                                       |
| RTTY Shift                  | Desplazamiento RTTY                                                                                        |                                                                                                       |
| DIGL Offset                 | Desplazamiento digital de banda lateral inferior                                                           |                                                                                                       |
| DIGU Offset                 | Desplazamiento digital de banda lateral superior                                                           |                                                                                                       |

**Acciones**

| Botón       | Qué hace                                                                                  | Notas                                                                                                 |
|-------------|-------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Add          | Crea una nueva memoria a partir del slice activo actual (sin selección por letra).        | La variante de insignia de letra de slice se eliminó; agregar siempre apunta al slice activo. Atajo Ctrl+N. |
| Edit         | Activa el modo de edición en línea en el campo Nombre de la memoria seleccionada.         | F2 o Ctrl+E también activa la edición. Solo habilitado cuando exactamente una memoria está seleccionada. |
| Tune         | Sintoniza el slice activo a la memoria seleccionada.                                       | Solo habilitado cuando exactamente una memoria está seleccionada.                                     |
| Select All   | Selecciona cada fila visible (respetando la búsqueda/filtro).                             | Atajo Ctrl+Shift+A.                                                                                   |
| Import...    | Importa memorias desde un archivo CSV con diálogo de progreso.                            | Muestra el progreso de la importación y un resumen con las filas omitidas.                           |
| Export...    | Exporta las memorias seleccionadas (o filtradas) a CSV.                                   | Valida el CSV generado antes de guardar.                                                              |
| Remove       | Elimina las memorias seleccionadas (con confirmación). Muestra el progreso para eliminación por lotes. | La tecla Supr/Retroceso también lo activa. La etiqueta del botón cambia a 'Remove Selected' cuando >1 fila está seleccionada. |

**Barra de título de la ventana**

El diálogo utiliza una barra de título personalizada sin marco. La barra de título muestra el nombre del diálogo "Memory Channels" con un glifo de agarre a la izquierda. Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar entre los estados maximizado y restaurado.

**Controles de la ventana**

| Control       | Qué hace                                                                                  | Notas                                                          |
|---------------|-------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| — (Minimizar) | Minimiza el diálogo.                                                                       |                                                                |
| □ (Maximizar) | Maximiza o restaura el diálogo.                                                            |                                                                |
| × (Cerrar)    | Cierra el diálogo. Escape primero borra el campo de búsqueda, luego cierra el diálogo.    |                                                                |

**Redimensionamiento**

Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. La zona de impacto para redimensionar tiene 12 píxeles de ancho.

**Conteo de selección**

El indicador en la parte inferior derecha de la fila de botones muestra cuántas filas están seleccionadas actualmente, formateado como `<N> de <M> seleccionados`.

## Geometría persistente

El diálogo guarda y restaura su posición y tamaño entre sesiones utilizando una clave de geometría persistente llamada "MemoryDialogGeometry". El diálogo se abre en su última ubicación y tamaño conocidos.

## Consejos

- El campo Search: tiene un botón de borrar en el lado derecho; haga clic en él para eliminar el filtro sin borrar la selección de Profile:.
- Presione Ctrl+F para enfocar el campo Search: directamente.
- Ordenar y filtrar no elimina ni reordena las memorias en la radio; solo cambia lo que es visible en la tabla.

## Relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Editar el nombre, modo o desplazamiento de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar la radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Exportar memorias para respaldo o uso compartido](export-memories-for-backup-or-sharing.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
- [Recuperar una memoria de repetidor FM y restaurar el desplazamiento y el tono CTCSS](recall-an-fm-repeater-memory-and-restore-offset-and-ctcss-tone.md)
