# Eliminar uno o varios canales de memoria

Elimine los canales de memoria almacenados que ya no necesite. AetherSDR solicita confirmación antes de eliminar, por lo que ningún canal se pierde accidentalmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La función Memory Channels requiere una conexión activa con el radio.
- Identifique los canales que desea eliminar. Use Search: o Profile: para reducir la lista primero si es necesario.

## Pasos

1. Abra `Settings > Memory...` para abrir el cuadro de diálogo Memory Channels.
2. Seleccione el canal o los canales que desea eliminar:
   - Haga clic en una fila individual para seleccionarla.
   - Haga Shift-click en una segunda fila para seleccionar un rango contiguo.
   - En Linux y Windows, haga Ctrl-click en filas individuales para agregarlas o quitarlas de la selección. En macOS, use Command-click.
   - Haga clic en Select All para seleccionar todas las filas que se muestran en ese momento en la tabla.
3. Confirme su selección verificando el indicador de cantidad de elementos seleccionados en la esquina inferior derecha del cuadro de diálogo (mostrado como `<N> selected`).
4. Haga clic en Remove.
5. Confirme la eliminación en el cuadro de diálogo de confirmación que aparece.

Los canales de memoria seleccionados se eliminan de forma permanente del radio.

## Consejos

- Si tiene una lista de memoria extensa, use el campo Search: o el cuadro combinado Profile: para filtrar la tabla antes de usar Select All. Esto le permite seleccionar y eliminar rápidamente un subconjunto de canales sin tener que elegir cada fila manualmente.
- La eliminación no se puede deshacer desde AetherSDR. Exporte sus canales de memoria antes de una eliminación masiva si es posible que los necesite más adelante.

## Relacionados

- [Exportar canales de memoria para respaldo o compartir](export-memories-for-backup-or-sharing.md)
- [Buscar canales de memoria por nombre](search-memories-by-name.md)
- [Filtrar canales de memoria por perfil](filter-memories-by-profile.md)
- [Importar canales de memoria desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Descripción general de Memory Channels](overview.md)
