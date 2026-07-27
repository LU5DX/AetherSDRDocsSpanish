# Resumen de canales de memoria

El diálogo de Canales de memoria le permite almacenar, organizar y recuperar frecuencias de radio junto con sus parámetros operativos asociados. Úselo para crear una biblioteca de repetidores, frecuencias de red, spots DX o cualquier frecuencia que sintonice regularmente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo requiere una conexión activa con la radio.

## Cómo funciona

Abra el diálogo con `Settings > Memory...`. El diálogo muestra todas las memorias almacenadas en la radio en una tabla desplazable. Desde aquí puede agregar nuevas memorias, editar las existentes, sintonizar una frecuencia almacenada o administrar su lista de memorias en bloque.

**Filtrado y búsqueda**

La parte superior del diálogo proporciona dos filtros que funcionan juntos. El campo Search: reduce la tabla a las filas cuyo nombre coincide con el texto que escribe; presione Enter o use el botón de borrar para restablecerlo. El cuadro combinado Profile: filtra por el perfil global o de transmisión actualmente activo. Ambos filtros se aplican simultáneamente.

**La tabla de memoria**

Cada fila representa una memoria almacenada. Las columnas son:

| Columna                     | Lo que almacena                                                                                             | Notas                                                                                                |
|-----------------------------|-------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| Group                       | Nombre del grupo organizativo                                                                               |                                                                                                      |
| Owner                       | Etiqueta del propietario                                                                                    |                                                                                                      |
| Frequency                   | Frecuencia almacenada en MHz                                                                                |                                                                                                      |
| Name                        | Etiqueta de la memoria                                                                                      |                                                                                                      |
| Mode                        | Modo operativo (p. ej., USB, FM, CW)                                                                        | Se edita usando un cuadro combinado desplegable con valores de modo conocidos                         |
| Step                        | Paso de sintonía                                                                                            | Se edita usando un cuadro combinado desplegable con valores de paso conocidos                         |
| FM TX Offset Dir            | Dirección del desplazamiento del repetidor FM                                                               | Se edita usando un cuadro combinado desplegable                                                       |
| Repeater Offset             | Desplazamiento del repetidor en MHz                                                                         |                                                                                                      |
| Tone Mode                   | Modo de tono CTCSS/DCS                                                                                      | Se edita usando un cuadro combinado desplegable                                                       |
| Tone Value                  | Frecuencia o código de tono                                                                                 | Se edita usando un cuadro combinado desplegable                                                       |
| Squelch                     | Silenciador habilitado/deshabilitado                                                                         |                                                                                                      |
| Squelch Level               | Nivel de umbral del silenciador                                                                             |                                                                                                      |
| RX Filter Low               | Borde inferior del filtro de recepción en Hz                                                                |                                                                                                      |
| RX Filter High              | Borde superior del filtro de recepción en Hz                                                                |                                                                                                      |
| RTTY Mark                   | Frecuencia de marca RTTY                                                                                    |                                                                                                      |
| RTTY Shift                  | Desplazamiento RTTY                                                                                         |                                                                                                      |
| DIGL Offset                 | Desplazamiento de banda lateral inferior digital                                                            |                                                                                                      |
| DIGU Offset                 | Desplazamiento de banda lateral superior digital                                                            |                                                                                                      |

Al editar un campo restringido (Mode, Step, Offset Dir, Tone Mode, Tone Value, Group) haciendo doble clic en la celda, se abre un cuadro combinado inmediatamente. Para los campos estrictos, el cuadro combinado está bloqueado a los valores conocidos; los campos editables sugieren valores comunes pero aún aceptan entrada escrita (validada por la radio al confirmar). La lista se abre de inmediato, por lo que seleccionar un valor es efectivamente un clic una vez que la celda está en edición.

**Acciones**

