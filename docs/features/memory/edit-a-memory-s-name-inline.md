# Editar el nombre de una memoria en línea

Cambie el nombre de un canal de memoria almacenado directamente en la tabla de Memorias sin abrir un cuadro de diálogo independiente.

## Antes de comenzar

- Abra **Settings > Memory...** para mostrar el cuadro de diálogo Memory Channels.
- La radio debe estar conectada.

## Pasos

1. Haga clic en una fila de la tabla de Memorias para seleccionarla. Solo se puede editar una memoria a la vez.

2. Realice una de las siguientes acciones para entrar en el modo de edición en línea en el campo Name:
   - Haga clic en **Edit**.
   - Presione **F2** o **Ctrl+E**.

3. Escriba el nuevo nombre.

4. Presione **Enter** para confirmar o **Esc** para cancelar.

## Función de cada control

| Control | Comportamiento |
|---------|----------------|
| Botón **Edit** | Activa el modo de edición en línea en la columna Name de la memoria seleccionada. Solo está habilitado cuando hay exactamente una memoria seleccionada. |
| **F2** / **Ctrl+E** | Atajo de teclado que activa el mismo modo de edición que el botón **Edit**. |

## Consejos

- La columna Name admite hasta el límite de caracteres establecido por el firmware de la radio. AetherSDR codifica el nombre según lo requiere el protocolo SmartSDR.
- Para cancelar la edición, presione **Esc** antes de presionar Enter.
- El cuadro de diálogo Memory Channels utiliza un marco **PersistentDialog** que recuerda su tamaño y posición entre sesiones. La geometría se almacena en el ajuste `MemoryDialogGeometry` y se restaura la próxima vez que se abre el diálogo.

## Relacionado

- [Resumen de Memory Channels](overview.md)
- [Añadir una memoria desde el slice activo](add-a-memory-from-the-active-slice.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
- [Sintonizar la radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Buscar memorias por nombre](search-memories-by-name.md)

# Cuadro de diálogo Memory Channels

Administre los canales de memoria de la radio: añada, edite, busque, filtre, sintonice, importe, exporte y elimine frecuencias almacenadas.

## Abrir el diálogo

- Seleccione **Settings > Memory...**

## Funciones del diálogo

| Control | Descripción |
|---------|-------------|
| Barra de título — Memory Channels | Barra de título sin bordes de 18 px con degradado, con un asa de agarre a la izquierda y el título del diálogo. Añadido en v26.5.1. |
| — (Minimizar) | Minimiza el diálogo. |
| □ (Maximizar) | Maximiza o restaura el diálogo. |
| × (Cerrar) | Cierra el diálogo. Presionar Escape limpia primero el campo de búsqueda y luego cierra el diálogo. |
| Arrastrar para mover | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. |
| Redimensionar en 8 ejes | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. La zona de contacto para redimensionar es de 12 px. |
| Campo de texto **Search:** | Filtra la tabla por nombre de memoria. Tiene un botón de limpiar. Presione Enter para enviar. Presione **Ctrl+F** para enfocar el campo de búsqueda. |
| Cuadro combinado **Profile:** | Filtra la tabla por perfil global o de transmisión activo. Valor predeterminado: "All Memories". Recopila los nombres de perfil de los perfiles globales y de transmisión de RadioModel. |
| Tabla de Memorias | Muestra y edita las filas de memoria. Ordenable haciendo clic en los encabezados de columna (Frequency, Name, Mode). Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. Soporta ExtendedSelection. Modo de edición en línea mediante el botón **Edit** o **F2**/**Ctrl+E**. Delete o Backspace elimina las filas seleccionadas. Doble clic sintoniza. Ctrl+Shift+A selecciona todo. |
| Conteo de selección | Muestra "<N> de <M> seleccionados". |
| Botón **Import...** | Importa memorias desde un archivo CSV con un cuadro de diálogo de progreso. Muestra el progreso de importación y un resumen con las filas omitidas. |
| Botón **Export...** | Exporta las memorias seleccionadas (o filtradas) a CSV. Valida el CSV generado antes de guardarlo. |
| Botón **Add** | Crea una nueva memoria desde el slice activo (actual). Atajo de teclado: **Ctrl+N**. |
| Botón **Edit** | Activa el modo de edición en línea en el campo Name de la memoria seleccionada. Solo está habilitado cuando hay exactamente una memoria seleccionada. Atajos de teclado: **F2** o **Ctrl+E**. |
| Botón **Tune** | Sintoniza el slice activo a la memoria seleccionada. Solo está habilitado cuando hay exactamente una memoria seleccionada. |
| Botón **Select All** | Selecciona todas las filas visibles (respetando la búsqueda/filtro). Atajo de teclado: **Ctrl+Shift+A**. |
| Botón **Remove** | Elimina las memorias seleccionadas (con confirmación). Muestra el progreso para la eliminación por lotes. La etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada. Atajos de teclado: **Delete** o **Backspace**. |

## Estilo visual

El diálogo utiliza un estilo temático. El color de fondo de las filas alternas de la tabla está controlado por el contenedor de tema `dialog/memory` y el token de tema `{{color.background.0}}`. El color de fondo del elemento seleccionado usa el color `#2060a0`. Estos estilos se aplican mediante `AetherSDR::ThemeManager`.

## Consejos

- El diálogo recuerda su tamaño y posición entre sesiones. La geometría se almacena en el ajuste `MemoryDialogGeometry`.
- Para añadir una memoria desde el slice activo, presione **Ctrl+N** o haga clic en **Add**.
- Para eliminar memorias, seleccione una o más filas y presione **Delete** o **Backspace**, o haga clic en **Remove**.
- Para sintonizar la radio a una memoria almacenada, haga doble clic en la fila o selecciónela y haga clic en **Tune**.
- Para seleccionar todas las memorias visibles, presione **Ctrl+Shift+A** o haga clic en **Select All**.
- El campo de búsqueda admite el filtrado por nombre de memoria. Presione **Ctrl+F** para enfocarlo.
- La importación y exportación utilizan el formato CSV. La exportación valida el archivo generado antes de guardarlo.
