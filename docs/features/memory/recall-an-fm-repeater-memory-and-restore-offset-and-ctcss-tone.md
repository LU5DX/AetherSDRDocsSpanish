# Recuperar una memoria de repetidor FM y restaurar el desfase y el tono CTCSS

Abra una memoria guardada de repetidor FM y sintonice el slice activo en ella, restaurando en una sola operación la frecuencia de recepción almacenada, la dirección del desfase de transmisión, el desfase del repetidor y el valor del tono CTCSS.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Memory Channels requiere una conexión activa con el radio.
- La memoria del repetidor ya debe existir en la tabla de memorias con sus columnas FM TX Offset Dir, Repeater Offset, Tone Mode y Tone Value completadas. Si no es así, consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md) y [Editar el nombre, modo o desfase de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md).
- Al menos un slice debe estar activo en el radio.

## Pasos

1. Abra `Settings > Memory...`.
2. Localice la memoria del repetidor. Si la lista es larga, escriba parte del nombre de la memoria en el campo **Search:** y presione Enter para filtrar la tabla.
3. Haga clic en la fila de la memoria del repetidor para seleccionarla.
4. Haga clic en **Tune**.

El slice activo se sintoniza en la frecuencia almacenada. El radio restaura el modo, FM TX Offset Dir, Repeater Offset, Tone Mode y Tone Value desde la fila de la memoria.

Alternativamente, haga doble clic en la fila para sintonizar sin usar el botón **Tune**.

## Qué hace cada control

| Control                           | Propósito                                                                                                     | Notas                                                                                          |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| **Search:**                       | Filtra la tabla por nombre de memoria.                                                                        | Tiene un botón de borrar; presione Enter para saltar a la primera coincidencia. Ctrl+F enfoca el campo de búsqueda. |
| **Profile:**                      | Limita la tabla a las memorias que pertenecen al perfil global o de transmisión seleccionado.                 | Recoge nombres de perfiles de los perfiles globales de RadioModel y de los perfiles de transmisión. |
| **Tabla de memorias — FM TX Offset Dir** | Almacena la dirección del desfase de transmisión (ej. menos, más, simplex).                                         | Columna 7 en la tabla. Se restaura al sintonizar.                                             |
| **Tabla de memorias — Repeater Offset**  | Almacena la frecuencia de desfase en MHz.                                                                         | Columna 8 en la tabla. Se restaura al sintonizar.                                             |
| **Tabla de memorias — Tone Mode**        | Almacena el modo CTCSS/DCS (ej. codificación de tono CTCSS).                                                         | Columna 9 en la tabla. Se restaura al sintonizar.                                             |
| **Tabla de memorias — Tone Value**       | Almacena la frecuencia del tono CTCSS o el código DCS.                                                                | Columna 10 en la tabla. Se restaura al sintonizar.                                             |
| **Import...**                     | Importa memorias desde un archivo CSV con un cuadro de diálogo de progreso.                                      | Muestra el progreso de la importación y un resumen con las filas omitidas.                     |
| **Export...**                     | Exporta las memorias seleccionadas (o filtradas) a CSV.                                                             | Valida el CSV generado antes de guardarlo.                                                      |
| **Add**                           | Crea una nueva memoria a partir del slice activo (actual).                                                       | Atajo Ctrl+N. Se eliminó la variante de la insignia de letra del slice; agregar siempre apunta al slice activo. |
| **Edit**                          | Activa el modo de edición en línea en el campo Name de la memoria seleccionada.                                                | F2 o Ctrl+E también activa la edición. Solo está habilitado cuando está seleccionada exactamente una memoria.          |
| **Tune**                          | Sintoniza el slice activo en la memoria seleccionada, restaurando todos los campos almacenados.                                 | Debe estar seleccionada una fila. Hacer doble clic en una fila tiene el mismo efecto.                          |
| **Select All**                    | Selecciona todas las filas visibles (respetando la búsqueda/filtro).                                                       | Atajo Ctrl+Shift+A.                                                                             |
| **Remove**                        | Elimina las memorias seleccionadas (con confirmación). Muestra el progreso para la eliminación por lotes.                            | La tecla Supr/Retroceso también activa la acción. La etiqueta del botón cambia a 'Remove Selected' cuando hay >1 fila seleccionada. |
| Barra de título — Memory Channels         | Barra de título sin marco con degradado de 18 px, un glifo de agarre a la izquierda y el título del cuadro de diálogo.                        | Añadido en v26.5.1 (#2509). Utiliza FramelessWindowTitleBar; redimensionamiento en 8 ejes mediante FramelessResizer. |
| — (Minimizar)                      | Minimiza el cuadro de diálogo.                                                                                       |                                                                                                |
| □ (Maximizar)                      | Maximiza o restaura el cuadro de diálogo.                                                                           |                                                                                                |
| × (Cerrar)                         | Cierra el cuadro de diálogo. Escape primero borra la búsqueda, luego cierra.                                                 |                                                                                                |
| Arrastrar para mover               | Haga clic y arrastre la barra de título para mover el cuadro de diálogo.                                                            | Haga doble clic en la barra de título para alternar entre maximizar y restaurar.                                      |
| Redimensionamiento en 8 ejes               | Haga clic y arrastre cualquier borde o esquina del cuadro de diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. | Zona de redimensionamiento de 12 px mediante FramelessResizer.                                                 |
| Recuento de selección               | Muestra '<N> de <M> seleccionados'.                                                                                |                                                                                                |

## Consejos

- Si sus memorias de repetidor están mezcladas con otras entradas, use **Profile:** para filtrar por un grupo dedicado a repetidores, de modo que la fila objetivo sea más fácil de encontrar.
- Puede ordenar la tabla por cualquier columna ordenable — por ejemplo, Frequency — haciendo clic en el encabezado de la columna. Esto puede ayudarle a encontrar un repetidor por su frecuencia de salida. Consulte [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md).
- Presione Ctrl+Shift+A para seleccionar rápidamente todas las memorias visibles que coincidan con su búsqueda o filtro de perfil.
- Presione Ctrl+N para agregar una nueva memoria desde el slice activo sin usar el ratón.

## Solución de problemas

- **Tune está atenuado** — No hay ninguna fila seleccionada. Primero haga clic en una fila de la tabla de memorias y luego haga clic en **Tune**.
- **El desfase o el tono del repetidor no se aplican después de sintonizar** — Las columnas FM TX Offset Dir, Repeater Offset, Tone Mode o Tone Value pueden estar vacías para esa memoria. Seleccione la fila, haga clic en **Edit**, complete las columnas faltantes y sintonice de nuevo. Consulte [Editar el nombre, modo o desfase de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md).
- **La memoria esperada no aparece en la tabla** — Verifique el filtro **Profile:**. Si está seleccionado un perfil distinto al que contiene la memoria del repetidor, la fila estará oculta. Establezca **Profile:** en el perfil correcto o borre el filtro.
- **El botón Add no crea la memoria esperada** — El botón **Add** ahora siempre apunta al slice activo. Asegúrese de que el slice correcto esté activo antes de hacer clic en Add.

## Relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Editar el nombre, modo o desfase de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar el radio en una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
- [Importar memorias desde CSV](import-memories-from-csv.md)
- [Exportar memorias a CSV](export-memories-to-csv.md)
- [Eliminar memorias](remove-memories.md)
