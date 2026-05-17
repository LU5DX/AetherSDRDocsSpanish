# Eliminar uno o más recuerdos

Elimine los canales de memoria almacenados que ya no necesite. AetherSDR solicita confirmación antes de eliminar, por lo que ningún recuerdo se pierde accidentalmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Memory Channels requiere una conexión activa con el radio.
- Sepa qué recuerdos desea eliminar. Use Search: o Profile: para filtrar primero la lista si es necesario.

## Pasos

1. Abra `Settings > Memory...` para abrir el cuadro de diálogo Memory Channels.
2. Seleccione el recuerdo o los recuerdos que desea eliminar:
   - Haga clic en una sola fila para seleccionarla.
   - Haga clic con Mayús en una segunda fila para seleccionar un rango contiguo.
   - En Linux y Windows, haga clic con Ctrl en filas individuales para agregarlas o eliminarlas de la selección. En macOS, use Command-clic.
   - Presione Ctrl+Shift+A o haga clic en Select All para seleccionar todas las filas visibles (respetando la búsqueda y el filtro).
3. Confirme su selección verificando el indicador de recuento de selección en el área inferior derecha del cuadro de diálogo (se muestra como `<N> de <M> seleccionados`).
4. Haga clic en Remove (la etiqueta del botón cambia a "Remove Selected" cuando se selecciona más de una fila). Alternativamente, presione Delete o Backspace.
5. Confirme la eliminación en el cuadro de diálogo de confirmación que aparece.

Los recuerdos seleccionados se eliminan permanentemente del radio. Para eliminaciones por lotes, un cuadro de diálogo de progreso muestra el estado de la eliminación.

## Consejos

- Si tiene una lista de recuerdos larga, use el campo Search: o el cuadro combinado Profile: para filtrar la tabla antes de usar Select All. Esto le permite seleccionar y eliminar rápidamente un subconjunto de recuerdos sin tener que elegir cada fila manualmente.
- La eliminación no se puede deshacer desde AetherSDR. Exporte sus recuerdos antes de una eliminación masiva si es posible que los necesite más adelante.
- Presione Escape para limpiar el campo Search:; presionar Escape nuevamente cierra el cuadro de diálogo.
- Haga doble clic en la barra de título para alternar maximizar/restaurar el cuadro de diálogo.
- Para mover el cuadro de diálogo, haga clic y arrastre la barra de título. Para cambiar el tamaño del cuadro de diálogo, haga clic y arrastre cualquier borde o esquina; el cursor cambia para indicar la dirección del redimensionamiento.

## Relacionado

- [Export memories for backup or sharing](export-memories-for-backup-or-sharing.md)
- [Search memories by name](search-memories-by-name.md)
- [Filter memories by profile](filter-memories-by-profile.md)
- [Import memories from a CSV/JSON file](import-memories-from-a-csv-json-file.md)
- [Memory Channels overview](overview.md)
