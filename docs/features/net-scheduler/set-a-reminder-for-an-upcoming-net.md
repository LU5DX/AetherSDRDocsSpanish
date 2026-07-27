# Configurar un recordatorio para una red próxima

Configure AetherSDR para mostrar un banner en el panadapter antes de que comience una red programada, para que no se pierda su reunión semanal o diaria al aire.

## Antes de comenzar

- Necesita al menos una entrada de red en el calendario. Si aún no ha creado una, consulte [Crear un calendario de red recurrente](create-a-recurring-net-schedule.md).
- No se requiere conexión a la radio para configurar recordatorios, pero el banner solo aparecerá mientras AetherSDR esté en ejecución y conectado.

## Pasos

1. Abra el diálogo **Net Scheduler**: **Tools > Net Scheduler...**
2. Seleccione la entrada de red para la que desea un recordatorio desde la **Net table**.
3. Haga clic en **Edit**.
4. En el editor de red, ajuste el control giratorio **Reminder** al número de minutos antes de la hora de inicio de la red en que desea ser alertado (rango: 1–60 minutos). El valor predeterminado es 5 minutos.
5. Confirme que la **Recurrence rule** esté configurada con el calendario deseado (Once, Daily, Weekly, Biweekly o Monthly).
6. Guarde la entrada.

Cuando la red se acerque, aparecerá un banner en el panadapter mostrando el nombre de la red y la cuenta regresiva.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---------|---------------------|--------------|-----------------|----------------|
| **Reminder** | 5 min | 1–60 min | None | Minutos antes del inicio de la red para mostrar el banner de recordatorio en el panadapter. |
| **Recurrence rule** | Weekly | Once / Daily / Weekly / Biweekly / Monthly | None | Frecuencia con que se repite la red. Afecta cuándo se activa el recordatorio. |

## Consejos

- Para eliminar un recordatorio, ajuste el control giratorio **Reminder** a su valor mínimo (1 minuto) o elimine por completo la entrada de red.
- El indicador **Next net** en el diálogo **Net Scheduler** muestra el nombre y la cuenta regresiva hasta la próxima red programada, para que pueda verificar la configuración de sus recordatorios.

## Relacionado

- [Descripción general del Net Scheduler](overview.md)
- [Crear un calendario de red recurrente](create-a-recurring-net-schedule.md)
- [Editar o eliminar una red programada](edit-or-delete-a-scheduled-net.md)
