# Eliminar una o más memorias

Elimine los canales de memoria almacenados que ya no necesite. AetherSDR solicita confirmación antes de eliminar, por lo que ninguna memoria se pierde accidentalmente.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. Memory Channels requiere una conexión activa con el equipo.
- Sepa qué memorias desea eliminar. Use el campo Search: o Profile: para reducir la lista primero si es necesario.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo de Memory Channels.
2. Seleccione la memoria o memorias que desea eliminar:
   - Haga clic en una sola fila para seleccionarla.
   - Mayús+clic en una segunda fila para seleccionar un rango contiguo.
   - En Linux y Windows, Ctrl+clic en filas individuales para agregarlas o quitarlas de la selección. En macOS, use Comando+clic.
   - Presione Ctrl+Shift+A o haga clic en Select All para seleccionar todas las filas visibles (respetando la búsqueda y el filtro).
3. Confirme su selección verificando el indicador de recuento de selección en la esquina inferior derecha del diálogo (se muestra como `<N> de <M> seleccionados`).
4. Haga clic en Remove (la etiqueta del botón cambia a "Remove Selected" cuando hay más de una fila seleccionada). Alternativamente, presione Delete o Backspace.
5. Confirme la eliminación en el diálogo de confirmación que aparece.

Las memorias seleccionadas se eliminan permanentemente del equipo. Para eliminaciones por lotes, un diálogo de progreso muestra el estado de eliminación.

## Consejos

- Si tiene una lista larga de memorias, use el campo Search: o el cuadro combinado Profile: para filtrar la tabla antes de usar Select All. Esto le permite seleccionar y eliminar rápidamente un subconjunto de memorias sin tener que elegir cada fila manualmente.
- La eliminación no se puede deshacer desde AetherSDR. Exporte sus memorias antes de una eliminación masiva si es posible que las necesite más adelante.
- Presione Escape para limpiar el campo Search:; presionar Escape nuevamente cierra el diálogo.
- Haga doble clic en la barra de título para maximizar/restaurar el diálogo.

## Relacionado

- [Exportar memorias para respaldo o intercambio](export-memories-for-backup-or-sharing.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Resumen de Memory Channels](overview.md)
