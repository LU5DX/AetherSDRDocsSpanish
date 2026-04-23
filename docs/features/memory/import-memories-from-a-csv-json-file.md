# Importar memorias desde un archivo CSV/JSON

Use esta página para cargar memorias almacenadas desde un archivo CSV o JSON en la lista de canales de memoria del radio. Esto le permite restaurar una copia de seguridad, mover memorias entre equipos o cargar una lista de frecuencias preparada fuera de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El diálogo Memory Channels requiere una conexión de radio activa.
- Tenga listo su archivo CSV o JSON y anote su ubicación en el disco.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Haga clic en `Import...`.
3. En el diálogo de archivos que se abre, navegue hasta su archivo CSV o JSON y selecciónelo.
4. Confirme la selección. AetherSDR lee el archivo y agrega las memorias al radio.

## Consejos

- Después de importar, use el campo `Search:` o el cuadro combinado `Profile:` para verificar que las memorias importadas aparezcan correctamente.
- Si importó memorias en un grupo específico, establezca `Profile:` con el nombre de ese grupo para ver solo esas entradas.

## Solución de problemas

- **Las memorias no aparecen después de la importación** — Confirme que el radio esté conectado. El diálogo requiere una conexión de radio activa para registrar las entradas de memoria. Desconecte y vuelva a conectar si es necesario, y luego intente la importación de nuevo.
- **El diálogo de importación se abre pero no se puede seleccionar ningún archivo** — Asegúrese de que su archivo tenga extensión `.csv` o `.json`. Es posible que el diálogo filtre los archivos sin una extensión reconocida.

## Temas relacionados

- [Descripción general de Memory Channels](overview.md)
- [Exportar memorias para copia de seguridad o uso compartido](export-memories-for-backup-or-sharing.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
