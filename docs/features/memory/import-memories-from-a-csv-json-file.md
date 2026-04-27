# Importar memorias desde un archivo CSV/JSON

Cargue un archivo de memorias guardado en AetherSDR para poblar los canales de memoria de su radio con frecuencias, modos y desplazamientos almacenados.

## Antes de comenzar

- Su radio debe estar conectada. El diálogo Memory Channels requiere una conexión de radio activa.
- Tenga listo en el disco su archivo de memorias CSV o JSON.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Haga clic en `Import...`.
3. En el selector de archivos que se abre, navegue hasta su archivo CSV o JSON y selecciónelo.
4. Confirme la selección. AetherSDR lee el archivo y agrega las memorias a la radio.

## Consejos

- Después de importar, use el campo `Search:` o el combo `Profile:` para verificar que las memorias importadas aparezcan con los nombres y grupos esperados.
- Si desea hacer una copia de seguridad antes de importar, haga clic primero en `Export...` para guardar las memorias actuales en un archivo.

## Solución de problemas

- **Las memorias importadas no aparecen en la tabla** — El archivo puede contener errores de formato o campos no compatibles. Verifique que el archivo sea una exportación CSV o JSON válida de AetherSDR o de una fuente compatible. Las filas con campos obligatorios faltantes (como la frecuencia) pueden omitirse de forma silenciosa.
- **Import... no es seleccionable** — El diálogo requiere una conexión de radio activa. Conéctese primero al FLEX-8600 mediante `Settings > Connect to Radio...` y luego vuelva a abrir el diálogo Memory Channels.

## Relacionados

- [Exportar memorias para respaldo o intercambio](export-memories-for-backup-or-sharing.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Descripción general de Memory Channels](overview.md)
