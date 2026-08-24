# Diálogo de Canales de Memoria

Administre los canales de memoria del radio: agregue desde el slice activo, edite, busque, filtre por perfil, sintonice, importe/exporte y elimine frecuencias almacenadas.

## Abrir el Diálogo

1. Abra el diálogo de Canales de Memoria: **Settings > Memory...**
2. El diálogo se abre como una ventana sin marco con su propia barra de título. Arrastre la barra de título para mover el diálogo, o arrastre cualquier borde o esquina para redimensionarlo.

## Búsqueda y Filtro

### Buscar por nombre

1. Haga clic en el campo **Search:**.
2. Escriba texto para filtrar la tabla por nombre de memoria. La tabla se actualiza mientras escribe.
3. Haga clic en el botón **×** del campo para borrar la búsqueda, o presione Escape para borrar la búsqueda antes de cerrar el diálogo.
4. Presione Enter para confirmar la búsqueda, o Ctrl+F para enfocar el campo de búsqueda.

### Filtrar por perfil

1. Haga clic en el cuadro combinado **Profile:**.
2. Seleccione un perfil global o de transmisión para filtrar la tabla. Seleccione **All Memories** para mostrar todas las memorias.

## Tabla de Memorias

La tabla de memorias muestra todas las columnas de cada memoria: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset.

- Haga clic en un encabezado de columna para ordenar por esa columna.
- Haga doble clic en una fila para sintonizar el slice activo a esa memoria.
- Ctrl+Shift+A selecciona todas las filas visibles (respetando la búsqueda y el filtro).
- Delete o Backspace elimina las filas seleccionadas (con confirmación).

### Editar una memoria en línea

1. Seleccione una sola fila de memoria.
2. Haga clic en **Edit**, o presione F2 o Ctrl+E. El campo **Name** entra en modo de edición.
3. Edite el nombre y presione Enter para confirmar.
4. Para cambiar otros campos, haga clic en la celda y edítela directamente. Los campos con valores restringidos (Mode, Offset Direction, Tone Mode, Tone Value, Step, Group) utilizan editores de cuadro combinado que se abren inmediatamente al entrar en modo de edición.

## Agregar y Sintonizar

### Agregar una memoria desde el slice activo

1. Asegúrese de que el slice que desea almacenar sea el slice activo.
2. Haga clic en **Add**, o presione Ctrl+N. Se crea una nueva memoria a partir de la configuración del slice activo. No se necesita selección por letra: el slice activo siempre se utiliza.

### Sintonizar una memoria

1. Seleccione una sola fila de memoria.
2. Haga clic en **Tune**. El slice activo sintoniza la frecuencia de esa memoria.

## Importación y Exportación

### Importar memorias desde un archivo CSV

Importe canales de memoria que haya preparado sin conexión o que haya recibido de otro operador al radio. AetherSDR lee un archivo CSV y agrega cada fila válida como una nueva entrada de memoria, mostrando un diálogo de progreso y un resumen de las filas omitidas.

**Antes de comenzar**

- Debe haber un radio conectado.
- El archivo CSV debe usar la misma disposición de columnas que una exportación de AetherSDR (Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset).  
  Consulte [Export memories for backup or sharing](export-memories-for-backup-or-sharing.md) para conocer el formato exacto de los encabezados de columna.

**Pasos**

1. Abra el diálogo de Canales de Memoria: **Settings > Memory...**
2. Haga clic en **Import...**
3. En el selector de archivos, localice y seleccione su archivo CSV y luego haga clic en Open.
4. Espere a que se complete el diálogo de progreso. Un resumen mostrará cuántas memorias se importaron y enumerará las filas omitidas (por ejemplo, debido a una frecuencia no válida o un valor faltante).

### Exportar memorias a un archivo CSV

1. Seleccione las memorias que desea exportar. Si no hay nada seleccionado, se exportan todas las memorias filtradas.
2. Haga clic en **Export...**
3. En el selector de archivos, elija una ubicación y un nombre de archivo, y luego haga clic en Save.
4. AetherSDR valida el CSV generado antes de guardarlo. Si la validación falla, corrija el problema e intente nuevamente.

## Eliminación de Memorias

1. Seleccione una o más filas de memoria.
2. Haga clic en **Remove** (la etiqueta del botón cambia a **Remove Selected** cuando hay más de una fila seleccionada), o presione Delete o Backspace.
3. Confirme la eliminación. Para la eliminación por lotes, un diálogo de progreso muestra el avance de la eliminación.

## Controles de la Barra de Título

- **— (Minimize)**: Minimiza el diálogo.
- **□ (Maximize)**: Maximiza o restaura el diálogo.
- **× (Close)**: Cierra el diálogo. Escape primero borra la búsqueda y luego cierra.
- **Arrastrar para mover**: Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar maximizar/restaurar.
- **Redimensionado de 8 ejes**: Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección del redimensionado.

## Consejos

- Ordene o filtre la tabla de memorias después de importar para verificar las nuevas entradas. Consulte [Sort memory table by column header](sort-memory-table-by-column-header.md) y [Filter memories by profile](filter-memories-by-profile.md).
- La tabla de memorias usa el color de fondo del tema activo para las filas alternadas. El contenedor del diálogo se estiliza con la clave de tema `dialog/memory`.
- El contador de selección en la parte inferior muestra cuántas filas del total están seleccionadas.

## Relacionado

- [Export memories for backup or sharing](export-memories-for-backup-or-sharing.md)
- [Add a memory from the active slice](add-a-memory-from-the-active-slice.md)
- [Delete one or more memories](delete-one-or-more-memories.md)
