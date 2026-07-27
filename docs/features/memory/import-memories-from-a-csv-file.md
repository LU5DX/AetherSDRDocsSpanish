# Importar memorias desde un archivo CSV

Importe canales de memoria que haya preparado sin conexión o recibido de otro operador en la radio. AetherSDR lee un archivo CSV y agrega cada fila válida como una nueva entrada de memoria, mostrando un diálogo de progreso y un resumen de las filas omitidas.

## Antes de comenzar

- Debe haber una radio conectada.
- El archivo CSV debe usar la misma disposición de columnas que una exportación de AetherSDR (Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset).  
  Consulte [Exportar memorias para respaldo o compartir](export-memories-for-backup-or-sharing.md) para conocer el formato exacto del encabezado de columna.

## Pasos

1. Abra el diálogo de Canales de Memoria: **Settings > Memory...**
2. Haga clic en **Import...**
3. En el selector de archivos, ubique y seleccione su archivo CSV, luego haga clic en Abrir.
4. Espere a que el diálogo de progreso se complete. Aparecerá un resumen que muestra cuántas memorias se importaron y enumera las filas que se omitieron (por ejemplo, debido a una frecuencia inválida o un valor faltante).

## Consejos

- Ordene o filtre la tabla de memorias después de la importación para verificar las nuevas entradas. Consulte [Ordenar tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md) y [Filtrar memorias por perfil](filter-memories-by-profile.md).
- La tabla de memorias usa el color de fondo del tema activo para las filas alternadas. El contenedor del diálogo tiene el estilo con la clave de tema `dialog/memory`.
- La edición en línea admite editores de cuadro combinado para campos restringidos (Mode, Offset Direction, Tone Mode, Tone Value, Step, Group). Estos editores se abren inmediatamente al ingresar al modo de edición, por lo que seleccionar un valor es efectivamente un solo clic.

## Relacionados

- [Exportar memorias para respaldo o compartir](export-memories-for-backup-or-sharing.md)
- [Agregar una memoria desde el slice activo](add-a-memory-from-the-active-slice.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
