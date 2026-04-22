# Importar memorias desde un archivo CSV/JSON

Use esta página para cargar canales de memoria almacenados desde un archivo CSV o JSON en AetherSDR. Esto le permite restaurar una copia de seguridad anterior o cargar memorias preparadas en otro sistema.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo Memory Channels requiere una conexión de radio activa.
- Necesita un archivo CSV o JSON de memorias para importar. Para crear uno a partir de sus memorias actuales, consulte [Exportar memorias para copia de seguridad o uso compartido](export-memories-for-backup-or-sharing.md).

## Pasos

1. Abra `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Haga clic en `Import...`.
3. En el explorador de archivos que se abre, navegue hasta su archivo CSV o JSON y selecciónelo.
4. Confirme la selección. AetherSDR leerá el archivo y agregará las memorias a la radio.

## Consejos

- Si la importación encuentra filas con problemas, AetherSDR informa el error por fila, incluyendo el nombre de la memoria y la frecuencia cuando estén disponibles.
- Use el campo `Search:` o el cuadro combinado `Profile:` después de importar para verificar que las memorias esperadas aparezcan en la tabla.

## Relacionados

- [Exportar memorias para copia de seguridad o uso compartido](export-memories-for-backup-or-sharing.md)
- [Descripción general de Memory Channels](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
