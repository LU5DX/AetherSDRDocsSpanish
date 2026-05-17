# Filtrar memorias por perfil

Use el filtro de Perfil en el diálogo Canales de Memoria para restringir la tabla de memorias a las entradas que pertenecen a un perfil global específico. Esto es útil cuando tiene una lista de memorias extensa y desea ver solo los canales relevantes para su contexto operativo actual.

## Antes de comenzar

- La radio debe estar conectada. El diálogo Canales de Memoria requiere una conexión activa con la radio.
- Debe existir al menos un perfil global en la radio. El cuadro combinado `Profile:` se llena con los perfiles globales activos de la radio.

## Pasos

1. Abra `Settings > Memory...`.
2. Localice el cuadro combinado `Profile:` en la fila de filtros en la parte superior del diálogo.
3. Haga clic en el cuadro combinado `Profile:` y seleccione el perfil por el que desea filtrar.
4. La tabla de memorias se actualiza inmediatamente para mostrar solo las entradas que coinciden con el perfil seleccionado.

Para eliminar el filtro y mostrar todas las memorias, seleccione la entrada en blanco o predeterminada en la parte superior del cuadro combinado `Profile:`.

## Qué hace cada control

| Control                     | Comportamiento                                                                                                                                                                                                                         | Notas                                                                                                                                      |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Campo de texto `Search:`    | Filtra la tabla por nombre de memoria.                                                                                                                                                                                                 | Tiene botón de borrar; Enter confirma. Ctrl+F enfoca el campo de búsqueda.                                                                 |
| Cuadro combinado `Profile:` | Filtra la tabla de memorias por el perfil global o de transmisión seleccionado. Se llena con los perfiles globales activos y los perfiles de transmisión de la radio.                                                                  |                                                                                                                                            |
| Tabla de memorias           | Muestra y edita filas de memoria. Ordenable haciendo clic en los encabezados de columna (Frecuencia, Nombre, Modo). Columnas: Grupo, Propietario, Frecuencia, Nombre, Modo, Paso, Dir. Despl. FM TX, Desplazamiento Repetidor, Modo Tono, Valor Tono, Silenciador, Nivel Silenciador, Filtro RX Bajo, Filtro RX Alto, Marca RTTY, Desplazamiento RTTY, Despl. DIGL, Despl. DIGU. | ExtendedSelection; modo de edición en línea mediante botón Editar o F2/Ctrl+E. Supr/Retroceso elimina filas seleccionadas. Doble clic sintoniza. Ctrl+Mayús+A selecciona todo. |
| Botón `Import...`           | Importa memorias desde un archivo CSV con un diálogo de progreso.                                                                                                                                                                      | Muestra el progreso de importación y un resumen con las filas omitidas.                                                                                 |
| Botón `Export...`           | Exporta las memorias seleccionadas (o filtradas) a CSV.                                                                                                                                                                                | Valida el CSV generado antes de guardarlo.                                                                                                 |
| Botón `Add`                 | Crea una nueva memoria a partir del segmento (slice) activo actual.                                                                                                                                                                    | Atajo Ctrl+N.                                                                                                                           |
| Botón `Edit`                | Activa el modo de edición en línea en el campo Nombre de la memoria seleccionada.                                                                                                                                                      | F2 o Ctrl+E también activan la edición. Solo disponible cuando está seleccionada exactamente una memoria.                                                         |
| Botón `Tune`                | Sintoniza el segmento activo en la memoria seleccionada.                                                                                                                                                                               | Solo disponible cuando está seleccionada exactamente una memoria.                                                                                          |
| Botón `Select All`          | Selecciona cada fila visible (respetando la búsqueda/filtro).                                                                                                                                                                          | Atajo Ctrl+Mayús+A.                                                                                                                     |
| Botón `Remove`              | Elimina las memorias seleccionadas (con confirmación). Muestra progreso para la eliminación por lotes.                                                                                                                                 | También se activa con la tecla Supr/Retroceso. La etiqueta del botón cambia a 'Remove Selected' cuando hay más de 1 fila seleccionada.                                        |
| Barra de título — Memory Channels | Barra de título de 18 píxeles, sin marco y con degradado, con un ícono de agarre a la izquierda y el título del diálogo.                                                                                                                | Añadido en v26.5.1 (#2509). Usa FramelessWindowTitleBar; cambio de tamaño en 8 ejes mediante FramelessResizer.                                                |
| — (Minimizar)                | Minimiza el diálogo.                                                                                                                                                                                                                        |                                                                                                                                            |
| □ (Maximizar)                | Maximiza o restaura el diálogo.                                                                                                                                                                                                            |                                                                                                                                            |
| × (Cerrar)                   | Cierra el diálogo. Escape primero limpia la búsqueda, luego cierra.                                                                                                                                                                      |                                                                                                                                            |
| Arrastrar para mover        | Haga clic y arrastre la barra de título para mover el diálogo.                                                                                                                                                                             | Haga doble clic en la barra de título para alternar entre maximizar y restaurar.                                                                                     |
| Cambio de tamaño en 8 ejes  | Haga clic y arrastre cualquier borde o esquina del diálogo para cambiar su tamaño. El cursor cambia para indicar la dirección del cambio de tamaño.                                                                                      | Zona de activación de 12 píxeles para el cambio de tamaño mediante FramelessResizer.                                                                                                |
| Contador de selección       | Muestra '<N> de <M> seleccionados'.                                                                                                                                                 |                                                                                                                                            |

## Consejos

- El filtrado por perfil y la búsqueda por nombre (`Search:`) funcionan juntos. Puede seleccionar un perfil en `Profile:` y escribir en `Search:` para reducir aún más los resultados por nombre de memoria.
- El botón `Export...` respeta el filtro de perfil actual: solo se exportan las memorias visibles bajo el filtro activo.
- La barra de título sin marco y el cambio de tamaño de borde en 8 ejes ahora forman parte de la infraestructura del diálogo persistente. El diálogo recuerda su geometría entre sesiones mediante la clave de ajuste `MemoryDialogGeometry`. El comportamiento de la barra de título (arrastrar para mover, doble clic para maximizar/restaurar) y el cambio de tamaño de borde en 8 ejes se mantienen como se describe en la tabla de controles.

## Relacionado

- [Resumen de Canales de Memoria](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Exportar memorias para respaldo o compartir](export-memories-for-backup-or-sharing.md)
