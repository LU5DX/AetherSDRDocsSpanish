# Importar o exportar horarios de redes

Guarde su horario de redes como un archivo JSON para realizar copias de seguridad, transferirlo a otro equipo o compartirlo con otro usuario de AetherSDR. También puede cargar un horario exportado previamente de vuelta a la aplicación.

## Antes de comenzar

- Asegúrese de tener al menos una entrada de red en la tabla del Net Scheduler, o un archivo JSON exportado previamente listo para importar.

## Pasos

1. Abra el Net Scheduler: `Tools > Net Scheduler...`
2. Haga clic en **Import / Export**.
3. Para **exportar**:
   - Seleccione la carpeta de destino y el nombre del archivo en el diálogo de archivo.
   - Haga clic en **Save**. El horario se escribe como un archivo JSON.
4. Para **importar**:
   - Seleccione el archivo JSON que desea cargar.
   - Haga clic en **Open**. Las entradas de red existentes se reemplazan por el horario importado.

## Consejos

- El archivo JSON exportado contiene todas las entradas de red con sus nombres, frecuencias, modos, reglas de recurrencia, ajustes de recordatorio y preajustes de sintonización.
- La importación sobrescribe su horario actual; no hay fusión. Exporte primero su horario existente si desea conservarlo.

## Solución de problemas

- **La importación no hace nada o no muestra redes**: Es posible que el archivo seleccionado no sea un JSON válido de horario de redes de AetherSDR. Asegúrese de importar un archivo exportado previamente por AetherSDR.

## Relacionados

- [Descripción general del Net Scheduler](overview.md)
- [Crear un horario de red recurrente](create-a-recurring-net-schedule.md)
- [Editar o eliminar una red programada](edit-or-delete-a-scheduled-net.md)
- [Sintonizar una red con un solo clic](tune-to-a-net-with-one-click.md)
