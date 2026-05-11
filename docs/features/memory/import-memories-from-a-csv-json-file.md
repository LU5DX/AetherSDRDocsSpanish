# Importar memorias desde un archivo CSV/JSON

Cargue un archivo de memorias guardado en AetherSDR para poblar los canales de memoria de su radio con frecuencias, modos y desplazamientos almacenados.

## Antes de comenzar

- Su radio debe estar conectado. El cuadro de diálogo de Canales de Memoria requiere una conexión activa con el radio.
- Tenga su archivo de memorias CSV o JSON listo en el disco.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el cuadro de diálogo de Canales de Memoria.
2. Haga clic en `Import...`.
3. En el selector de archivos que se abre, navegue hasta su archivo CSV o JSON y selecciónelo.
4. Confirme la selección. AetherSDR lee el archivo y agrega las memorias al radio. Aparece un cuadro de diálogo de progreso que muestra el avance de la importación, y un resumen informa sobre cualquier fila omitida.

## Consejos

- Después de importar, use el campo `Search:` o el cuadro combinado `Profile:` para verificar que las memorias importadas aparezcan con los nombres y grupos esperados.
- Si desea realizar una copia de seguridad antes de importar, primero haga clic en `Export...` para guardar las memorias actuales en un archivo.
- La barra de título tiene un glifo de agarre a la izquierda y permite arrastrar para mover. Haga doble clic en la barra de título para alternar entre maximizar y restaurar. Los botones de minimizar, maximizar y cerrar se encuentran en la esquina superior derecha.

## Solución de problemas

- **Las memorias importadas no aparecen en la tabla** — El archivo puede contener errores de formato o campos no compatibles. Verifique que el archivo sea una exportación CSV o JSON válida de AetherSDR o de una fuente compatible. Las filas con campos obligatorios faltantes (como la frecuencia) pueden omitirse silenciosamente.
- **Import... no se puede hacer clic** — El diálogo requiere una conexión activa con el radio. Conéctese primero al FLEX-8600 a través de `Settings > Connect to Radio...`, luego vuelva a abrir el cuadro de diálogo de Canales de Memoria.

## Relacionado

- [Exportar memorias para respaldo o compartir](export-memories-for-backup-or-sharing.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Descripción general de Canales de Memoria](overview.md)
