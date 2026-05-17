# Canales de Memoria

El diálogo de Canales de Memoria le permite gestionar los canales de memoria del radio: agregar frecuencias desde el slice activo, editar memorias existentes, buscar y filtrar, sintonizar, importar/exportar y eliminar frecuencias almacenadas.

## Abrir el diálogo

1. Abra **Settings > Memory...**

   Aparecerá el diálogo de Canales de Memoria con una barra de título sin bordes y capacidad de redimensionamiento en 8 ejes.

## Búsqueda y filtro

| Control | Comportamiento |
|---------|---------------|
| **Search:** campo de texto | Filtra la tabla por nombre de memoria. Tiene un botón de limpieza; presione Enter para enviar. **Ctrl+F** enfoca el campo de búsqueda. |
| **Profile:** cuadro combinado | Filtra por perfil global o de transmisión activo. El valor predeterminado es "All Memories". Recopila nombres de perfiles de los perfiles globales y de transmisión de RadioModel. |

## Tabla de memorias

La tabla de memorias muestra y edita filas de memoria. Las columnas incluyen Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset.

- Ordene haciendo clic en los encabezados de columna (Frequency, Name, Mode).
- Modo de selección extendida; edición en línea mediante el botón **Edit** o **F2**/**Ctrl+E**.
- **Delete**/**Backspace** elimina las filas seleccionadas.
- Un doble clic sintoniza el slice activo en esa memoria.
- **Ctrl+Shift+A** selecciona todo.

## Gestión de memorias

| Control | Comportamiento |
|---------|---------------|
| **Import...** | Importa memorias desde un archivo CSV con un diálogo de progreso. Muestra el progreso de la importación y un resumen con las filas omitidas. |
| **Export...** | Exporta las memorias seleccionadas (o filtradas) a CSV. Valida el CSV generado antes de guardarlo. |
| **Add** | Crea una nueva memoria desde el slice (activo) actual. Atajo **Ctrl+N**. La variante de la insignia de letra de slice fue eliminada; agregar siempre apunta al slice activo. |
| **Edit** | Activa el modo de edición en línea en el campo Name de la memoria seleccionada. **F2** o **Ctrl+E** también activan la edición. Solo está habilitado cuando está seleccionada exactamente una memoria. |
| **Tune** | Sintoniza el slice activo en la memoria seleccionada. Solo está habilitado cuando está seleccionada exactamente una memoria. |
| **Select All** | Selecciona todas las filas visibles (respetando la búsqueda/filtro). Atajo **Ctrl+Shift+A**. |
| **Remove** | Elimina las memorias seleccionadas (con confirmación). Muestra el progreso para la eliminación por lotes. La tecla **Delete**/**Backspace** también lo activa. La etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada. |

## Barra de título y controles de ventana

El diálogo de Canales de Memoria tiene una interfaz moderna sin bordes:

| Control | Comportamiento |
|---------|---------------|
| **Barra de título — Memory Channels** | Barra de título degradada de 18 píxeles sin bordes con un glifo de agarre a la izquierda y el título del diálogo. |
| **— (Minimizar)** | Minimiza el diálogo. |
| **□ (Maximizar)** | Maximiza o restaura el diálogo. |
| **× (Cerrar)** | Cierra el diálogo. Escape primero limpia la búsqueda, luego cierra. |
| **Arrastrar para mover** | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar. |
| **Redimensionamiento en 8 ejes** | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. Zona de impacto de redimensionamiento de 12 píxeles. |
| **Conteo de selección** | Muestra "<N> of <M> selected". |

## Atajos de teclado

| Atajo | Acción |
|-------|--------|
| **Ctrl+N** | Agregar una nueva memoria desde el slice activo (funciona incluso cuando el diálogo está cerrado) |
| **Ctrl+F** | Enfocar el campo de búsqueda |
| **F2** o **Ctrl+E** | Editar el nombre de la memoria seleccionada |
| **Delete** o **Backspace** | Eliminar las memorias seleccionadas |
| **Ctrl+Shift+A** | Seleccionar todas las filas visibles |
| **Esc** | Limpiar la búsqueda primero, luego cerrar el diálogo |
| **Doble clic** en una fila de memoria | Sintonizar el slice activo en esa memoria |

## Agregar una memoria rápidamente (Ctrl+N)

Agregue un canal de memoria desde el slice activo sin abrir ningún menú — simplemente presione un atajo de teclado.

### Antes de comenzar

- El radio debe estar conectado y tener un slice activo.
- No es necesario que el diálogo de Canales de Memoria esté abierto.

### Pasos

1. Presione **Ctrl+N** en cualquier lugar de la ventana principal de la aplicación.

   Se crea una nueva memoria a partir de los ajustes de frecuencia, modo y filtro del slice activo actual.

2. (Opcional) Abra **Settings > Memory...** para ver la nueva memoria en la tabla y editar su nombre u otros campos.

### Consejos

- Ctrl+N funciona incluso cuando otros diálogos tienen el foco, siempre que la ventana principal esté activa.
- Use **Settings > Memory...** para agregar, editar o eliminar memorias en lote. Ctrl+N es el atajo más rápido para una sola memoria.
