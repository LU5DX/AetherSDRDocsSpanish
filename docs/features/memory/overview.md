# Resumen de Canales de Memoria

El cuadro de diálogo Canales de Memoria le permite almacenar, organizar y recuperar frecuencias de radio junto con sus parámetros de operación asociados. Úselo para crear una biblioteca de repetidores, frecuencias de red, puntos DX o cualquier frecuencia que sintonice regularmente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El cuadro de diálogo requiere una conexión activa con la radio.

## Cómo funciona

Abra el cuadro de diálogo con `Settings > Memory...`. El cuadro de diálogo muestra todas las memorias almacenadas en la radio en una tabla desplazable. Desde aquí puede agregar nuevas memorias, editar las existentes, sintonizar una frecuencia almacenada o administrar su lista de memorias en bloque.

**Filtrado y búsqueda**

La parte superior del cuadro de diálogo proporciona dos filtros que funcionan en conjunto. El campo Search: reduce la tabla a las filas cuyo nombre coincida con el texto que escriba; presione Enter o use el botón de borrar para restablecerlo. El cuadro combinado Profile: filtra por el perfil global o de transmisión actualmente activo. Ambos filtros se aplican simultáneamente.

**La tabla de memorias**

Cada fila representa una memoria almacenada. Las columnas son:

| Columna                    | Qué almacena                                                                                               | Notas                                                                                                |
|----------------------------|------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| Group                      | Nombre del grupo organizativo                                                                              |                                                                                                      |
| Owner                      | Etiqueta de propietario                                                                                    |                                                                                                      |
| Frequency                  | Frecuencia almacenada en MHz                                                                               |                                                                                                      |
| Name                       | Etiqueta de la memoria                                                                                     |                                                                                                      |
| Mode                       | Modo de operación (p. ej., USB, FM, CW)                                                                    | Se edita con un cuadro combinado desplegable con valores de modo conocidos                           |
| Step                       | Paso de sintonización                                                                                      | Se edita con un cuadro combinado desplegable con valores de paso conocidos                           |
| FM TX Offset Dir           | Dirección del desplazamiento del repetidor FM                                                              | Se edita con un cuadro combinado desplegable                                                        |
| Repeater Offset            | Desplazamiento del repetidor en MHz                                                                        |                                                                                                      |
| Tone Mode                  | Modo de tono CTCSS/DCS                                                                                     | Se edita con un cuadro combinado desplegable                                                        |
| Tone Value                 | Frecuencia o código de tono                                                                                | Se edita con un cuadro combinado desplegable                                                        |
| Squelch                    | Squelch activado/desactivado                                                                               |                                                                                                      |
| Squelch Level              | Nivel de umbral del squelch                                                                                |                                                                                                      |
| RX Filter Low              | Borde inferior del filtro de recepción en Hz                                                               |                                                                                                      |
| RX Filter High             | Borde superior del filtro de recepción en Hz                                                               |                                                                                                      |
| RTTY Mark                  | Frecuencia de marca RTTY                                                                                   |                                                                                                      |
| RTTY Shift                 | Desplazamiento RTTY                                                                                        |                                                                                                      |
| DIGL Offset                | Desplazamiento digital de banda lateral inferior                                                           |                                                                                                      |
| DIGU Offset                | Desplazamiento digital de banda lateral superior                                                           |                                                                                                      |

La tabla admite ordenación al hacer clic en los encabezados de columna (Frequency, Name, Mode). Al editar un campo restringido (Mode, Step, Offset Dir, Tone Mode, Tone Value, Group) con doble clic en la celda, se abre un cuadro combinado inmediatamente. Para los campos estrictos, el cuadro combinado está bloqueado a los valores conocidos; los campos editables sugieren valores comunes pero aceptan entrada de texto (validada por la radio al confirmar). La lista se abre de inmediato, de modo que elegir un valor es efectivamente un solo clic una vez que se está editando la celda.

**Acciones**

