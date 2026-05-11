# Resumen de Canales de Memoria

El cuadro de diálogo Canales de Memoria le permite almacenar, organizar y recuperar frecuencias de radio junto con sus parámetros operativos asociados. Úselo para construir una biblioteca de repetidores, frecuencias de red, puntos DX o cualquier frecuencia que sintonice regularmente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El cuadro de diálogo requiere una conexión activa con la radio.

## Cómo funciona

Abra el cuadro de diálogo con `Settings > Memory...`. El cuadro de diálogo muestra todas las memorias almacenadas en la radio en una tabla desplazable. Desde aquí puede agregar nuevas memorias, editar las existentes, sintonizar una frecuencia almacenada o gestionar su lista de memorias de forma masiva.

**Filtrado y búsqueda**

La parte superior del cuadro de diálogo proporciona dos filtros que funcionan juntos. El campo Search: reduce la tabla a las filas cuyo nombre coincide con el texto que escribe; presione Enter o use el botón de borrar para restablecerlo. La lista desplegable Profile: filtra según el perfil global o de transmisión activo actualmente. Ambos filtros se aplican simultáneamente.

**La tabla de memorias**

Cada fila representa una memoria almacenada. Las columnas son:

| Columna                    | Qué almacena                                                                                              | Notas                                                                                                |
|----------------------------|-----------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| Group                      | Nombre del grupo organizativo                                                                             |                                                                                                      |
| Owner                      | Etiqueta del propietario                                                                                  |                                                                                                      |
| Frequency                  | Frecuencia almacenada en MHz                                                                              |                                                                                                      |
| Name                       | Etiqueta de la memoria                                                                                    |                                                                                                      |
| Mode                       | Modo operativo (ej. USB, FM, CW)                                                                          |                                                                                                      |
| Step                       | Paso de sintonía                                                                                          |                                                                                                      |
| FM TX Offset Dir           | Dirección del desplazamiento del repetidor FM                                                             |                                                                                                      |
| Repeater Offset            | Desplazamiento del repetidor en MHz                                                                       |                                                                                                      |
| Tone Mode                  | Modo de tono CTCSS/DCS                                                                                    |                                                                                                      |
| Tone Value                 | Frecuencia o código de tono                                                                               |                                                                                                      |
| Squelch                    | Silenciador activado/desactivado                                                                          |                                                                                                      |
| Squelch Level              | Nivel de umbral del silenciador                                                                           |                                                                                                      |
| RX Filter Low              | Borde inferior del filtro de recepción en Hz                                                              |                                                                                                      |
| RX Filter High             | Borde superior del filtro de recepción en Hz                                                              |                                                                                                      |
| RTTY Mark                  | Frecuencia de marca RTTY                                                                                  |                                                                                                      |
| RTTY Shift                 | Desplazamiento RTTY                                                                                       |                                                                                                      |
| DIGL Offset                | Desplazamiento de banda lateral inferior digital                                                          |                                                                                                      |
| DIGU Offset                | Desplazamiento de banda lateral superior digital                                                          |                                                                                                      |
| Botón                      | Qué hace                                                                                                  |                                                                                                      |
| ---                        | ---                                                                                                       |                                                                                                      |
| Add                        | Crea una nueva memoria a partir del segmento (slice) activo actual -- sin selección por letra.            | Se eliminó la variante de distintivo de letra de segmento; agregar siempre se dirige al segmento activo. Atajo Ctrl+N. |
| Edit                       | Activa el modo de edición en línea en el campo Nombre de la memoria seleccionada.                         | F2 o Ctrl+E también activan la edición. Solo habilitado cuando está seleccionada exactamente una memoria. |
| Tune                       | Sintoniza el segmento activo a la memoria seleccionada.                                                   | Solo habilitado cuando está seleccionada exactamente una memoria.                                    |
| Select All                 | Selecciona todas las filas visibles (respetando la búsqueda/filtro).                                      | Atajo Ctrl+Shift+A.                                                                                 |
| Import...                  | Importa memorias desde un archivo CSV con cuadro de diálogo de progreso.                                  | Muestra el progreso de la importación y un resumen con las filas omitidas.                           |
| Export...                  | Exporta las memorias seleccionadas (o filtradas) a CSV.                                                   | Valida el CSV generado antes de guardar.                                                             |
| Remove                     | Elimina las memorias seleccionadas (con confirmación). Muestra el progreso para la eliminación por lotes. | La tecla Supr/Retroceso también lo activa. La etiqueta del botón cambia a 'Remove Selected' cuando hay más de 1 fila seleccionada. |

**Barra de título sin marco**

El cuadro de diálogo utiliza una barra de título personalizada sin marco, introducida en la v26.5.1. La barra de título muestra el nombre del cuadro de diálogo "Memory Channels" con un glifo de agarre a la izquierda. Haga clic y arrastre la barra de título para mover el cuadro de diálogo. Haga doble clic en la barra de título para alternar entre los estados maximizado y restaurado.

**Controles de ventana**

| Control        | Qué hace                                                                               | Notas                                                         |
|----------------|----------------------------------------------------------------------------------------|---------------------------------------------------------------|
| — (Minimizar)  | Minimiza el cuadro de diálogo.                                                         |                                                               |
| □ (Maximizar)  | Maximiza o restaura el cuadro de diálogo.                                              |                                                               |
| × (Cerrar)     | Cierra el cuadro de diálogo. Escape primero borra el campo de búsqueda, luego cierra el cuadro de diálogo. |                                                               |

**Redimensionamiento en 8 ejes**

Haga clic y arrastre cualquier borde o esquina del cuadro de diálogo para redimensionarlo. El cursor cambia para indicar la dirección del redimensionamiento. La zona de impacto para redimensionar es de 12 píxeles de ancho a través de FramelessResizer.

**Conteo de selección**

El indicador en la parte inferior derecha de la fila de botones muestra cuántas filas están seleccionadas actualmente, con el formato `<N> de <M> seleccionados`.

## Consejos

- El campo Search: tiene un botón de borrar en el lado derecho; haga clic en él para eliminar el filtro sin borrar la selección de Profile:.
- Presione Ctrl+F para enfocar directamente el campo Search:.
- Ordenar y filtrar no elimina ni reordena las memorias en la radio; solo cambia lo que es visible en la tabla.
- El comportamiento de ventana sin marco es el mismo que en los cuadros de diálogo SpotHub y RadioSetup. La configuración global `View > Frameless Window` controla si este cuadro de diálogo utiliza el marco sin bordes.

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