| Botón        | Qué hace                                                                                    | Notas                                                                                                |
|--------------|---------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| Add          | Crea una nueva memoria a partir del slice activo actual -- sin selección por letra.         | Se eliminó la variante de insignia de letra de slice; agregar siempre apunta al slice activo. Atajo Ctrl+N. |
| Edit         | Activa el modo de edición en línea en el campo Name de la memoria seleccionada.              | F2 o Ctrl+E también activa la edición. Solo está habilitado cuando exactamente una memoria está seleccionada.        |
| Tune         | Sintoniza el slice activo a la memoria seleccionada.                                        | Solo está habilitado cuando exactamente una memoria está seleccionada.                                                    |
| Select All   | Selecciona todas las filas visibles (respetando búsqueda/filtro).                           | Atajo Ctrl+Shift+A.                                                                               |
| Import...    | Importa memorias desde un archivo CSV con un diálogo de progreso.                           | Muestra el progreso de la importación y un resumen con las filas omitidas.                                           |
| Export...    | Exporta las memorias seleccionadas (o filtradas) a CSV.                                      | Valida el CSV generado antes de guardar.                                                               |
| Remove       | Elimina las memorias seleccionadas (con confirmación). Muestra el progreso para eliminación en lote.         | La tecla Delete/Backspace también lo activa. La etiqueta del botón cambia a 'Remove Selected' cuando hay más de 1 fila seleccionada. |

**Barra de título de la ventana**

El diálogo utiliza una barra de título personalizada sin marco. La barra de título muestra el nombre del diálogo "Memory Channels" con un glifo de agarre a la izquierda. Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar entre los estados maximizado y restaurado. La franja superior del diálogo está reservada para el manejo de movimiento de la barra de título, por lo que un agarre en la barra de título no es interceptado por la zona de cambio de tamaño de la ventana.

**Controles de la ventana**

| Control       | Qué hace                                                                                    | Notas                                                         |
|---------------|---------------------------------------------------------------------------------------------|---------------------------------------------------------------|
| — (Minimizar) | Minimiza el diálogo.                                                                        |                                                               |
| □ (Maximizar) | Maximiza o restaura el diálogo.                                                             |                                                               |
| × (Cerrar)    | Cierra el diálogo. Escape primero borra el campo de búsqueda, luego cierra el diálogo.      |                                                               |

**Cambio de tamaño**

Haga clic y arrastre cualquier borde o esquina del diálogo para cambiar su tamaño. El cursor cambia para indicar la dirección del cambio de tamaño. La zona activa de cambio de tamaño tiene 12 píxeles de ancho. La zona de cambio de tamaño del borde superior está parcialmente reservada para la funcionalidad de movimiento de la barra de título; haga clic y arrastre en la barra de título para mover el diálogo.

**Conteo de selección**

El indicador en la parte inferior derecha de la fila de botones muestra cuántas filas están seleccionadas actualmente, con el formato `<N> de <M> seleccionadas`.

## Geometría persistente

El diálogo guarda y restaura su posición y tamaño entre sesiones utilizando una configuración de geometría persistente con clave "MemoryDialogGeometry". El diálogo se abre en su última ubicación y tamaño conocidos.

## Soporte de temas

La tabla de memoria utiliza estilo sensible al tema. El color de fondo de fila alterna y el color de resaltado de fila seleccionada provienen del tema activo. Para cambiar estos colores, modifique la configuración del contenedor `dialog/memory` del tema.

## Consejos

- El campo Search: tiene un botón de borrar en el lado derecho; haga clic en él para eliminar el filtro sin borrar la selección de Profile:.
- Presione Ctrl+F para enfocar el campo Search: directamente.
- Ordenar y filtrar no eliminan ni reordenan las memorias en la radio; solo cambian lo que es visible en la tabla.
- Al editar un campo restringido, el cuadro combinado se abre automáticamente para una selección de un clic. Los campos editables aceptan entrada escrita validada por la radio.

## Relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Editar el nombre, modo o desplazamiento de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar la radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Exportar memorias para respaldo o uso compartido](export-memories-for-backup-or-sharing.md)
- [Ordenar tabla de memoria por encabezado de columna](sort-memory-table-by-column-header.md)
- [Recuperar una memoria de repetidor FM y restaurar desplazamiento y tono CTCSS](recall-an-fm-repeater-memory-and-restore-offset-and-ctcss-tone.md)
