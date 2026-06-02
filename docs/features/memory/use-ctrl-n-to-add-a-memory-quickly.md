# Canales de Memoria

El diálogo de Canales de Memoria le permite gestionar los canales de memoria del radio — añadir frecuencias desde el slice activo, editar memorias existentes, buscar y filtrar, sintonizar, importar/exportar y eliminar frecuencias almacenadas.

## Abrir el diálogo

1. Abra **Settings > Memory...**

   Aparece el diálogo Canales de Memoria con una barra de título sin bordes y capacidad de redimensionamiento en 8 ejes.

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
- Haga doble clic para sintonizar el slice activo en esa memoria.
- **Ctrl+Shift+A** selecciona todo.

## Gestión de memorias

| Control | Comportamiento |
|---------|----------------|
| **Import...** | Importa memorias desde un archivo CSV con un diálogo de progreso. Muestra el progreso de importación y un resumen con las filas omitidas. |
| **Export...** | Exporta las memorias seleccionadas (o filtradas) a CSV. Valida el CSV generado antes de guardarlo. |
| **Add** | Crea una nueva memoria desde el slice actual (activo). Atajo **Ctrl+N**. La variante de insignia de letra de slice fue eliminada; añadir siempre apunta al slice activo. |
| **Edit** | Activa el modo de edición en línea en el campo de nombre de la memoria seleccionada. **F2** o **Ctrl+E** también activa la edición. Solo está habilitado cuando exactamente una memoria está seleccionada. |
| **Tune** | Sintoniza el slice activo en la memoria seleccionada. Solo está habilitado cuando exactamente una memoria está seleccionada. |
| **Select All** | Selecciona todas las filas visibles (respetando búsqueda/filtro). Atajo **Ctrl+Shift+A**. |
| **Remove** | Elimina las memorias seleccionadas (con confirmación). Muestra progreso para eliminación por lotes. La tecla **Delete**/**Backspace** también activa la acción. La etiqueta del botón cambia a "Remove Selected" cuando más de una fila está seleccionada. |

## Barra de título y controles de ventana

El diálogo Canales de Memoria tiene una interfaz moderna sin bordes:

| Control | Comportamiento |
|---------|----------------|
| **Barra de título — Memory Channels** | Barra de título degradada sin bordes de 18 px con un glifo de agarre a la izquierda y el título del diálogo. |
| **— (Minimizar)** | Minimiza el diálogo. |
| **□ (Maximizar)** | Maximiza o restaura el diálogo. |
| **× (Cerrar)** | Cierra el diálogo. Escape primero limpia la búsqueda, luego cierra. |
| **Arrastrar para mover** | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar. |
| **Redimensionamiento en 8 ejes** | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionar. El cursor cambia para indicar la dirección de redimensionamiento. Zona de clic para redimensionar de 12 px. |
| **Conteo de selección** | Muestra "<N> of <M> selected". |

## Atajos de teclado

| Atajo | Acción |
|-------|--------|
| **Ctrl+N** | Añadir una nueva memoria desde el slice activo (funciona incluso cuando el diálogo está cerrado) |
| **Ctrl+F** | Enfocar el campo de búsqueda |
| **F2** o **Ctrl+E** | Editar el nombre de la memoria seleccionada |
| **Delete** o **Backspace** | Eliminar las memorias seleccionadas |
| **Ctrl+Shift+A** | Seleccionar todas las filas visibles |
| **Esc** | Limpiar la búsqueda primero, luego cerrar el diálogo |
| **Doble clic** en una fila de memoria | Sintonizar el slice activo en esa memoria |

## Añadir una memoria rápidamente (Ctrl+N)

Añada un canal de memoria desde el slice activo sin abrir ningún menú — solo presione un atajo de teclado.

### Antes de comenzar

- El radio debe estar conectado y tener un slice activo.
- No es necesario que el diálogo Canales de Memoria esté abierto.

### Pasos

1. Presione **Ctrl+N** en cualquier lugar de la ventana principal de la aplicación.

   Se crea una nueva memoria a partir de la frecuencia, modo y configuración de filtro del slice activo actual.

2. (Opcional) Abra **Settings > Memory...** para ver la nueva memoria en la tabla y editar su nombre u otros campos.

### Consejos

- Ctrl+N funciona incluso cuando otros diálogos tienen el foco, siempre que la ventana principal esté activa.
- Use **Settings > Memory...** para añadir, editar o eliminar memorias en lote. Ctrl+N es el atajo más rápido para una sola memoria.

## Integración de temas

El diálogo Canales de Memoria admite el estilo de temas. La tabla usa el color de fondo definido por el tema para filas alternas. Para aplicar un tema personalizado, configure el contenedor `dialog/memory` en la definición de su tema.
