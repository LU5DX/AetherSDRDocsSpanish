# Agregar una memoria desde el slice activo

Guarde la frecuencia, el modo y otros ajustes del slice activo actual como un nuevo canal de memoria para poder recuperarlos más adelante.

## Antes de comenzar

- Debe haber una radio conectada y al menos un slice activo.
- Abra el diálogo Memory Channels: **Settings > Memory...**

## Pasos

1. En el diálogo Memory Channels, haga clic en **Add**.
   - O presione **Ctrl+N**.
2. Aparece una nueva fila en la tabla de memorias con la frecuencia, el modo y otros parámetros actuales del slice activo.
3. (Opcional) Edite el nombre de la memoria u otros campos:
   - Haga clic en **Edit** para activar la edición en línea del campo Name.
   - Haga clic directamente en otras celdas para editar sus valores. Para los campos restringidos (Mode, Step, Offset Direction, Tone Mode, Tone Value, Group), se abre automáticamente un cuadro combinado con los valores comunes. En los campos editables, puede escribir valores personalizados.

## Qué hace cada control

| Control | Etiqueta | Comportamiento |
|---|---|---|
| Barra de título | Memory Channels | Barra de título degradada de 18 px sin marco con un glifo de agarre a la izquierda y el título del diálogo. Haga clic y arrastre para mover; doble clic para alternar maximizar/restaurar. |
| Botón Minimizar | — (Minimize) | Minimiza el diálogo. |
| Botón Maximizar | □ (Maximize) | Maximiza o restaura el diálogo. |
| Botón Cerrar | × (Close) | Cierra el diálogo. Escape limpia el campo de búsqueda primero y luego cierra el diálogo. |
| Arrastrar para mover | — | Haga clic y arrastre la barra de título para mover el diálogo. Los 18 px superiores (altura de la barra de título) están reservados para mover; la zona de redimensionamiento comienza debajo. Doble clic para alternar maximizar/restaurar. |
| Redimensionamiento en 8 direcciones | — | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección del redimensionamiento. Zona de redimensionamiento de 12 px. La zona de redimensionamiento del borde superior comienza debajo de la barra de título. |
| Campo de búsqueda | Search: | Filtra la tabla por nombre de memoria. Tiene un botón de borrar; presione Enter para enviar. Ctrl+F enfoca este campo. |
| Filtro de perfil | Profile: | Filtra las memorias por perfil global o de transmisión activo. Valor predeterminado: "All Memories". |
| Tabla de memorias | — | Muestra las filas de memoria. Se puede ordenar haciendo clic en los encabezados de columna (Frequency, Name, Mode). Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. Selección extendida; modo de edición en línea mediante el botón Edit o F2/Ctrl+E. Delete/Backspace elimina las filas seleccionadas. Doble clic sintoniza. Ctrl+Shift+A selecciona todo. Las celdas editables usan editores de cuadro combinado para los campos restringidos (Mode, Step, Offset Direction, Tone Mode, Tone Value, Group): el menú desplegable se abre inmediatamente al comenzar a editar. El fondo de la tabla usa el color del tema `dialog/memory`. |
| Contador de selección | — | Muestra "<N> de <M> seleccionados". |
| Botón Add | Add | Crea una nueva memoria a partir de los ajustes actuales del slice activo (sin selección por letra: siempre apunta al slice activo). Atajo: Ctrl+N. |
| Botón Edit | Edit | Activa la edición en línea del campo Name de la memoria seleccionada. Solo se habilita cuando está seleccionada exactamente una memoria. Atajo: F2 o Ctrl+E. |
| Botón Tune | Tune | Sintoniza el slice activo a la memoria seleccionada. Solo se habilita cuando está seleccionada exactamente una memoria. |
| Botón Select All | Select All | Selecciona todas las filas visibles (respetando búsqueda/filtro). Atajo: Ctrl+Shift+A. |
| Botón Remove | Remove | Elimina las memorias seleccionadas (con confirmación). Muestra el progreso de la eliminación por lotes. La etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada. Atajo: Delete o Backspace. |
| Botón Import | Import... | Importa memorias desde un archivo CSV con diálogo de progreso. Muestra el progreso de la importación y un resumen con las filas omitidas. |
| Botón Export | Export... | Exporta las memorias seleccionadas (o filtradas) a CSV. Valida el CSV generado antes de guardarlo. |

## Consejos

- La memoria recibe automáticamente un número de índice secuencial. Para renombrarla, seleccione la fila y haga clic en **Edit** o presione **F2**.
- La memoria captura la frecuencia, el modo, el paso, los ajustes de filtro del slice activo y cualquier parámetro de repetidor FM (dirección de offset, offset, modo de tono, valor de tono, ajustes de squelch).
- El diálogo recuerda su tamaño y posición entre sesiones.
- El botón Add siempre apunta al slice activo; no hay selección por letra de slice.
- El diálogo usa el color del tema definido para `dialog/memory`. Los colores alternos de fila en la tabla de memorias siguen el color de fondo del tema.
- Al editar campos restringidos (Mode, Step, Offset Direction, Tone Mode, Tone Value, Group), se abre automáticamente un cuadro combinado con los valores conocidos. En los campos editables, puede escribir valores personalizados que la radio valida al confirmar.

## Relacionados

- [Edit a memory's name inline](edit-a-memory-s-name-inline.md)
- [Tune the radio to a stored memory](tune-the-radio-to-a-stored-memory.md)
- [Use Ctrl+N to add a memory quickly](use-ctrl-n-to-add-a-memory-quickly.md)
