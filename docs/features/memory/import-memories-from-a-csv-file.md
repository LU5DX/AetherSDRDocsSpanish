# Importar memorias desde un archivo CSV

Importe canales de memoria que haya preparado sin conexión o recibido de otro operador en la radio. AetherSDR lee un archivo CSV y agrega cada fila válida como una nueva entrada de memoria, mostrando un diálogo de progreso y un resumen de las filas omitidas.

## Antes de comenzar

- Debe haber una radio conectada.
- El archivo CSV debe usar la misma disposición de columnas que una exportación de AetherSDR (Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset).  
  Consulte [Export memories for backup or sharing](export-memories-for-backup-or-sharing.md) para conocer el formato exacto del encabezado de columnas.

## Pasos

1. Abra el diálogo de canales de memoria: **Settings > Memory...**
2. Haga clic en **Import...**
3. En el selector de archivos, localice y seleccione su archivo CSV, luego haga clic en Open.
4. Espere a que el diálogo de progreso termine. Aparecerá un resumen que muestra cuántas memorias se importaron y lista cualquier fila que se haya omitido (por ejemplo, debido a una frecuencia inválida o un valor faltante).

## Consejos

- Ordene o filtre la tabla de memorias después de la importación para verificar las nuevas entradas. Consulte [Sort memory table by column header](sort-memory-table-by-column-header.md) y [Filter memories by profile](filter-memories-by-profile.md).
- La tabla de memorias usa el color de fondo del tema activo para las filas alternadas. El contenedor del diálogo tiene estilo con la clave de tema `dialog/memory`.

## Relacionados

- [Export memories for backup or sharing](export-memories-for-backup-or-sharing.md)
- [Add a memory from the active slice](add-a-memory-from-the-active-slice.md)
- [Delete one or more memories](delete-one-or-more-memories.md)
