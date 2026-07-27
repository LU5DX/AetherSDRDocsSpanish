# Recordar una memoria de repetidor FM y restaurar desplazamiento y tono CTCSS

Abra una memoria guardada de repetidor FM y sintonice el segmento activo en ella, restaurando la frecuencia de recepción almacenada, la dirección del desplazamiento de transmisión, el desplazamiento del repetidor y el valor del tono CTCSS en una sola operación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Memory Channels requiere una conexión activa con la radio.
- La memoria del repetidor ya debe existir en la tabla de memorias con sus columnas FM TX Offset Dir, Repeater Offset, Tone Mode y Tone Value completadas. Si no es así, consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md) y [Editar el nombre, modo o desplazamiento de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md).
- Al menos un segmento debe estar activo en la radio.

## Pasos

1. Abra `Settings > Memory...`.
2. Localice la memoria del repetidor. Si la lista es larga, escriba parte del nombre de la memoria en el campo **Search:** y presione Enter para filtrar la tabla.
3. Haga clic en la fila de la memoria del repetidor para seleccionarla.
4. Haga clic en **Tune**.

El segmento activo se sintoniza a la frecuencia almacenada. La radio restaura el modo, FM TX Offset Dir, Repeater Offset, Tone Mode y Tone Value desde la fila de memoria.

Alternativamente, haga doble clic en la fila para sintonizar sin usar el botón **Tune**.

## Qué hace cada control

| Control                             | Propósito                                                                                                   | Notas                                                                                       |
|-------------------------------------|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| **Search:**                         | Filtra la tabla por nombre de memoria.                                                                      | Tiene un botón de limpieza; presione Enter para confirmar. Ctrl+F enfoca el campo de búsqueda. |
| **Profile:**                        | Limita la tabla a las memorias que pertenecen al perfil global o de transmisión seleccionado.               | Reúne los nombres de perfil de los perfiles globales de RadioModel y los perfiles de transmisión. |
| **Memory table**                    | Muestra y edita filas de memoria. Ordenable haciendo clic en los encabezados de columna (Frequency, Name, Mode). Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. | ExtendedSelection; modo de edición en línea mediante el botón Edit o F2/Ctrl+E. Delete/Backspace elimina las filas seleccionadas. Doble clic sintoniza. Ctrl+Shift+A selecciona todo. |
| **-- Memory table -- Mode**         | Selecciona entre valores de modo restringidos usando un editor de cuadro combinado que se abre inmediatamente al entrar en modo de edición. | Usa MemoryFieldDelegate con lista desplegable bloqueada; los valores fuera de la lista se conservan en la lista desplegable en lugar de intercambiarse. |
| **-- Memory table -- Step**         | Selecciona entre valores de paso comunes usando un editor de cuadro combinado editable que se abre inmediatamente al entrar en modo de edición. | Usa MemoryFieldDelegate con lista desplegable editable; la entrada escrita es validada por la radio al confirmar. |
| **-- Memory table -- FM TX Offset Dir** | Almacena la dirección del desplazamiento de transmisión (ej. menos, más, simplex).                           | Usa MemoryFieldDelegate con lista desplegable bloqueada. Columna 7 en la tabla. Se restaura al sintonizar. |
| **-- Memory table -- Repeater Offset**  | Almacena la frecuencia de desplazamiento en MHz.                                                             | Usa MemoryFieldDelegate con lista desplegable editable y validador doble. Columna 8 en la tabla. Se restaura al sintonizar. |
| **-- Memory table -- Tone Mode**        | Almacena el modo CTCSS/DCS (ej. codificación de tono CTCSS).                                                | Usa MemoryFieldDelegate con lista desplegable bloqueada. Columna 9 en la tabla. Se restaura al sintonizar. |
| **-- Memory table -- Tone Value**       | Almacena la frecuencia del tono CTCSS o el código DCS.                                                      | Usa MemoryFieldDelegate con lista desplegable editable y validador doble. Columna 10 en la tabla. Se restaura al sintonizar. |
| **-- Memory table -- Group**            | Selecciona entre nombres de grupo conocidos usando un editor de cuadro combinado que se abre inmediatamente al entrar en modo de edición. | Usa MemoryFieldDelegate con lista desplegable bloqueada.                                                |
| **Import...**                       | Importa memorias desde un archivo CSV con un diálogo de progreso.                                           | Muestra el progreso de la importación y un resumen con las filas omitidas.                                  |
| **Export...**                       | Exporta las memorias seleccionadas (o filtradas) a CSV.                                                      | Valida el CSV generado antes de guardarlo.                                                              |
| **Add**                             | Crea una nueva memoria desde el segmento activo actual.                                                      | Atajo Ctrl+N. La variante de insignia de letra de segmento se eliminó; agregar siempre apunta al segmento activo. |
| **Edit**                            | Entra en modo de edición en línea en el campo Name de la memoria seleccionada.                               | F2 o Ctrl+E también activan la edición. Solo se habilita cuando exactamente una memoria está seleccionada. |
| **Tune**                            | Sintoniza el segmento activo a la memoria seleccionada, restaurando todos los campos almacenados.           | Se debe seleccionar una fila. Hacer doble clic en una fila tiene el mismo efecto.                        |
| **Select All**                      | Selecciona todas las filas visibles (respetando la búsqueda/filtro).                                        | Atajo Ctrl+Shift+A.                                                                      |
| **Remove**                          | Elimina las memorias seleccionadas (con confirmación). Muestra el progreso para la eliminación por lotes.   | La tecla Delete/Backspace también activa. La etiqueta del botón cambia a 'Remove Selected' cuando hay >1 fila seleccionada. |
| Barra de título — Memory Channels   | Barra de título con degradado de 18 píxeles sin marco con un glifo de agarre a la izquierda y el título del diálogo. | Arrastrar para mover; doble clic para alternar maximizar/restaurar.                                      |
| — (Minimizar)                       | Minimiza el diálogo.                                                                                        |                                                                                             |
| □ (Maximizar)                       | Maximiza o restaura el diálogo.                                                                             |                                                                                             |
| × (Cerrar)                          | Cierra el diálogo. Escape primero limpia la búsqueda, luego cierra.                                        |                                                                                             |
| Arrastrar para mover                | Haga clic y arrastre la barra de título para mover el diálogo.                                             | Haga doble clic en la barra de título para alternar maximizar/restaurar.                                      |
| Redimensionamiento de 8 ejes        | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. | Zona de impacto de redimensionamiento de 12 píxeles. El borde superior del diálogo está reservado para el manejo de movimiento de la barra de título, por lo que arrastrar la barra de título no es interceptado por la zona de redimensionamiento. |
| Conteo de selección                 | Muestra '<N> de <M> seleccionados'.                                                                          |                                                                                             |

