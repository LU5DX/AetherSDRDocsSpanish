# Eliminar una o más memorias

Elimine los canales de memoria almacenados que ya no necesite. AetherSDR solicita confirmación antes de eliminar, por lo que ninguna memoria se pierde accidentalmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Memory Channels requiere una conexión activa con el radio.
- Sepa qué memorias desea eliminar. Use el campo Search:, Profile: o la tabla de memorias para filtrar la lista primero si es necesario.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Seleccione la memoria o las memorias que desea eliminar:
   - Haga clic en una sola fila para seleccionarla.
   - Mantenga presionada la tecla Shift y haga clic en una segunda fila para seleccionar un rango contiguo.
   - En Linux y Windows, mantenga presionada la tecla Ctrl y haga clic en filas individuales para agregarlas o quitarlas de la selección. En macOS, use Command-clic.
   - Presione Ctrl+Shift+A o haga clic en Select All para seleccionar todas las filas visibles (respetando la búsqueda y el filtro).
3. Confirme su selección asegurándose de que el número correcto de filas esté seleccionado:
   - El indicador de recuento de selección en el área inferior derecha del diálogo muestra `<N> of <M> selected` (donde N es el número de filas seleccionadas y M es el número total de filas).
   - La etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada.
4. Haga clic en Remove una sola vez, no dos. La etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada. Si hace clic dos veces seguidas, el primer clic elimina las memorias y el segundo clic no elimina nada (porque la selección se ha limpiado).

Las memorias seleccionadas se eliminan permanentemente del radio. Para eliminaciones por lotes, un diálogo de progreso muestra el estado de la eliminación.

## Consejos

- Si tiene una lista de memorias larga, use el campo Search: o el cuadro combinado Profile: para filtrar la tabla antes de usar Select All. Esto le permite seleccionar y eliminar rápidamente un subconjunto de memorias sin tener que elegir cada fila manualmente.
- La eliminación no se puede deshacer desde AetherSDR. Exporte sus memorias antes de una eliminación masiva si es posible que las necesite más adelante.
- Presione Escape para limpiar el campo Search:; presionar Escape nuevamente cierra el diálogo.
- El diálogo tiene una barra de título sin marco con un glifo de agarre a la izquierda. Haga doble clic en la barra de título para alternar maximizar/restaurar.
- Para mover el diálogo, haga clic y arrastre la barra de título. Para redimensionar el diálogo, haga clic y arrastre cualquier borde o esquina: el cursor cambia para indicar la dirección de redimensionamiento. El borde superior está reservado para arrastrar la barra de título; el redimensionamiento desde el borde superior no está disponible en la zona de 12 px.
- La apariencia del diálogo sigue el tema activo. La tabla de memorias usa colores de fila alternados del tema.

## Relacionado

- [Exportar memorias para respaldo o uso compartido](export-memories-for-backup-or-sharing.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Descripción general de Memory Channels](overview.md)
