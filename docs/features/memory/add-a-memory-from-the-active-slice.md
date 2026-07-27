# Añadir una memoria desde el slice activo

Guarde la frecuencia, el modo y otros ajustes del slice activo como un nuevo canal de memoria para recuperarlo más adelante.

## Antes de empezar

- Debe haber una radio conectada y al menos un slice activo.
- Abra el diálogo Canales de Memoria: **Settings > Memory...**

## Pasos

1. En el diálogo Canales de Memoria, haga clic en **Add**.
   - O presione **Ctrl+N**.
2. Aparece una nueva fila en la tabla de memoria con la frecuencia, el modo y otros parámetros actuales del slice activo.
3. (Opcional) Edite el nombre u otros campos de la memoria:
   - Haga clic en **Edit** para activar la edición en línea del campo Nombre.
   - Haga clic directamente en otras celdas para editar sus valores. Para campos restringidos (Mode, Step, Offset Direction, Tone Mode, Tone Value, Group), se abre automáticamente un cuadro combinado con valores comunes. Para los campos editables, puede escribir valores personalizados.

## Función de cada control

| Control | Etiqueta | Comportamiento |
|---|---|---|
| Barra de título | Memory Channels | Barra de título degradada de 18 px sin marco con un icono de agarre a la izquierda y el título del diálogo. Haga clic y arrastre para mover; haga doble clic para alternar maximizar/restaurar. |
| Botón Minimizar | — (Minimizar) | Minimiza el diálogo. |
| Botón Maximizar | □ (Maximizar) | Maximiza o restaura el diálogo. |
| Botón Cerrar | × (Cerrar) | Cierra el diálogo. Escape limpia primero el campo de búsqueda, luego cierra el diálogo. |
| Arrastrar para mover | — | Haga clic y arrastre la barra de título para mover el diálogo. Los 18 px superiores (altura de la barra de título) están reservados para mover; la zona de redimensión comienza debajo. Haga doble clic para alternar maximizar/restaurar. |
| Redimensión de 8 ejes | — | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección de redimensión. Zona de redimensión de 12 px. La zona de redimensión del borde superior comienza debajo de la barra de título. |
| Campo de búsqueda | Search: | Filtra la tabla por nombre de memoria. Tiene un botón de limpiar; presione Enter para enviar. Ctrl+F enfoca este campo. |
| Filtro de perfil | Profile: | Filtra las memorias por perfil global o de transmisión activo. Valor predeterminado: "All Memories". |
| Tabla de memoria | — | Muestra las filas de memoria. Ordenable haciendo clic en los encabezados de columna (Frequency, Name, Mode). Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. Haga doble clic para sintonizar. Ctrl+Shift+A selecciona todas las filas. Ctrl+F enfoca el campo de búsqueda. Las celdas editables usan editores de cuadro combinado para campos restringidos (Mode, Step, Offset Direction, Tone Mode, Tone Value, Group); el menú desplegable se abre inmediatamente al empezar a editar. El fondo de la tabla usa el color del tema `dialog/memory`. |
| Contador de selección | — | Muestra "<N> de <M> seleccionados". |
| Botón Add | Add | Crea una nueva memoria a partir de los ajustes actuales del slice activo. Atajo: Ctrl+N. |
| Botón Edit | Edit | Activa la edición en línea del campo Nombre de la memoria seleccionada. Solo está habilitado cuando hay exactamente una memoria seleccionada. Atajo: F2 o Ctrl+E. |
| Botón Tune | Tune | Sintoniza el slice activo en la memoria seleccionada. Solo está habilitado cuando hay exactamente una memoria seleccionada. |
| Botón Select All | Select All | Selecciona todas las filas visibles (respetando la búsqueda/filtro). Atajo: Ctrl+Shift+A. |
| Botón Remove | Remove | Elimina las memorias seleccionadas (con confirmación). Muestra el progreso para eliminación por lotes. La etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada. Atajo: Delete o Backspace. |
| Botón Import | Import... | Importa memorias desde un archivo CSV con un diálogo de progreso. Muestra el progreso de importación y un resumen con las filas omitidas. |
| Botón Export | Export... | Exporta las memorias seleccionadas (o filtradas) a CSV. Valida el CSV generado antes de guardarlo. |

## Consejos

- A la memoria se le asigna automáticamente un número de índice secuencial. Para renombrarla, seleccione la fila y haga clic en **Edit** o presione **F2**.
- La memoria captura la frecuencia, el modo, el paso, los ajustes de filtro y cualquier parámetro de repetidor FM (dirección de desplazamiento, desplazamiento, modo de tono, valor de tono, ajustes de squelch) del slice activo.
- El diálogo recuerda su tamaño y posición entre sesiones.
- El botón Add siempre apunta al slice activo; no hay selección por letra de slice.
- El diálogo usa el color del tema definido para `dialog/memory`. Los colores alternos de las filas en la tabla de memoria siguen el color de fondo del tema.
- Al editar campos restringidos (Mode, Step, Offset Direction, Tone Mode, Tone Value, Group), se abre automáticamente un cuadro combinado con los valores conocidos. Para campos editables, puede escribir valores personalizados que son validados por la radio al confirmarlos.

## Relacionados

- [Edit a memory's name inline](edit-a-memory-s-name-inline.md)
- [Tune the radio to a stored memory](tune-the-radio-to-a-stored-memory.md)
- [Use Ctrl+N to add a memory quickly](use-ctrl-n-to-add-a-memory-quickly.md)