## Consejos

- Si sus memorias de repetidor están mezcladas con otras entradas, use **Profile:** para filtrar por un grupo dedicado a repetidores para que la fila objetivo sea más fácil de localizar.
- Puede ordenar la tabla por cualquier columna ordenable — por ejemplo, Frequency — haciendo clic en el encabezado de la columna. Esto puede ayudarle a encontrar un repetidor por su frecuencia de salida. Consulte [Ordenar tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md).
- Presione Ctrl+Shift+A para seleccionar rápidamente todas las memorias visibles que coincidan con su búsqueda o filtro de perfil.
- Presione Ctrl+N para agregar una nueva memoria desde el segmento activo sin usar el mouse.
- Al editar un campo de memoria que usa un cuadro combinado (Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Group), la lista desplegable se abre automáticamente para que pueda elegir un valor con un solo clic. Para los campos editables (Step, Repeater Offset, Tone Value), también puede escribir un valor personalizado.

## Solución de problemas

- **Tune está atenuado** — No hay ninguna fila seleccionada. Haga clic en una fila de la tabla de memorias primero, luego haga clic en **Tune**.
- **El desplazamiento o tono del repetidor no se aplica después de sintonizar** — Las columnas FM TX Offset Dir, Repeater Offset, Tone Mode o Tone Value pueden estar vacías para esa memoria. Seleccione la fila, haga clic en **Edit**, complete las columnas faltantes y sintonice de nuevo. Consulte [Editar el nombre, modo o desplazamiento de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md).
- **La memoria esperada no aparece en la tabla** — Verifique el filtro **Profile:**. Si está seleccionado un perfil diferente al que contiene la memoria del repetidor, la fila estará oculta. Establezca **Profile:** en el perfil correcto o limpie el filtro.
- **El botón Add no crea la memoria esperada** — El botón **Add** ahora siempre apunta al segmento activo. Asegúrese de que el segmento correcto esté activo antes de hacer clic en Add.
- **Un campo de memoria muestra un valor que no está en la lista desplegable** — Los valores heredados o corruptos se conservan en la lista desplegable para que pueda verlos en lugar de que se intercambien silenciosamente. Puede editar el campo para seleccionar un valor válido.

## Relacionado

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Editar el nombre, modo o desplazamiento de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar la radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Ordenar tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
- Importar memorias desde CSV
- Exportar memorias a CSV
- Eliminar memorias
