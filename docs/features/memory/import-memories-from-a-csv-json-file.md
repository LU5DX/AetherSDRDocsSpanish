# Importar memorias desde un archivo CSV/JSON

Importe archivos de memoria previamente exportados o de terceros en la lista de canales de memoria de AetherSDR. Use esta función al migrar memorias desde otro equipo, restaurar una copia de seguridad o cargar una lista de frecuencias compartida.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El diálogo Memory Channels requiere una conexión activa con el equipo.
- Tenga su archivo de memoria CSV o JSON disponible en el disco.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Haga clic en `Import...`.
3. En el explorador de archivos que se abre, navegue hasta su archivo CSV o JSON y selecciónelo.
4. Confirme la selección. AetherSDR lee el archivo y agrega las memorias al equipo.

## Consejos

- Después de importar, use el campo `Search:` para filtrar por nombre, o el cuadro combinado `Profile:` para filtrar por grupo; esto le ayudará a confirmar que las entradas importadas aparecieron correctamente.
- Si importó memorias en un grupo específico, establezca `Profile:` con el nombre de ese grupo para ver únicamente esas entradas.

## Solución de problemas

- **Las memorias no aparecen tras la importación** — Verifique que el archivo sea una exportación CSV o JSON válida producida por AetherSDR o una fuente compatible. Los archivos con campos obligatorios ausentes (como Frequency o Mode) pueden omitirse o generar entradas sin nombre.
- **Import... aparece en gris o no está disponible** — El diálogo requiere una conexión activa con el equipo. Conéctese primero al FLEX-8600 mediante `Settings > Connect to Radio...` y luego vuelva a abrir `Settings > Memory...`.

## Relacionados

- [Exportar memorias para respaldo o uso compartido](export-memories-for-backup-or-sharing.md)
- [Descripción general de Memory Channels](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
