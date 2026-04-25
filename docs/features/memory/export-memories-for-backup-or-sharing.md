# Exportar memorias para copia de seguridad o compartir

La exportación le permite guardar canales de memoria seleccionados en un archivo CSV en su computadora para respaldarlos o compartirlos con otros operadores.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. El diálogo Memory Channels requiere una conexión activa con la radio.
- Abra el diálogo Memory Channels desde `Settings > Memory...`.

## Pasos

1. Abra `Settings > Memory...`.
2. Seleccione las memorias que desea exportar. Haga clic en una fila para seleccionarla. Haga Shift-clic para seleccionar un rango. Haga Ctrl-clic (o Command-clic en macOS) para agregar o quitar filas individuales. Haga clic en `Select All` para seleccionar todas las filas de la vista actual.
3. Haga clic en `Export...`.
4. En el diálogo de archivo, elija una carpeta de destino y confirme o cambie el nombre del archivo. El nombre predeterminado se genera automáticamente con el formato `AetherSDR_Memories_<date-time>_v<version>.csv` y se guarda en su carpeta `Documents` de inicio.
5. Confirme el guardado. Las memorias seleccionadas se escriben en el archivo CSV.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| `Select All` | Selecciona todas las filas visibles actualmente en la tabla de memorias. |
| `Export...` | Exporta las filas seleccionadas actualmente a un archivo CSV. |
| `Search:` | Filtra la tabla por nombre de memoria. Úselo para reducir la tabla antes de seleccionar filas para exportar. |
| `Profile:` | Filtra la tabla por perfil global activo. Úselo para aislar las memorias pertenecientes a un perfil específico antes de exportar. |

## Consejos

- Use `Search:` o `Profile:` para filtrar la tabla antes de seleccionar, de modo que `Select All` capture únicamente las filas que desea.
- El archivo exportado está ordenado por frecuencia y luego por índice interno, independientemente del orden de clasificación actual en la tabla.

## Relacionados

- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Descripción general de Memory Channels](overview.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
