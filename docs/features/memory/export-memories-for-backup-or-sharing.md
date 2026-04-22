# Exportar memorias para respaldo o compartir

Exporte uno o más canales de memoria almacenados a un archivo CSV para guardarlos de forma segura o para compartirlos con otro operador.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. El diálogo Memory Channels requiere una conexión de radio activa.
- Las memorias que desea exportar deben existir previamente en la tabla de memorias.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Seleccione las memorias que desea exportar. Haga clic en una fila para seleccionarla. Haga Shift-clic para seleccionar un rango. Haga Ctrl-clic (o Command-clic en macOS) para agregar o quitar filas individuales. Para exportar todas las memorias, haga clic en `Select All`.
3. Opcionalmente, use el campo `Search:` o el cuadro combinado `Profile:` para filtrar la tabla antes de seleccionar, de modo que solo sean visibles las memorias relevantes.
4. Haga clic en `Export...`.
5. En el diálogo de archivo que se abre, confirme o cambie la ubicación de guardado y el nombre del archivo, luego guarde el archivo. El nombre de archivo predeterminado incluye la fecha y hora actuales y la versión de AetherSDR (por ejemplo, `AetherSDR_Memories_01-15-25_14_30_v4.1.5.csv`), y se guarda en su carpeta `Documents` de inicio.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| `Search:` | Filtra la tabla de memorias por nombre. Borre el texto con el botón de borrado integrado o eliminando el texto manualmente. |
| `Profile:` | Filtra la tabla de memorias según el perfil global activo. |
| Tabla de memorias | Muestra todas las memorias que coinciden con el filtro actual. El recuento de selección se muestra en el indicador `<N> selected` en la parte inferior derecha. |
| `Select All` | Selecciona todas las filas visibles actualmente en la tabla. |
| `Export...` | Escribe las memorias seleccionadas en un archivo CSV de su elección. |

## Consejos

- El indicador de recuento de selección en la parte inferior del diálogo muestra cuántas filas están seleccionadas actualmente, lo que ayuda a confirmar que tiene las memorias correctas antes de hacer clic en `Export...`.
- Si desea exportar únicamente un grupo, use el filtro `Profile:` para reducir la tabla a ese grupo primero y, a continuación, haga clic en `Select All` antes de exportar.
- La ruta de exportación predeterminada es su carpeta `Documents` de inicio. Cámbiela en el diálogo de archivo si prefiere una ubicación diferente.

## Temas relacionados

- [Importar memorias desde un archivo CSV/JSON](import-memories-from-a-csv-json-file.md)
- [Descripción general de Memory Channels](overview.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