| Botón        | Qué hace                                                                                                   | Notas                                                                                                |
|--------------|------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| Import...    | Importa memorias desde un archivo CSV con cuadro de diálogo de progreso.                                   | Muestra el progreso de la importación y un resumen con las filas omitidas.                           |
| Export...    | Exporta las memorias seleccionadas (o filtradas) a CSV.                                                    | Valida el CSV generado antes de guardarlo.                                                           |
| Add          | Crea una nueva memoria a partir de la slice (segmento) activa actual: sin selección por letra.             | La variante con insignia de letra de slice se eliminó; agregar siempre apunta a la slice activa. Atajo Ctrl+N. |
| Edit         | Activa el modo de edición en línea en el campo Name de la memoria seleccionada.                            | F2 o Ctrl+E también activan la edición. Solo se habilita cuando está seleccionada exactamente una memoria. |
| Tune         | Sintoniza la slice activa a la memoria seleccionada.                                                       | Solo se habilita cuando está seleccionada exactamente una memoria.                                   |
| Select All   | Selecciona todas las filas visibles (respetando búsqueda/filtro).                                          | Atajo Ctrl+Shift+A.                                                                                  |
| Remove       | Elimina las memorias seleccionadas (con confirmación). Muestra progreso para la eliminación en lote.       | La tecla Delete/Backspace también lo activa. La etiqueta del botón cambia a 'Remove Selected' cuando hay más de 1 fila seleccionada. |

**Barra de título de la ventana**

El cuadro de diálogo usa una barra de título personalizada de 18 píxeles sin marco con degradado en la franja superior. La barra de título muestra el nombre del cuadro de diálogo "Memory Channels" con un glifo de agarre a la izquierda. Haga clic y arrastre la barra de título para mover el cuadro de diálogo. Haga doble clic en la barra de título para alternar entre los estados maximizado y restaurado. La barra de título está separada del manejo de redimensionamiento, por lo que el agarre de la barra de título no es capturado por la zona de redimensionamiento de la ventana.

**Controles de ventana**

| Control       | Qué hace                                                                                                   | Notas                                                         |
|---------------|------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------|
| — (Minimize)  | Minimiza el cuadro de diálogo.                                                                             |                                                               |
| □ (Maximize)  | Maximiza o restaura el cuadro de diálogo.                                                                  |                                                               |
| × (Close)     | Cierra el cuadro de diálogo. Escape borra primero el campo de búsqueda y luego cierra el cuadro de diálogo.|                                                               |

**Redimensionamiento**

Haga clic y arrastre cualquier borde o esquina del cuadro de diálogo para redimensionarlo. El cursor cambia para indicar la dirección del redimensionamiento. La zona de impacto de redimensionamiento tiene 12 píxeles de ancho. La zona de redimensionamiento del borde superior está parcialmente reservada para la función de movimiento de la barra de título; haga clic y arrastre en la barra de título para mover el cuadro de diálogo.

**Conteo de selección**

El indicador en la parte inferior derecha de la fila de botones muestra cuántas filas están actualmente seleccionadas, con el formato `<N> de <M> seleccionadas`.

## Geometría persistente

El cuadro de diálogo guarda y restaura su posición y tamaño entre sesiones usando una configuración de geometría persistente con clave "MemoryDialogGeometry". El cuadro de diálogo se abre en su última ubicación y tamaño conocidos.

## Soporte de temas

La tabla de memorias usa estilos basados en el tema. El color de fondo alterno de las filas y el color de resaltado de la fila seleccionada provienen del tema activo. Para cambiar estos colores, modifique la configuración del contenedor `dialog/memory` del tema.

## Consejos

- El campo Search: tiene un botón de borrar en el lado derecho; haga clic en él para eliminar el filtro sin borrar la selección de Profile:.
- Presione Ctrl+F para enfocar directamente el campo Search:.
- Ordenar y filtrar no elimina ni reordena las memorias en la radio; solo cambian lo que es visible en la tabla.
- Al editar un campo restringido, el cuadro combinado se abre automáticamente para seleccionar con un clic. Los campos editables aceptan entrada de texto validada por la radio.
- Haga doble clic en cualquier fila para sintonizar la radio a esa memoria.
- La tabla usa ExtendedSelection; mantenga presionada Ctrl o Shift y haga clic para seleccionar varias filas, o presione Ctrl+Shift+A para seleccionar todas las filas visibles.
- Presione Delete o Backspace para eliminar las filas seleccionadas sin usar el botón Remove.

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
