# Exportar memorias para respaldo o compartir

Exporte uno o más canales de memoria a un archivo CSV para hacer una copia de seguridad o compartirlos con otros operadores.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Memory Channels requiere una conexión activa al radio.
- Debe tener al menos una memoria almacenada. Si la tabla de memorias está vacía, no hay nada que exportar.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Seleccione las filas que desea exportar. Haga clic en una fila para seleccionarla. Haga clic con Shift para seleccionar un rango. Haga clic con Ctrl (Command en macOS) para agregar o quitar filas individuales de la selección.
3. Para exportar todas las memorias, haga clic en `Select All` para seleccionar todas las filas.
4. Haga clic en `Export...`.
5. En el diálogo de archivo que se abre, confirme o cambie la ruta de destino y el nombre del archivo, luego guarde el archivo. El nombre de archivo predeterminado se basa en la fecha y hora actuales y la versión de la aplicación, y se guarda en su carpeta `Documents`.

## Consejos

- Use el cuadro combinado `Profile:` para filtrar la tabla a un solo grupo antes de hacer clic en `Select All`. Esto le permite exportar únicamente las memorias que pertenecen a un perfil particular sin seleccionar filas manualmente.
- Use el campo `Search:` para filtrar por nombre si desea revisar el contenido de la tabla antes de seleccionar.

## Relacionado

- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Descripción general de Memory Channels](overview.md)
