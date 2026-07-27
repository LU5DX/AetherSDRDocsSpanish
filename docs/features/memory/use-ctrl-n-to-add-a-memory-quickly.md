# Canales de memoria

El diálogo de Canales de memoria le permite gestionar los canales de memoria del radio — añadir frecuencias desde la porción activa, editar memorias existentes, buscar y filtrar, sintonizar, importar/exportar y eliminar frecuencias almacenadas.

## Abrir el diálogo

1. Abra **Settings > Memory...**

   Aparece el diálogo de Canales de memoria con una barra de título sin marco y capacidad de redimensionamiento en 8 ejes.

## Búsqueda y filtro

| Control | Comportamiento |
|---------|----------------|
| **Search:** campo de texto | Filtra la tabla por nombre de memoria. Tiene un botón de limpiar; presione Enter para enviar. **Ctrl+F** enfoca el campo de búsqueda. |
| **Profile:** cuadro combinado | Filtra por perfil global o de transmisión activo. El valor predeterminado es "All Memories". Recolecta nombres de perfil de los perfiles globales y de transmisión de RadioModel. |

## Tabla de memorias

La tabla de memorias muestra y edita filas de memoria. Las columnas incluyen Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset.

- Ordene haciendo clic en los encabezados de columna (Frequency, Name, Mode).
- Modo de selección extendida; edición en línea mediante el botón **Edit** o **F2**/**Ctrl+E**.
- **Delete**/**Backspace** elimina las filas seleccionadas.
- Un doble clic sintoniza la porción activa a esa memoria.
- **Ctrl+Shift+A** selecciona todo.

### Edición en línea con campos desplegables

Al editar una celda de memoria, los campos restringidos (Mode, Offset Dir, Tone Mode, Tone Value, Step, Group) abren un editor de cuadro combinado. La lista se abre inmediatamente para que pueda elegir un valor con un solo clic.

- **Campos estrictos** (no editables): Solo se ofrecen valores conocidos del radio.
- **Campos editables**: Se proporcionan valores comunes, pero puede escribir texto personalizado; el radio valida la entrada al confirmar. Se aplican validadores de Entero y Decimal cuando corresponde.
- Si una celda contiene un valor que no está en la lista (por ejemplo, de una memoria antigua), el valor se conserva y se muestra como el primer elemento para que no se cambie silenciosamente.

## Gestión de memorias

| Control | Comportamiento |
|---------|----------------|
| **Import...** | Importa memorias desde un archivo CSV con diálogo de progreso. Muestra el progreso de importación y un resumen con las filas omitidas. |
| **Export...** | Exporta memorias seleccionadas (o filtradas) a CSV. Valida el CSV generado antes de guardar. |
| **Add** | Crea una nueva memoria desde la porción activa actual. Acceso directo **Ctrl+N**. Se eliminó la variante de insignia de letra de porción; añadir siempre apunta a la porción activa. |
| **Edit** | Activa el modo de edición en línea en el campo Name de la memoria seleccionada. **F2** o **Ctrl+E** también activan la edición. Solo está habilitado cuando está seleccionada exactamente una memoria. |
| **Tune** | Sintoniza la porción activa a la memoria seleccionada. Solo está habilitado cuando está seleccionada exactamente una memoria. |
| **Select All** | Selecciona todas las filas visibles (respetando búsqueda/filtro). Acceso directo **Ctrl+Shift+A**. |
| **Remove** | Elimina las memorias seleccionadas (con confirmación). Muestra progreso para eliminación por lotes. La tecla **Delete**/**Backspace** también lo activa. La etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada. |

## Barra de título y controles de ventana

El diálogo de Canales de memoria tiene una interfaz moderna sin marco:

| Control | Comportamiento |
|---------|----------------|
| **Title bar — Memory Channels** | Barra de título degradada de 18 px sin marco con glifo de agarre a la izquierda y el título del diálogo. |
| **— (Minimize)** | Minimiza el diálogo. |
| **□ (Maximize)** | Maximiza o restaura el diálogo. |
| **× (Close)** | Cierra el diálogo. Escape primero limpia la búsqueda, luego cierra. |
| **Arrastrar para mover** | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar. |
| **Redimensionamiento en 8 ejes** | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. Zona de impacto de redimensionamiento de 12 px. El borde superior reserva un área (la altura de la barra de título) para arrastrar y mover en lugar de redimensionar. |
| **Conteo de selección** | Muestra "<N> de <M> seleccionados". |

## Atajos de teclado

| Atajo | Acción |
|-------|--------|
| **Ctrl+N** | Añadir una nueva memoria desde la porción activa (funciona incluso con el diálogo cerrado) |
| **Ctrl+F** | Enfocar el campo de búsqueda |
| **F2** o **Ctrl+E** | Editar el nombre de la memoria seleccionada |
| **Delete** o **Backspace** | Eliminar memorias seleccionadas |
| **Ctrl+Shift+A** | Seleccionar todas las filas visibles |
| **Esc** | Limpiar búsqueda primero, luego cerrar diálogo |
| **Doble clic** en una fila de memoria | Sintonizar la porción activa a esa memoria |

## Añadir una memoria rápidamente (Ctrl+N)

Añada un canal de memoria desde la porción activa sin abrir ningún menú — solo presione un atajo de teclado.

### Antes de comenzar

- El radio debe estar conectado y tener una porción activa.
- No es necesario que el diálogo de Canales de memoria esté abierto.

### Pasos

1. Presione **Ctrl+N** en cualquier parte de la ventana principal de la aplicación.

   Se crea una nueva memoria a partir de la frecuencia, modo y configuración de filtro de la porción activa actual.

2. (Opcional) Abra **Settings > Memory...** para ver la nueva memoria en la tabla y editar su nombre u otros campos.

### Consejos

- Ctrl+N funciona incluso cuando otros diálogos tienen el foco, siempre que la ventana principal esté activa.
- Use **Settings > Memory...** para añadir, editar o eliminar memorias en lote. Ctrl+N es el atajo más rápido para una sola memoria.

## Integración de temas

El diálogo de Canales de memoria admite estilo de temas. La tabla usa el color de fondo definido por el tema para filas alternas. Para aplicar un tema personalizado, configure el contenedor `dialog/memory` en su definición de tema.
