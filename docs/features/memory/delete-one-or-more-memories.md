# Eliminar uno o más recuerdos

Elimine los canales de memoria almacenados que ya no necesite. AetherSDR solicita confirmación antes de eliminar, por lo que ninguna memoria se pierde accidentalmente.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. Memory Channels requiere una conexión activa al equipo.
- Sepa qué memorias desea eliminar. Use Search: o Profile: para acotar la lista primero si es necesario.

## Pasos

1. Abra `Settings > Memory...` para abrir el cuadro de diálogo Memory Channels.
2. Seleccione la memoria o memorias que desea eliminar:
   - Haga clic en una sola fila para seleccionarla.
   - Mayús+clic en una segunda fila para seleccionar un rango contiguo.
   - En Linux y Windows, Ctrl+clic en filas individuales para agregarlas o eliminarlas de la selección. En macOS, use Comando+clic.
   - Presione Ctrl+Shift+A o haga clic en Select All para seleccionar todas las filas visibles (respetando la búsqueda y el filtro).
3. Confirme su selección verificando el indicador de cantidad de selección en la parte inferior derecha del cuadro de diálogo (se muestra como `<N> de <M> seleccionados`).
4. Haga clic en Remove (la etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada). Alternativamente, presione Delete o Backspace.
5. Confirme la eliminación en el cuadro de diálogo de confirmación que aparece.

Las memorias seleccionadas se eliminan permanentemente del equipo. Para eliminaciones por lotes, un cuadro de diálogo de progreso muestra el estado de la eliminación.

## Consejos

- Si tiene una lista larga de memorias, use el campo Search: o el cuadro combinado Profile: para filtrar la tabla antes de usar Select All. Esto le permite seleccionar y eliminar rápidamente un subconjunto de memorias sin tener que elegir cada fila manualmente.
- La eliminación no se puede deshacer desde dentro de AetherSDR. Exporte sus memorias antes de una eliminación masiva si pudiera necesitarlas más adelante.
- Presione Escape para limpiar el campo Search:; presionar Escape nuevamente cierra el cuadro de diálogo.
- Haga doble clic en la barra de título para alternar maximizar/restaurar el cuadro de diálogo.
- Para mover el cuadro de diálogo, haga clic y arrastre la barra de título. Para cambiar el tamaño del cuadro de diálogo, haga clic y arrastre cualquier borde o esquina; el cursor cambia para indicar la dirección del redimensionamiento.
- La apariencia del cuadro de diálogo sigue el tema activo. La tabla de memorias usa colores de fila alternados del tema.

## Relacionados

- [Export memorias para respaldo o uso compartido](export-memories-for-backup-or-sharing.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Descripción general de Memory Channels](overview.md)
