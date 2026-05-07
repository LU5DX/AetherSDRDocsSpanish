# Importar memorias desde un archivo CSV/JSON

Cargue un archivo de memorias guardado en AetherSDR para poblar los canales de memoria de su radio con frecuencias, modos y desplazamientos almacenados.

## Antes de comenzar

- Su radio debe estar conectado. El diálogo de Canales de Memoria requiere una conexión activa con el radio.
- Tenga listo su archivo de memorias CSV o JSON en el disco.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el diálogo de Canales de Memoria.
2. Haga clic en `Import...`.
3. En el selector de archivos que se abre, navegue hasta su archivo CSV o JSON y selecciónelo.
4. Confirme la selección. AetherSDR lee el archivo y agrega las memorias al radio.

## Consejos

- Después de importar, use el campo `Search:` o el cuadro combinado `Profile:` para verificar que las memorias importadas aparezcan con los nombres y grupos esperados.
- Si desea hacer una copia de seguridad antes de importar, primero haga clic en `Export...` para guardar las memorias actuales en un archivo.

## Solución de problemas

- **Las memorias importadas no aparecen en la tabla** — El archivo puede contener errores de formato o campos no admitidos. Verifique que el archivo sea una exportación CSV o JSON válida de AetherSDR o de una fuente compatible. Las filas con campos obligatorios faltantes (como la frecuencia) podrían omitirse silenciosamente.
- **Import... no se puede hacer clic** — El diálogo requiere una conexión activa con el radio. Conéctese primero al FLEX-8600 mediante `Settings > Connect to Radio...`, luego vuelva a abrir el diálogo de Canales de Memoria.

## Relacionados

- [Exportar memorias para copia de seguridad o compartir](export-memories-for-backup-or-sharing.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Resumen de Canales de Memoria](overview.md)
