# Canales de Memoria

El diálogo de Canales de Memoria (`Settings > Memory...`) gestiona las frecuencias almacenadas de la radio: agregar, editar, buscar, filtrar por perfil, sintonizar, importar, exportar y eliminar memorias.

## Controles

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| **Search:** | campo_texto | Filtra la tabla por nombre de memoria. Tiene un botón de borrado; presione Enter para enviar. Presione Ctrl+F para enfocar el campo de búsqueda. |
| **Profile:** | cuadro_combinado | Filtra las memorias por perfil global o de transmisión activo. El valor predeterminado es "All Memories". Recopila los nombres de perfil de los perfiles globales y de transmisión de la radio. |
| **Tabla de memorias** | lista | Muestra y edita filas de memoria. Ordenable haciendo clic en los encabezados de columna (Frequency, Name, Mode y otros). Las columnas incluyen: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. Admite ExtendedSelection; edición en línea mediante el botón Edit o F2/Ctrl+E. Delete/Backspace elimina las filas seleccionadas. Doble clic sintoniza una memoria. Ctrl+Shift+A selecciona todo. |
| **Import...** | botón | Importa memorias desde un archivo CSV. Muestra un diálogo de progreso y un resumen con las filas omitidas. |
| **Export...** | botón | Exporta las memorias seleccionadas (o filtradas) a CSV. Valida el CSV generado antes de guardarlo. |
| **Add** | botón | Crea una nueva memoria a partir del slice (segmento) activo actual. Atajo: Ctrl+N. |
| **Edit** | botón | Activa el modo de edición en línea en el campo Name de la memoria seleccionada. Solo está habilitado cuando hay exactamente una memoria seleccionada. Atajo: F2 o Ctrl+E. |
| **Tune** | botón | Sintoniza el slice activo a la memoria seleccionada. Solo está habilitado cuando hay exactamente una memoria seleccionada. |
| **Select All** | botón | Selecciona todas las filas visibles (respetando búsqueda y filtro). Atajo: Ctrl+Shift+A. |
| **Remove** | botón | Elimina las memorias seleccionadas (con confirmación). Muestra progreso para eliminación por lotes. La etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada. Atajo: Delete o Backspace. |
| **Barra de título — Memory Channels** | indicador | Barra de título sin marco de 18 px con degradado, glifo de agarre a la izquierda y el título del diálogo. Añadido en v26.5.1 (#2509). |
| **— (Minimizar)** | botón | Minimiza el diálogo. |
| **□ (Maximizar)** | botón | Maximiza o restaura el diálogo. |
| **× (Cerrar)** | botón | Cierra el diálogo. Presione Escape para borrar primero el campo de búsqueda y luego cerrar. |
| **Arrastrar para mover** | control_arrastre | Haga clic y arrastre la barra de título para mover el diálogo. Doble clic en la barra de título para alternar maximizar/restaurar. |
| **Redimensionar en 8 ejes** | control_arrastre | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionar. El cursor cambia para indicar la dirección del redimensionamiento. La zona activa de redimensionamiento tiene 12 px de ancho. |
| **Conteo de selección** | indicador | Muestra "<N> de <M> seleccionados". |

### Agregar una Memoria desde un Slice

1. Asegúrese de que el slice deseado esté activo (haga clic en su barra de slice).
2. Haga clic en **Add** (o presione Ctrl+N).
3. Aparece una nueva fila en la tabla de memorias con la frecuencia, el modo y otros ajustes del slice activo.

**Nota:** La variante de selección de slice por letra se ha eliminado. Agregar siempre tiene como objetivo el slice activo.

### Editar una Memoria en Línea

La tabla de memorias admite edición en línea para campos restringidos (como Mode, Step, Tone Mode, Offset Direction) mediante delegados de cuadro combinado. Cuando hace doble clic o presiona F2 en una celda restringida, aparece una lista desplegable con valores válidos. Para campos editables, puede escribir un valor personalizado que la radio valida al confirmar.

1. Seleccione la fila de memoria a editar.
2. Haga clic en **Edit** (o presione F2 o Ctrl+E) para entrar en modo de edición en el campo Name.
3. Para editar otros campos, haga doble clic en la celda o presione F2 mientras la celda está seleccionada.
4. Para campos de cuadro combinado (Mode, Step, Offset Dir, Tone Mode, Tone Value, Group), la lista se abre inmediatamente. Seleccione un valor o escriba un valor editable.
5. Presione Enter para confirmar el cambio, o Escape para cancelar.

### Sintonizar una Memoria

1. Seleccione exactamente una memoria en la tabla.
2. Haga clic en **Tune**. El slice activo se sintoniza a la frecuencia de la memoria.

**Consejo:** Haga doble clic en cualquier memoria para sintonizar directamente sin usar el botón Tune.

### Eliminar Memorias

1. Seleccione una o más memorias (use Ctrl+clic para selección no contigua, Shift+clic para rango, o Ctrl+Shift+A para seleccionar todas las filas visibles).
2. Haga clic en **Remove** (o presione Delete o Backspace).
3. Confirme la eliminación cuando se le solicite. Aparece una barra de progreso para eliminaciones por lotes.

### Importar Memorias desde CSV

1. Haga clic en **Import...**.
2. Seleccione un archivo CSV. Un diálogo de progreso muestra el proceso de importación.
3. Revise el resumen para ver las filas omitidas.

### Exportar Memorias a CSV

1. Seleccione las memorias a exportar, o aplique búsqueda/filtro para limitar el conjunto.
2. Haga clic en **Export...**.
3. Elija una ubicación de guardado y un nombre de archivo. El CSV exportado se valida antes de guardarlo.

## Ordenar la Tabla de Memorias

Haga clic en cualquier encabezado de columna ordenable para ordenar la tabla por esa columna. Haga clic en el mismo encabezado nuevamente para invertir la dirección del orden.

- La columna **Frequency** utiliza ordenación numérica (14.225 se ordena entre 14.200 y 14.300).
- Los indicadores de ordenación aparecen en el encabezado.
- La ordenación no afecta el índice almacenado en la radio.
- Los filtros de búsqueda y perfil permanecen activos mientras se ordena.

## Relacionados

- [Sort Memory Table by Column Header](sort-memory-table-by-column-header.md)
- [Search memories by name](search-memories-by-name.md)
- [Filter memories by profile](filter-memories-by-profile.md)
- [Tune the radio to a stored memory](tune-the-radio-to-a-stored-memory.md)
