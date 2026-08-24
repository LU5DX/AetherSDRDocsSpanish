# Recordar una memoria de repetidor FM y restaurar offset y tono CTCSS

Abra una memoria de repetidor FM guardada y sintonice el slice activo a ella, restaurando la frecuencia de recepción almacenada, la dirección del offset de transmisión, el offset del repetidor y el valor del tono CTCSS en una sola operación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Memory Channels requiere una conexión activa con la radio.
- La memoria del repetidor ya debe existir en la tabla de memorias con sus columnas FM TX Offset Dir, Repeater Offset, Tone Mode y Tone Value completadas. Si no es así, consulte [Add a memory at current frequency](add-a-memory-at-current-frequency.md) y [Edit a memory's name, mode or offset inline](edit-a-memory-s-name-mode-or-offset-inline.md).
- Al menos un slice debe estar activo en la radio.

## Pasos

1. Abra `Settings > Memory...`.
2. Localice la memoria del repetidor. Si la lista es larga, escriba parte del nombre de la memoria en el campo **Search:** y presione Enter para filtrar la tabla.
3. Haga clic en la fila de la memoria del repetidor para seleccionarla.
4. Haga clic en **Tune**.

El slice activo se sintoniza a la frecuencia almacenada. La radio restaura el modo, FM TX Offset Dir, Repeater Offset, Tone Mode y Tone Value desde la fila de memoria.

Alternativamente, haga doble clic en la fila para sintonizar sin usar el botón **Tune**.

## Función de cada control

| Control                             | Propósito                                                                                                     | Notas                                                                                       |
|-------------------------------------|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| **Search:**                         | Filtra la tabla por nombre de memoria.                                                                           | Tiene un botón de borrado; presione Enter para confirmar. Ctrl+F enfoca el campo de búsqueda.                 |
| **Profile:**                        | Reduce la tabla a las memorias pertenecientes al perfil global o de transmisión seleccionado.                         | Recopila nombres de perfiles de los perfiles globales de RadioModel y de los perfiles de transmisión.               |
| **Memory table**                    | Muestra y edita filas de memoria. Ordenable haciendo clic en los encabezados de columna (Frequency, Name, Mode). Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. | ExtendedSelection; modo de edición en línea mediante el botón Edit o F2/Ctrl+E. Delete/Backspace elimina las filas seleccionadas. Doble clic sintoniza. Ctrl+Shift+A selecciona todo. |
| **-- Memory table -- Mode**         | Selecciona entre valores de modo restringidos mediante un editor de cuadro combinado que se abre inmediatamente al entrar en modo de edición. | Usa MemoryFieldDelegate con lista desplegable bloqueada; los valores fuera de lista se conservan en la lista desplegable en lugar de intercambiarse. |
| **-- Memory table -- Step**         | Selecciona entre valores de paso comunes mediante un editor de cuadro combinado editable que se abre inmediatamente al entrar en modo de edición. | Usa MemoryFieldDelegate con lista desplegable editable; la entrada escrita es validada por la radio al confirmar. |
| **-- Memory table -- FM TX Offset Dir** | Almacena la dirección del offset de transmisión (por ejemplo, menos, más, simplex).                                          | Usa MemoryFieldDelegate con lista desplegable bloqueada. Columna 7 en la tabla. Se restaura al sintonizar. |
| **-- Memory table -- Repeater Offset**  | Almacena la frecuencia de offset en MHz.                                                                         | Usa MemoryFieldDelegate con lista desplegable editable y validador doble. Columna 8 en la tabla. Se restaura al sintonizar. |
| **-- Memory table -- Tone Mode**        | Almacena el modo CTCSS/DCS (por ejemplo, codificación de tono CTCSS).                                                        | Usa MemoryFieldDelegate con lista desplegable bloqueada. Columna 9 en la tabla. Se restaura al sintonizar. |
| **-- Memory table -- Tone Value**       | Almacena la frecuencia de tono CTCSS o el código DCS.                                                               | Usa MemoryFieldDelegate con lista desplegable editable y validador doble. Columna 10 en la tabla. Se restaura al sintonizar. |
| **-- Memory table -- Group**            | Selecciona entre nombres de grupo conocidos mediante un editor de cuadro combinado que se abre inmediatamente al entrar en modo de edición.   | Usa MemoryFieldDelegate con lista desplegable bloqueada.                                                |
| **Import...**                       | Importa memorias desde un archivo CSV con diálogo de progreso.                                                      | Muestra el progreso de la importación y un resumen con las filas omitidas.                                  |
| **Export...**                       | Exporta las memorias seleccionadas (o filtradas) a CSV.                                                             | Valida el CSV generado antes de guardarlo.                                                      |
| **Add**                             | Crea una nueva memoria desde el slice actual (activo).                                                       | Atajo Ctrl+N. La variante con insignia de letra de slice se eliminó; agregar siempre apunta al slice activo. |
| **Edit**                            | Entra en modo de edición en línea en el campo Name de la memoria seleccionada.                                                | F2 o Ctrl+E también activa la edición. Solo se habilita cuando exactamente una memoria está seleccionada.          |
| **Tune**                            | Sintoniza el slice activo a la memoria seleccionada, restaurando todos los campos almacenados.                                 | Debe seleccionarse una fila. Hacer doble clic en una fila tiene el mismo efecto.                        |
| **Select All**                      | Selecciona todas las filas visibles (respetando búsqueda/filtro).                                                       | Atajo Ctrl+Shift+A.                                                                      |
| **Remove**                          | Elimina las memorias seleccionadas (con confirmación). Muestra progreso para eliminación por lotes.                            | La tecla Delete/Backspace también lo activa. La etiqueta del botón cambia a 'Remove Selected' cuando hay más de 1 fila seleccionada. |
| Barra de título — Memory Channels         | Barra de título sin marco de 18 px con degradado, glifo de agarre a la izquierda y el título del diálogo.                        | Añadido en v26.5.1 (#2509). Usa FramelessWindowTitleBar; redimensionamiento de 8 ejes mediante FramelessResizer. |
| — (Minimize)                        | Minimiza el diálogo.                                                                                       |                                                                                             |
| □ (Maximize)                        | Maximiza o restaura el diálogo.                                                                           |                                                                                             |
| × (Close)                           | Cierra el diálogo. Escape borra la búsqueda primero, luego cierra.                                                                                                                 |                                                                                             |
| Arrastrar para mover                        | Haga clic y arrastre la barra de título para mover el diálogo.                                                            | Doble clic en la barra de título alterna maximizar/restaurar.                                      |
| Redimensionamiento de 8 ejes                       | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección del redimensionamiento. | Zona de redimensionamiento de 12 px mediante FramelessResizer. El borde superior del diálogo está reservado para el manejo de movimiento de la barra de título, por lo que arrastrar la barra de título no es interceptado por la zona de redimensionamiento. |
| Recuento de selección                     | Muestra '<N> of <M> selected'.                                                                                |                                                                                             |

## Consejos

- Si sus memorias de repetidor están mezcladas con otras entradas, use **Profile:** para filtrar por un grupo dedicado a repetidores para que la fila objetivo sea más fácil de localizar.
- Puede ordenar la tabla por cualquier columna ordenable — por ejemplo, Frequency — haciendo clic en el encabezado de columna. Esto puede ayudarle a encontrar un repetidor por su frecuencia de salida. Consulte [Sort memory table by column header](sort-memory-table-by-column-header.md).
- Presione Ctrl+Shift+A para seleccionar rápidamente todas las memorias visibles que coincidan con su búsqueda o filtro de perfil.
- Presione Ctrl+N para agregar una nueva memoria desde el slice activo sin usar el ratón.
- Al editar un campo de memoria que usa un cuadro combinado (Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Group), la lista desplegable se abre automáticamente para que pueda elegir un valor con un solo clic. Para campos editables (Step, Repeater Offset, Tone Value), también puede escribir un valor personalizado.

## Solución de problemas

- **Tune está atenuado** — No hay ninguna fila seleccionada. Haga clic en una fila de la tabla de memorias primero, luego haga clic en **Tune**.
- **El offset del repetidor o el tono no se aplican después de sintonizar** — Las columnas FM TX Offset Dir, Repeater Offset, Tone Mode o Tone Value pueden estar vacías para esa memoria. Seleccione la fila, haga clic en **Edit**, complete las columnas faltantes y sintonice nuevamente. Consulte [Edit a memory's name, mode or offset inline](edit-a-memory-s-name-mode-or-offset-inline.md).
- **La memoria esperada no aparece en la tabla** — Verifique el filtro **Profile:**. Si está seleccionado un perfil distinto al que contiene la memoria del repetidor, la fila estará oculta. Establezca **Profile:** al perfil correcto o borre el filtro.
- **El botón Add no crea la memoria esperada** — El botón **Add** ahora siempre apunta al slice activo. Asegúrese de que el slice correcto esté activo antes de hacer clic en Add.
- **Un campo de memoria muestra un valor que no está en la lista desplegable** — Los valores heredados o corruptos se conservan en la lista desplegable para que pueda verlos en lugar de que se intercambien silenciosamente. Puede editar el campo para seleccionar un valor válido.

## Relacionados

- [Add a memory at current frequency](add-a-memory-at-current-frequency.md)
- [Edit a memory's name, mode or offset inline](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Tune the radio to a stored memory](tune-the-radio-to-a-stored-memory.md)
- [Search memories by name](search-memories-by-name.md)
- [Filter memories by profile](filter-memories-by-profile.md)
- [Sort memory table by column header](sort-memory-table-by-column-header.md)
- Importar memorias desde CSV
- Exportar memorias a CSV
- Eliminar memorias
