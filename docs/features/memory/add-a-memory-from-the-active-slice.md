# Añadir una memoria desde el slice activo

Guarde la frecuencia, el modo y otros ajustes del slice activo como un nuevo canal de memoria para recuperarlos posteriormente.

## Antes de comenzar

- Debe haber una radio conectada y al menos un slice activo.
- Abra el diálogo de Canales de Memoria: **Settings > Memory...**

## Pasos

1. En el diálogo de Canales de Memoria, haga clic en **Add**.
   - O presione **Ctrl+N**.
2. Aparece una nueva fila en la tabla de memoria con la frecuencia, el modo y otros parámetros actuales del slice activo.
3. (Opcional) Edite el nombre de la memoria u otros campos:
   - Haga clic en **Edit** para activar la edición en línea del campo Nombre.
   - Haga clic directamente en otras celdas para editar sus valores.

## Descripción de cada control

| Control | Etiqueta | Comportamiento |
|---|---|---|
| Barra de título | Memory Channels | Barra de título sin marco con degradado de 18 px, agarre a la izquierda y título del diálogo. Haga clic y arrastre para mover; haga doble clic para alternar maximizar/restaurar. |
| Botón Minimizar | — (Minimizar) | Minimiza el diálogo. |
| Botón Maximizar | □ (Maximizar) | Maximiza o restaura el diálogo. |
| Botón Cerrar | × (Cerrar) | Cierra el diálogo. Escape limpia primero el campo de búsqueda y luego cierra el diálogo. |
| Arrastrar para mover | — | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic para alternar maximizar/restaurar. |
| Redimensionar en 8 ejes | — | Haga clic y arrastre cualquier borde o esquina para redimensionar. El cursor cambia para indicar la dirección. Zona activa de 12 px. |
| Campo de búsqueda | Search: | Filtra la tabla por nombre de memoria. Tiene un botón de limpiar; presione Enter para enviar. Ctrl+F enfoca este campo. |
| Filtro de perfil | Profile: | Filtra memorias por perfil global o de transmisión activo. Predeterminado: "All Memories". |
| Tabla de memoria | — | Muestra filas de memoria. Ordenable haciendo clic en los encabezados de columna (Frequency, Name, Mode). Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. Haga doble clic para sintonizar. Ctrl+Shift+A selecciona todas las filas. Ctrl+F enfoca el campo de búsqueda. |
| Contador de selección | — | Muestra "<N> de <M> seleccionados". |
| Botón Añadir | Add | Crea una nueva memoria a partir de los ajustes actuales del slice activo. Atajo: Ctrl+N. |
| Botón Editar | Edit | Activa la edición en línea en el campo Nombre de la memoria seleccionada. Solo se habilita cuando está seleccionada exactamente una memoria. Atajo: F2 o Ctrl+E. |
| Botón Sintonizar | Tune | Sintoniza el slice activo en la memoria seleccionada. Solo se habilita cuando está seleccionada exactamente una memoria. |
| Botón Seleccionar todo | Select All | Selecciona todas las filas visibles (respetando búsqueda/filtro). Atajo: Ctrl+Shift+A. |
| Botón Eliminar | Remove | Elimina las memorias seleccionadas (con confirmación). Muestra progreso para eliminación por lotes. La etiqueta cambia a "Remove Selected" cuando hay más de una fila seleccionada. Atajo: Delete o Backspace. |
| Botón Importar | Import... | Importa memorias desde un archivo CSV con diálogo de progreso. Muestra el progreso de importación y un resumen con cualquier fila omitida. |
| Botón Exportar | Export... | Exporta las memorias seleccionadas (o filtradas) a CSV. Valida el CSV generado antes de guardar. |

## Consejos

- A la memoria se le asigna automáticamente un número de índice secuencial. Para renombrarla, seleccione la fila y haga clic en **Edit** o presione **F2**.
- La memoria captura la frecuencia, modo, paso, ajustes de filtro del slice activo y cualquier parámetro de repetidor FM (dirección de desplazamiento, offset, modo de tono, valor de tono, ajustes de squelch).
- El diálogo recuerda su tamaño y posición entre sesiones.
- El botón Add siempre se dirige al slice activo; no hay selección por letra de slice.

## Relacionado

- [Edit a memory's name inline](edit-a-memory-s-name-inline.md)
- [Tune the radio to a stored memory](tune-the-radio-to-a-stored-memory.md)
- [Use Ctrl+N to add a memory quickly](use-ctrl-n-to-add-a-memory-quickly.md)
