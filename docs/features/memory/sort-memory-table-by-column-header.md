# Canales de Memoria

El diálogo de Canales de Memoria (`Settings > Memory...») gestiona las frecuencias almacenadas en el radio: permite agregar, editar, buscar, filtrar por perfil, sintonizar, importar, exportar y eliminar memorias.

## Controles

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| **Buscar:** | campo_de_texto | Filtra la tabla por nombre de memoria. Incluye un botón de limpiar; presione Enter para enviar. Presione Ctrl+F para enfocar el campo de búsqueda. |
| **Perfil:** | cuadro_combinado | Filtra las memorias por perfil global o de transmisión activo. El valor predeterminado es "Todas las memorias". Recopila los nombres de perfil de los perfiles globales y de transmisión del radio. |
| **Tabla de memorias** | lista | Muestra y edita las filas de memoria. Se puede ordenar haciendo clic en los encabezados de columna (Frecuencia, Nombre, Modo y otros). Las columnas incluyen: Grupo, Propietario, Frecuencia, Nombre, Modo, Paso, Dirección de desplazamiento FM, Desplazamiento del repetidor, Modo de tono, Valor de tono, Silenciador, Nivel de silenciador, Filtro RX bajo, Filtro RX alto, Marca RTTY, Desplazamiento RTTY, Desplazamiento DIGL, Desplazamiento DIGU. Soporta selección extendida; edición en línea mediante el botón Editar o F2/Ctrl+E. Suprimir/Retroceso elimina las filas seleccionadas. Doble clic sintoniza una memoria. Ctrl+Mayús+A selecciona todo. |
| **Importar...** | botón | Importa memorias desde un archivo CSV. Muestra un diálogo de progreso y un resumen con las filas omitidas. |
| **Exportar...** | botón | Exporta las memorias seleccionadas (o filtradas) a CSV. Valida el CSV generado antes de guardarlo. |
| **Agregar** | botón | Crea una nueva memoria a partir del segmento (slice) activo actual. Atajo: Ctrl+N. |
| **Editar** | botón | Activa el modo de edición en línea en el campo Nombre de la memoria seleccionada. Solo está habilitado cuando hay exactamente una memoria seleccionada. Atajo: F2 o Ctrl+E. |
| **Sintonizar** | botón | Sintoniza el segmento activo a la memoria seleccionada. Solo está habilitado cuando hay exactamente una memoria seleccionada. |
| **Seleccionar todo** | botón | Selecciona todas las filas visibles (respetando la búsqueda y el filtro). Atajo: Ctrl+Mayús+A. |
| **Eliminar** | botón | Elimina las memorias seleccionadas (con confirmación). Muestra el progreso para eliminaciones por lote. La etiqueta del botón cambia a "Eliminar seleccionados" cuando hay más de una fila seleccionada. Atajo: Suprimir o Retroceso. |
| **Barra de título — Canales de Memoria** | indicador | Barra de título de 18 px sin marco con degradado, un asa de agarre a la izquierda y el título del diálogo. Agregado en v26.5.1 (#2509). |
| **— (Minimizar)** | botón | Minimiza el diálogo. |
| **□ (Maximizar)** | botón | Maximiza o restaura el diálogo. |
| **× (Cerrar)** | botón | Cierra el diálogo. Presione Escape para limpiar primero el campo de búsqueda, luego cerrar. |
| **Arrastrar para mover** | asa_de_arrastre | Haga clic y arrastre la barra de título para mover el diálogo. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. |
| **Redimensionar en 8 direcciones** | asa_de_arrastre | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento. La zona de impacto para redimensionar tiene 12 px de ancho. |
| **Recuento de selección** | indicador | Muestra "<N> de <M> seleccionados". |

### Agregar una Memoria desde un Segmento

1. Asegúrese de que el segmento deseado esté activo (haga clic en su barra de segmento).
2. Haga clic en **Agregar** (o presione Ctrl+N).
3. Aparece una nueva fila en la tabla de memorias con la frecuencia, el modo y otras configuraciones del segmento activo.

**Nota:** Se eliminó la variante de selección de segmento por letra. Agregar siempre apunta al segmento activo.

### Editar una Memoria en Línea

La tabla de memorias admite la edición en línea para campos restringidos (como Modo, Paso, Modo de tono, Dirección de desplazamiento) mediante delegados de cuadro combinado. Al hacer doble clic o presionar F2 en una celda restringida, aparece una lista desplegable con valores válidos. Para los campos editables, puede escribir un valor personalizado que el radio valida al confirmar.

1. Seleccione la fila de memoria que desea editar.
2. Haga clic en **Editar** (o presione F2 o Ctrl+E) para entrar en modo de edición en el campo Nombre.
3. Para editar otros campos, haga doble clic en la celda o presione F2 mientras la celda está seleccionada.
4. Para los campos de cuadro combinado (Modo, Paso, Dirección de desplazamiento, Modo de tono, Valor de tono, Grupo), la lista se abre inmediatamente. Seleccione un valor o escriba un valor editable.
5. Presione Enter para confirmar el cambio, o Escape para cancelar.

### Sintonizar una Memoria

1. Seleccione exactamente una memoria en la tabla.
2. Haga clic en **Sintonizar**. El segmento activo se sintoniza a la frecuencia de la memoria.

**Consejo:** Haga doble clic en cualquier memoria para sintonizar directamente sin usar el botón Sintonizar.

### Eliminar Memorias

1. Seleccione una o más memorias (use Ctrl+clic para selección no contigua, Mayús+clic para un rango, o Ctrl+Mayús+A para seleccionar todas las filas visibles).
2. Haga clic en **Eliminar** (o presione Suprimir o Retroceso).
3. Confirme la eliminación cuando se le solicite. Aparece una barra de progreso para eliminaciones por lote.

### Importar Memorias desde CSV

1. Haga clic en **Importar...**.
2. Seleccione un archivo CSV. Un diálogo de progreso muestra el proceso de importación.
3. Revise el resumen para ver las filas omitidas.

### Exportar Memorias a CSV

1. Seleccione las memorias a exportar, o aplique búsqueda/filtro para limitar el conjunto.
2. Haga clic en **Exportar...**.
3. Elija una ubicación de guardado y un nombre de archivo. El CSV exportado se valida antes de guardarlo.

## Ordenar la Tabla de Memorias

Haga clic en cualquier encabezado de columna ordenable para ordenar la tabla por esa columna. Vuelva a hacer clic en el mismo encabezado para invertir la dirección de ordenamiento.

- La columna **Frecuencia** utiliza ordenamiento numérico (14.225 se ordena entre 14.200 y 14.300).
- Los indicadores de ordenamiento aparecen en el encabezado.
- El ordenamiento no afecta el índice almacenado en el radio.
- Los filtros de búsqueda y perfil permanecen activos durante el ordenamiento.

## Relacionados

- [Ordenar tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Sintonizar el radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
