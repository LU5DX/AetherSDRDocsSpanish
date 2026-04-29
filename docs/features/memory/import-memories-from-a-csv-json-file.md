# Importar memorias desde un archivo CSV/JSON

Cargue un archivo de memorias guardado en AetherSDR para llenar los canales de memoria de su radio con frecuencias, modos y desplazamientos almacenados.

## Antes de comenzar

- Su radio debe estar conectada. El cuadro de diálogo Memory Channels requiere una conexión de radio activa.
- Tenga su archivo de memorias CSV o JSON disponible en el disco.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el cuadro de diálogo Memory Channels.
2. Haga clic en `Import...`.
3. En el selector de archivos que se abre, navegue hasta su archivo CSV o JSON y selecciónelo.
4. Confirme la selección. AetherSDR lee el archivo y agrega las memorias a la radio.

## Consejos

- Después de importar, use el campo `Search:` o el cuadro combinado `Profile:` para verificar que las memorias importadas aparezcan con los nombres y grupos esperados.
- Si desea hacer una copia de seguridad antes de importar, haga clic en `Export...` primero para guardar las memorias actuales en un archivo.

## Solución de problemas

- **Las memorias importadas no aparecen en la tabla** — El archivo puede contener errores de formato o campos no compatibles. Verifique que el archivo sea una exportación CSV o JSON válida de AetherSDR o de una fuente compatible. Las filas con campos obligatorios faltantes (como la frecuencia) pueden omitirse silenciosamente.
- **Import... no es seleccionable** — El cuadro de diálogo requiere una conexión de radio activa. Conéctese al FLEX-8600 primero mediante `Settings > Connect to Radio...` y luego vuelva a abrir el cuadro de diálogo Memory Channels.

## Relacionados

- [Exportar memorias para copia de seguridad o para compartir](export-memories-for-backup-or-sharing.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Descripción general de Memory Channels](overview.md)
