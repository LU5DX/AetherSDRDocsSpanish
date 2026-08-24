# Canales de Memoria

El diálogo de Canales de Memoria le permite gestionar los canales de memoria de la radio: agregar frecuencias desde el slice activo, editar memorias existentes, buscar y filtrar, sintonizar, importar/exportar y eliminar frecuencias almacenadas.

## Abrir el diálogo

1. Abra **Settings > Memory...**

   Aparece el diálogo de Canales de Memoria con una barra de título sin marco y capacidad de redimensionado en 8 ejes.

## Buscar y filtrar

| Control | Comportamiento |
|---------|----------|
| **Search:** campo de texto | Filtra la tabla por nombre de memoria. Tiene un botón de borrado; presione Enter para enviar. **Ctrl+F** enfoca el campo de búsqueda. |
| **Profile:** cuadro combinado | Filtra por perfil global o de transmisión activo. El valor predeterminado es "All Memories". Recopila los nombres de perfil de los perfiles globales y de transmisión de RadioModel. |

## Tabla de memorias

La tabla de memorias muestra y edita filas de memoria. Las columnas incluyen Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset.

- Ordene haciendo clic en los encabezados de columna (Frequency, Name, Mode).
- Modo ExtendedSelection; edición en línea mediante el botón **Edit** o **F2**/**Ctrl+E**.
- **Delete**/**Backspace** elimina las filas seleccionadas.
- Doble clic sintoniza el slice activo a esa memoria.
- **Ctrl+Shift+A** selecciona todo.

### Edición en línea con campos desplegables

Al editar una celda de memoria, los campos restringidos (Mode, Offset Dir, Tone Mode, Tone Value, Step, Group) abren un editor de cuadro combinado. La lista se despliega inmediatamente para que pueda elegir un valor con un solo clic.

- **Campos estrictos** (no editables): Solo se ofrecen valores conocidos de la radio.
- **Campos editables**: Se cargan valores comunes, pero puede escribir texto personalizado; la radio valida la entrada al confirmar. Se aplican validadores de entero y decimal cuando corresponde.
- Si una celda contiene un valor que no está en la lista (por ejemplo, de una memoria heredada), el valor se conserva y se muestra como primer elemento para que no se modifique silenciosamente.

## Gestión de memorias

| Control | Comportamiento |
|---------|----------|
| **Import...** | Importa memorias desde un archivo CSV con diálogo de progreso. Muestra el progreso de la importación y un resumen con las filas omitidas. |
| **Export...** | Exporta las memorias seleccionadas (o filtradas) a CSV. Valida el CSV generado antes de guardarlo. |
| **Add** | Crea una nueva memoria desde el slice actual (activo). Atajo **Ctrl+N**. La variante con insignia de letra de slice se eliminó; agregar siempre se dirige al slice activo. |
| **Edit** | Entra en modo de edición en línea en el campo Name de la memoria seleccionada. **F2** o **Ctrl+E** también activan la edición. Solo está habilitado cuando está seleccionada exactamente una memoria. |
| **Tune** | Sintoniza el slice activo a la memoria seleccionada. Solo está habilitado cuando está seleccionada exactamente una memoria. |
| **Select All** | Selecciona todas las filas visibles (respetando la búsqueda/filtro). Atajo **Ctrl+Shift+A**. |
| **Remove** | Elimina las memorias seleccionadas (con confirmación). Muestra progreso para la eliminación por lotes. La tecla **Delete**/**Backspace** también lo activa. La etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada. |

## Barra de título y controles de ventana

El diálogo de Canales de Memoria tiene una interfaz moderna sin marco:

| Control | Comportamiento |
|---------|----------|
| **Title bar — Memory Channels** | Barra de título sin marco de 18 px con degradado, glifo de agarre a la izquierda y el título del diálogo. |
| **— (Minimize)** | Minimiza el diálogo. |
| **□ (Maximize)** | Maximiza o restaura el diálogo. |
| **× (Close)** | Cierra el diálogo. Escape borra la búsqueda primero y luego cierra. |
| **Drag-to-move** | Haga clic y arrastre la barra de título para mover el diálogo. Doble clic en la barra de título alterna maximizar/restaurar. |
| **8-axis resize** | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección del redimensionado. Zona de redimensionado de 12 px mediante FramelessResizer. El borde superior reserva un área (la altura de la barra de título) para arrastrar y mover en lugar de redimensionar. |
| **Selection count** | Muestra "<N> de <M> seleccionados". |

## Atajos de teclado

| Atajo | Acción |
|----------|--------|
| **Ctrl+N** | Agregar una nueva memoria desde el slice activo (funciona incluso cuando el diálogo está cerrado) |
| **Ctrl+F** | Enfocar el campo de búsqueda |
| **F2** o **Ctrl+E** | Editar el nombre de la memoria seleccionada |
| **Delete** o **Backspace** | Eliminar las memorias seleccionadas |
| **Ctrl+Shift+A** | Seleccionar todas las filas visibles |
| **Esc** | Borrar la búsqueda primero, luego cerrar el diálogo |
| **Doble clic** en una fila de memoria | Sintonizar el slice activo a esa memoria |

## Agregar una memoria rápidamente (Ctrl+N)

Agregue un canal de memoria desde el slice activo sin abrir ningún menú — simplemente presione un atajo de teclado.

### Antes de comenzar

- La radio debe estar conectada y tener un slice activo.
- El diálogo de Canales de Memoria no necesita estar abierto.

### Pasos

1. Presione **Ctrl+N** en cualquier lugar de la ventana principal de la aplicación.

   Se crea una nueva memoria a partir de la frecuencia, el modo y los ajustes de filtro del slice activo actual.

2. (Opcional) Abra **Settings > Memory...** para ver la nueva memoria en la tabla y editar su nombre u otros campos.

### Consejos

- Ctrl+N funciona incluso cuando otros diálogos tienen el foco, siempre que la ventana principal esté activa.
- Use **Settings > Memory...** para agregar, editar o eliminar memorias en lote. Ctrl+N es el atajo más rápido para una sola memoria.

## Integración de temas

El diálogo de Canales de Memoria admite estilos de tema. La tabla usa el color de fondo definido por el tema para las filas alternas. Para aplicar un tema personalizado, configure el contenedor `dialog/memory` en su definición de tema.
