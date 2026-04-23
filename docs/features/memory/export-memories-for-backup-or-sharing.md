# Exportar memorias para copia de seguridad o compartir

Exporte uno o más canales de memoria a un archivo CSV para hacer una copia de seguridad o compartirlos con otro operador.

## Antes de comenzar

- Es necesario tener conectada una radio FLEX-8600. El diálogo Memory Channels requiere una conexión de radio activa.
- Las memorias que desea exportar deben existir previamente. Consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md) si necesita crearlas primero.

## Pasos

1. Abra `Settings > Memory...`.
2. Seleccione las memorias que desea exportar. Haga clic en una fila para seleccionarla. Shift-click selecciona un rango. Ctrl-click (o Command-click en macOS) agrega o quita filas individuales. Para exportar todas las memorias, haga clic en `Select All`.
3. Haga clic en `Export...`.
4. En el diálogo de archivo, elija una carpeta de destino y confirme o cambie el nombre del archivo. El nombre predeterminado tiene la forma `AetherSDR_Memories_<date-time>_v<version>.csv` dentro de su carpeta Documentos.
5. Confirme el guardado. Las memorias seleccionadas se escriben en el archivo CSV.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| `Select All` | Selecciona todas las filas de la tabla de memorias. |
| `Export...` | Exporta las filas de memoria actualmente seleccionadas a un archivo CSV. |
| `Profile:` | Filtra la tabla según el perfil global activo, lo que limita las memorias visibles y seleccionables antes de exportar. |
| `Search:` | Filtra la tabla por nombre de memoria, permitiéndole localizar memorias específicas antes de seleccionarlas. |
| Contador de selección | Muestra el número de filas actualmente seleccionadas (por ejemplo, `3 selected`) en el área inferior derecha del diálogo. |

## Consejos

- Si solo desea exportar las memorias pertenecientes a un grupo, use el cuadro combinado `Profile:` para filtrar la tabla antes de hacer clic en `Select All`. Solo se mostrarán las filas visibles que coincidan con ese perfil, lo que facilita la selección masiva.
- La ruta de exportación predeterminada coloca el archivo en su carpeta `Documents` de inicio con una marca de tiempo y un número de versión en el nombre, lo que le ayuda a distinguir múltiples copias de seguridad.

## Relacionado

- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Descripción general de Memory Channels](overview.md)
