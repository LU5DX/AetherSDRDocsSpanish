# Importar memorias desde un archivo CSV/JSON

Use esta página para cargar frecuencias almacenadas y configuraciones de canal desde un archivo CSV o JSON hacia la lista de canales de memoria de AetherSDR. Esto es útil para restaurar una copia de seguridad o cargar un archivo de frecuencias compartido por otro operador.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Memory Channels requiere una conexión de radio activa.
- Tenga listo en su sistema de archivos local el archivo CSV o JSON que desea importar.

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Haga clic en `Import...`.
3. En el explorador de archivos que se abre, navegue hasta su archivo CSV o JSON y selecciónelo.
4. Confirme la selección para iniciar la importación. AetherSDR procesará el archivo y agregará las memorias a la tabla.

## Sugerencias

- Después de importar, use el campo **Search:** o el cuadro combinado **Profile:** para verificar que las memorias esperadas aparezcan en la tabla.
- Si importó memorias en un grupo específico, seleccione ese grupo en **Profile:** para filtrar la tabla y confirmar que las entradas se cargaron correctamente.

## Solución de problemas

- **Las memorias importadas no aparecen en la tabla** — Es posible que el archivo no coincida con el formato CSV o JSON esperado. Intente exportar primero una memoria existente para ver la estructura esperada y luego compárela con su archivo de importación. Consulte [Exportar memorias para copia de seguridad o compartir](export-memories-for-backup-or-sharing.md).
- **Import... aparece atenuado o no disponible** — AetherSDR no está conectado a la radio. Conéctese primero mediante `Settings > Connect to Radio...` y vuelva a intentarlo.

## Relacionados

- [Exportar memorias para copia de seguridad o compartir](export-memories-for-backup-or-sharing.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
