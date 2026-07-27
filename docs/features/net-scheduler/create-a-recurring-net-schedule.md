# Crear un horario de red recurrente

Configure un horario de red personal con reglas de recurrencia para que AetherSDR le recuerde antes de cada red semanal, diaria o mensual y le permita sintonizar su frecuencia con un solo clic.

## Antes de comenzar

- AetherSDR debe estar ejecutándose (no se requiere una conexión de radio para crear o editar entradas de horario).
- Conozca la frecuencia, el modo y la frecuencia de repetición de la red.

## Pasos

1. Abra el Planificador de Redes: `Tools > Net Scheduler...`
2. Haga clic en **Add Net**.
3. En el editor de redes, ingrese un nombre para la red.
4. Configure la frecuencia y el modo usando uno de estos métodos:
   - Escriba manualmente la frecuencia y seleccione un modo de las opciones disponibles.
   - Haga clic en **Capture Current** para copiar la frecuencia, el modo y la configuración del filtro del slice activo en la nueva entrada.
5. En el cuadro combinado **Recurrence rule**, elija con qué frecuencia se repite la red:
   - **Once** — se ejecuta una sola vez
   - **Daily**
   - **Weekly**
   - **Biweekly**
   - **Monthly**
6. Configure el spinbox **Reminder** con la cantidad de minutos antes de la hora de inicio de la red en la que desea que aparezca el banner de recordatorio en el panadapter (1–60 minutos, valor predeterminado 5 min).
7. Confirme la entrada. La nueva red aparece en la **Net table** ordenada por hora de inicio.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado / Rango | Clave de configuración |
|---------|----------|------------------------------|------------------------|
| **Net table** | Lista ordenable de todas las redes programadas que muestra nombre, frecuencia, regla de recurrencia, próxima ocurrencia y tiempo de recordatorio. Haga doble clic para QSY. | — | `Nets` |
| **Add Net** | Abre el editor de redes para crear una nueva entrada de horario. | — | — |
| **Edit / Delete** | Edite las propiedades de la red seleccionada o elimínela del horario. | — | — |
| **Tune Now** | Sintoniza inmediatamente el slice activo a la frecuencia, modo y filtro de la red seleccionada. | — | — |
| **Capture Current** | Rellena la frecuencia, modo y filtro actuales del VFO en el editor de redes como una presintonía. | — | — |
| **Import / Export** | Guarde o cargue todo el horario de redes como un archivo JSON. | — | — |
| **Recurrence rule** | Con qué frecuencia se repite la red. | **Once** / Daily / Weekly / Biweekly / Monthly | — |
| **Reminder** | Minutos antes de que comience la red para mostrar el banner de recordatorio en el panadapter. | 5 min (1–60 min) | — |

## Consejos

- Use **Capture Current** mientras está sintonizado en la frecuencia habitual de una red para evitar escribir los kHz exactos y el modo manualmente.
- El indicador **Next net** en el diálogo de Net Scheduler muestra el nombre de la próxima red programada y un contador regresivo.

## Relacionado

- [Overview](overview.md)
- [Capture the current frequency as a net preset](capture-the-current-frequency-as-a-net-preset.md)
- [Edit or delete a scheduled net](edit-or-delete-a-scheduled-net.md)
- [Set a reminder for an upcoming net](set-a-reminder-for-an-upcoming-net.md)
- [Tune to a net with one click](tune-to-a-net-with-one-click.md)
- [Import or export net schedules](import-or-export-net-schedules.md)
