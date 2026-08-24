# Canales de Memoria

El diálogo de Canales de Memoria gestiona los canales de memoria de la radio: agregar, editar, buscar, filtrar por perfil, sintonizar, importar, exportar y eliminar frecuencias almacenadas.

## Abrir el diálogo de Canales de Memoria

1. Haga clic en `Settings > Memory...`.

## Qué hace cada control

| Control                     | Comportamiento                                                                                                                                                                     | Notas                                                                                                                                      |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Campo de texto `Search:`    | Filtra la tabla por nombre de memoria.                                                                                                                                             | Tiene botón de borrar; Enter envía la búsqueda. Ctrl+F enfoca el campo de búsqueda.                                                        |
| Cuadro combinado `Profile:` | Filtra la tabla de memorias por el perfil global o de transmisión seleccionado. Se completa desde los perfiles globales y de transmisión activos de la radio.                       |                                                                                                                                            |
| Tabla de memorias           | Muestra y edita filas de memoria. Ordenable haciendo clic en los encabezados de columna (Frequency, Name, Mode). Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. | Selección extendida; modo de edición en línea mediante el botón Edit o F2/Ctrl+E. Delete/Barra espaciadora elimina las filas seleccionadas. Doble clic sintoniza. Ctrl+Shift+A selecciona todo. La tabla usa colores alternos de fila según el tema. |
| Botón `Import...`           | Importa memorias desde un archivo CSV con diálogo de progreso.                                                                                                                     | Muestra el progreso de importación y un resumen con las filas omitidas.                                                                    |
| Botón `Export...`           | Exporta las memorias seleccionadas (o filtradas) a CSV.                                                                                                                            | Valida el CSV generado antes de guardarlo.                                                                                                 |
| Botón `Add`                 | Crea una nueva memoria desde el slice actual (activo).                                                                                                                             | Se eliminó la variante con insignia de letra de slice; agregar siempre apunta al slice activo. Atajo Ctrl+N.                                |
| Botón `Edit`                | Entra en modo de edición en línea en el campo Name de la memoria seleccionada.                                                                                                    | F2 o Ctrl+E también activan la edición. Solo se habilita cuando está seleccionada exactamente una memoria.                                |
| Botón `Tune`                | Sintoniza el slice activo a la memoria seleccionada.                                                                                                                               | Solo se habilita cuando está seleccionada exactamente una memoria.                                                                         |
| Botón `Select All`          | Selecciona todas las filas visibles (respetando búsqueda/filtro).                                                                                                                  | Atajo Ctrl+Shift+A.                                                                                                                        |
| Botón `Remove`              | Elimina las memorias seleccionadas (con confirmación). Muestra progreso para eliminación por lotes.                                                                                | La tecla Delete/Barra espaciadora también lo activa. La etiqueta del botón cambia a 'Remove Selected' cuando hay más de 1 fila seleccionada. |
| Barra de título — Memory Channels | Barra de título sin marco de 18 px con degradado, glifo de agarre a la izquierda y el título del diálogo.                                                                          | Agregado en v26.5.1 (#2509). Usa FramelessWindowTitleBar; redimensionamiento en 8 ejes mediante FramelessResizer.                          |
| — (Minimizar)               | Minimiza el diálogo.                                                                                                                                                               |                                                                                                                                            |
| □ (Maximizar)               | Maximiza o restaura el diálogo.                                                                                                                                                    |                                                                                                                                            |
| × (Cerrar)                  | Cierra el diálogo. Escape primero limpia la búsqueda y luego cierra.                                                                                                               |                                                                                                                                            |
| Arrastrar para mover        | Haga clic y arrastre la barra de título para mover el diálogo.                                                                                                                     | Doble clic en la barra de título alterna entre maximizar/restaurar.                                                                        |
| Redimensionamiento en 8 ejes | Haga clic y arrastre cualquier borde o esquina del diálogo para redimensionarlo. El cursor cambia para indicar la dirección de redimensionamiento.                                 | Zona de redimensionamiento de 12 px mediante FramelessResizer.                                                                             |
| Conteo de selección         | Muestra '<N> de <M> seleccionados'.                                                                                                                                                |                                                                                                                                            |

## Editar campos de memoria

Para editar un campo de memoria directamente en la tabla:

1. Haga doble clic en la celda que desea editar, o seleccione una memoria y presione F2.
2. Para campos restringidos (Mode, Offset Direction, Tone Mode, Tone Value, Step, Group), aparece un cuadro combinado prellenado con valores válidos. La lista se despliega inmediatamente para selección con un clic.
   - Si el valor actual no está en la lista (por ejemplo, de una memoria heredada), permanece visible y editable.
3. Para campos editables, puede escribir un valor. Los campos numéricos (Tone Value, Repeater Offset) muestran un validador para evitar entradas no válidas.
4. Presione Enter para confirmar la edición, o Escape para cancelar.

## Filtrar memorias por perfil

Use el filtro de perfil en el diálogo de Canales de Memoria para reducir la tabla de memorias a las entradas que pertenecen a un perfil global específico. Esto es útil cuando tiene una lista de memorias grande y desea ver solo los canales relevantes a su contexto operativo actual.

### Antes de comenzar

- La radio debe estar conectada. El diálogo de Canales de Memoria requiere una conexión activa con la radio.
- Debe existir al menos un perfil global en la radio. El cuadro combinado `Profile:` se completa desde los perfiles globales activos de la radio.

### Pasos

1. Abra `Settings > Memory...`.
2. Localice el cuadro combinado `Profile:` en la fila de filtros en la parte superior del diálogo.
3. Haga clic en el cuadro combinado `Profile:` y seleccione el perfil por el que desea filtrar.
4. La tabla de memorias se actualiza inmediatamente para mostrar solo las entradas que coinciden con el perfil seleccionado.

Para limpiar el filtro y mostrar todas las memorias, seleccione la entrada en blanco o predeterminada en la parte superior del cuadro combinado `Profile:`.

## Consejos

- El filtro por perfil y la búsqueda por nombre (`Search:`) funcionan juntos. Puede seleccionar un perfil en `Profile:` y escribir en `Search:` para reducir aún más los resultados por nombre de memoria.
- El botón `Export...` respeta el filtro de perfil actual: solo se exportan las memorias visibles bajo el filtro activo.
- La barra de título sin marco y el redimensionamiento de bordes en 8 ejes ahora forman parte de la infraestructura persistente del diálogo. El diálogo recuerda su geometría entre sesiones mediante la clave de configuración `MemoryDialogGeometry`. El comportamiento de la barra de título (arrastrar para mover, doble clic para maximizar/restaurar) y el redimensionamiento de bordes en 8 ejes permanecen como se describe en la tabla de controles.
- La tabla de memorias usa colores alternos de fila según el tema. La apariencia se adapta al esquema de color de fondo del tema activo para el diálogo.

## Relacionado

- [Resumen de Canales de Memoria](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Exportar memorias para respaldo o intercambio](export-memories-for-backup-or-sharing.md)
