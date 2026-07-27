# Editar el nombre de una memoria en línea

Cambie el nombre de un canal de memoria almacenado directamente en la tabla de Memorias sin abrir un diálogo separado.

## Antes de comenzar

- Abra **Settings > Memory...** para mostrar el diálogo Memory Channels.
- La radio debe estar conectada.

## Pasos

1. Haga clic en una fila de la tabla de Memorias para seleccionarla. Solo se puede editar una memoria a la vez.

2. Realice una de las siguientes acciones para entrar en modo de edición en línea en el campo Name:
   - Haga clic en **Edit**.
   - Presione **F2** o **Ctrl+E**.

3. Escriba el nuevo nombre.

4. Presione **Enter** para confirmar o **Esc** para cancelar.

## Función de cada control

| Control | Comportamiento |
|---------|---------|
| Botón **Edit** | Entra en modo de edición en línea en la columna Name de la memoria seleccionada. Solo se habilita cuando está seleccionada exactamente una memoria. |
| **F2** / **Ctrl+E** | Atajo de teclado que activa el mismo modo de edición que el botón **Edit**. |

## Consejos

- La columna Name admite hasta el límite de caracteres establecido por el firmware de la radio. AetherSDR codifica el nombre según lo requiere el protocolo SmartSDR.
- Para cancelar la edición, presione **Esc** antes de presionar Enter.
- El diálogo Memory Channels utiliza un marco **PersistentDialog** que recuerda su tamaño y posición entre sesiones. La geometría se almacena en la configuración `MemoryDialogGeometry` y se restaura la próxima vez que se abra el diálogo.

## Relacionados

- [Memory Channels overview](overview.md)
- [Add a memory from the active slice](add-a-memory-from-the-active-slice.md)
- [Delete one or more memories](delete-one-or-more-memories.md)
- [Tune the radio to a stored memory](tune-the-radio-to-a-stored-memory.md)
- [Search memories by name](search-memories-by-name.md)

# Diálogo Memory Channels

Gestione los canales de memoria de la radio: agregue, edite, busque, filtre, sintonice, importe, exporte y elimine frecuencias almacenadas.

## Abrir el diálogo

- Seleccione **Settings > Memory...**

## Características del diálogo

| Control | Descripción |
|---------|-------------|
| Barra de título — Memory Channels | Barra de título degradada sin marco de 18 px con el icono de agarre a la izquierda y el título del diálogo. Añadido en v26.5.1. |
| — (Minimizar) | Minimiza el diálogo. |
| □ (Maximizar) | Maximiza o restaura el diálogo. |
| × (Cerrar) | Cierra el diálogo. Presionar Escape limpia primero el campo de búsqueda y luego cierra el diálogo. |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. La barra de título proporciona un controlador de movimiento de borde a borde; la zona de cambio de tamaño del borde superior está reservada para la barra de título para evitar que el redimensionador robe eventos de arrastre. |
| Redimensionamiento de 8 ejes | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. La zona de activación de redimensionamiento es de 12 px. El borde superior no es redimensionable; la barra de título maneja las operaciones de movimiento en su lugar. |
| Campo de texto **Search:** | Filtra la tabla por nombre de memoria. Tiene un botón de limpieza. Presione Enter para enviar. Presione **Ctrl+F** para enfocar el campo de búsqueda. |
| Cuadro combinado **Profile:** | Filtra la tabla por perfil global o de transmisión activo. Valor predeterminado: "All Memories". Recopila nombres de perfil de los perfiles globales de RadioModel y los perfiles de transmisión. |
| Tabla de Memorias | Muestra y edita filas de memoria. Ordenable haciendo clic en los encabezados de columna (Frequency, Name, Mode). Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. Admite ExtendedSelection. Modo de edición en línea mediante el botón **Edit** o **F2**/**Ctrl+E**. Delete o Backspace elimina las filas seleccionadas. Doble clic para sintonizar. Ctrl+Shift+A para seleccionar todo. Varios campos restringidos (Mode, Offset Dir, Tone Mode, Tone Value, Step, Group) utilizan un editor de cuadro combinado que se abre inmediatamente para una selección con un solo clic. Los campos combinados editables aceptan entrada escrita validada por la radio al confirmar. |
| Recuento de selección | Muestra "<N> de <M> seleccionados". |
| Botón **Import...** | Importa memorias desde un archivo CSV con un diálogo de progreso. Muestra el progreso de la importación y un resumen con cualquier fila omitida. |
| Botón **Export...** | Exporta las memorias seleccionadas (o filtradas) a CSV. Valida el CSV generado antes de guardarlo. |
| Botón **Add** | Crea una nueva memoria desde la (rebanada) activa actual. Atajo de teclado: **Ctrl+N**. |
| Botón **Edit** | Entra en modo de edición en línea en el campo Name de la memoria seleccionada. Solo se habilita cuando está seleccionada exactamente una memoria. Atajos de teclado: **F2** o **Ctrl+E**. |
| Botón **Tune** | Sintoniza la rebanada activa a la memoria seleccionada. Solo se habilita cuando está seleccionada exactamente una memoria. |
| Botón **Select All** | Selecciona todas las filas visibles (respetando búsqueda/filtro). Atajo de teclado: **Ctrl+Shift+A**. |
| Botón **Remove** | Elimina las memorias seleccionadas (con confirmación). Muestra progreso para la eliminación por lotes. La etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada. Atajos de teclado: **Delete** o **Backspace**. |

## Estilo visual

El diálogo utiliza estilo temático. El color de fondo de filas alternas de la tabla está controlado por el contenedor de tema `dialog/memory` y el token de tema `{{color.background.0}}`. El color de fondo del elemento seleccionado utiliza el color `#2060a0`. Estos estilos se aplican mediante `AetherSDR::ThemeManager`.

## Consejos

- El diálogo recuerda su tamaño y posición entre sesiones. La geometría se almacena en la configuración `MemoryDialogGeometry`.
- Para agregar una memoria desde la rebanada activa, presione **Ctrl+N** o haga clic en **Add**.
- Para eliminar memorias, seleccione una o más filas y presione **Delete** o **Backspace**, o haga clic en **Remove**.
- Para sintonizar la radio a una memoria almacenada, haga doble clic en la fila o selecciónela y haga clic en **Tune**.
- Para seleccionar todas las memorias visibles, presione **Ctrl+Shift+A** o haga clic en **Select All**.
- El campo de búsqueda admite filtrar por nombre de memoria. Presione **Ctrl+F** para enfocarlo.
- La importación y exportación utilizan formato CSV. La exportación valida el archivo generado antes de guardarlo.
- En la tabla de Memorias, los campos restringidos (Mode, Offset Dir, Tone Mode, Tone Value, Step, Group) utilizan un editor de cuadro combinado. La lista se abre automáticamente cuando comienza a editar la celda. Para campos estrictos, solo están disponibles los valores conocidos. Para campos editables, puede escribir un valor personalizado, que será validado por la radio al confirmarse. Si hay un valor heredado o corrupto, se conserva en lugar de ser reemplazado silenciosamente.
