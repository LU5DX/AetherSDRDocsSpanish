# Resumen de canales de memoria

El cuadro de diálogo de Canales de memoria le permite almacenar, organizar y recuperar frecuencias de radio junto con sus parámetros operativos asociados. Úselo para crear una biblioteca de repetidores, frecuencias de red, puntos DX o cualquier frecuencia que sintonice regularmente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El cuadro de diálogo requiere una conexión activa con la radio.

## Cómo funciona

Abra el cuadro de diálogo con `Settings > Memory...`. El cuadro de diálogo muestra todas las memorias almacenadas en la radio en una tabla desplazable. Desde aquí puede agregar nuevas memorias, editar las existentes, sintonizar una frecuencia almacenada o administrar su lista de memorias de forma masiva.

**Filtrado y búsqueda**

La parte superior del cuadro de diálogo proporciona dos filtros que funcionan juntos. El campo Search: reduce la tabla a las filas cuyo nombre coincide con el texto que escriba; presione Enter o use el botón de limpiar para restablecerlo. El cuadro combinado Profile: filtra por el perfil de transmisión global o activo actual. Ambos filtros se aplican simultáneamente.

**La tabla de memorias**

Cada fila representa una memoria almacenada. Las columnas son:

| Columna                    | Qué almacena                                                                                              | Notas                                                                                                |
|----------------------------|-----------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| Group                      | Nombre del grupo organizativo                                                                             |                                                                                                      |
| Owner                      | Etiqueta del propietario                                                                                  |                                                                                                      |
| Frequency                  | Frecuencia almacenada en MHz                                                                              |                                                                                                      |
| Name                       | Etiqueta de la memoria                                                                                    |                                                                                                      |
| Mode                       | Modo de operación (p. ej. USB, FM, CW)                                                                   |                                                                                                      |
| Step                       | Paso de sintonía                                                                                          |                                                                                                      |
| FM TX Offset Dir           | Dirección del offset del repetidor FM                                                                     |                                                                                                      |
| Repeater Offset            | Offset del repetidor en MHz                                                                               |                                                                                                      |
| Tone Mode                  | Modo de tono CTCSS/DCS                                                                                    |                                                                                                      |
| Tone Value                 | Frecuencia o código de tono                                                                               |                                                                                                      |
| Squelch                    | Silenciador activado/desactivado                                                                          |                                                                                                      |
| Squelch Level              | Nivel de umbral del silenciador                                                                           |                                                                                                      |
| RX Filter Low              | Borde inferior del filtro de recepción en Hz                                                              |                                                                                                      |
| RX Filter High             | Borde superior del filtro de recepción en Hz                                                              |                                                                                                      |
| RTTY Mark                  | Frecuencia de marca RTTY                                                                                  |                                                                                                      |
| RTTY Shift                 | Desplazamiento RTTY                                                                                       |                                                                                                      |
| DIGL Offset                | Offset digital de banda lateral inferior                                                                  |                                                                                                      |
| DIGU Offset                | Offset digital de banda lateral superior                                                                  |                                                                                                      |

**Acciones**

| Botón       | Qué hace                                                                                 | Notas                                                                                                |
|-------------|------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| Add         | Crea una nueva memoria a partir del slice activo actual (sin selección por letra).       | Se eliminó la variante de insignia de letra de slice; agregar siempre apunta al slice activo. Atajo Ctrl+N. |
| Edit        | Activa el modo de edición en línea en el campo Name de la memoria seleccionada.          | F2 o Ctrl+E también activan la edición. Solo se habilita cuando está seleccionada exactamente una memoria. |
| Tune        | Sintoniza el slice activo a la memoria seleccionada.                                     | Solo se habilita cuando está seleccionada exactamente una memoria.                                    |
| Select All  | Selecciona todas las filas visibles (respetando la búsqueda/filtro).                     | Atajo Ctrl+Shift+A.                                                                                   |
| Import...   | Importa memorias desde un archivo CSV con cuadro de diálogo de progreso.                 | Muestra el progreso de la importación y un resumen con las filas omitidas.                           |
| Export...   | Exporta las memorias seleccionadas (o filtradas) a CSV.                                  | Valida el CSV generado antes de guardarlo.                                                           |
| Remove      | Elimina las memorias seleccionadas (con confirmación). Muestra progreso para eliminación masiva. | La tecla Supr/Retroceso también lo activa. La etiqueta del botón cambia a 'Remove Selected' cuando hay >1 fila seleccionada. |

**Barra de título de la ventana**

El cuadro de diálogo utiliza una barra de título personalizada sin marco. La barra de título muestra el nombre del diálogo "Memory Channels" con un glifo de agarre a la izquierda. Haga clic y arrastre la barra de título para mover el cuadro de diálogo. Haga doble clic en la barra de título para alternar entre los estados maximizado y restaurado.

**Controles de la ventana**

| Control       | Qué hace                                                                                 | Notas                                                         |
|---------------|------------------------------------------------------------------------------------------|---------------------------------------------------------------|
| — (Minimizar) | Minimiza el cuadro de diálogo.                                                           |                                                               |
| □ (Maximizar) | Maximiza o restaura el cuadro de diálogo.                                                |                                                               |
| × (Cerrar)    | Cierra el cuadro de diálogo. Escape primero limpia el campo de búsqueda, luego lo cierra.|                                                               |

**Redimensionamiento**

Haga clic y arrastre cualquier borde o esquina del cuadro de diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. La zona de impacto para redimensionar tiene 12 píxeles de ancho.

**Conteo de selección**

El indicador en la parte inferior derecha de la fila de botones muestra cuántas filas están seleccionadas actualmente, con el formato `<N> of <M> selected`.

## Geometría persistente

El cuadro de diálogo guarda y restaura su posición y tamaño entre sesiones usando una configuración de geometría persistente con la clave "MemoryDialogGeometry". El cuadro de diálogo se abre en su última ubicación y tamaño conocidos.

## Soporte de temas

La tabla de memorias utiliza estilos que se adaptan al tema. El color de fondo de filas alternas y el color de resaltado de la fila seleccionada provienen del tema activo. Para cambiar estos colores, modifique la configuración del contenedor `dialog/memory` del tema.

## Consejos

- El campo Search: tiene un botón de limpiar en el lado derecho; haga clic en él para eliminar el filtro sin borrar la selección de Profile:.
- Presione Ctrl+F para enfocar directamente el campo Search:.
- La ordenación y el filtrado no eliminan ni reordenan las memorias en la radio; solo cambian lo que es visible en la tabla.

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
