# Descripción general del Planificador de Redes

El Planificador de Redes le ayuda a gestionar redes de radio recurrentes — piense en redes semanales de club, redes diarias de DX o ejercicios mensuales de ARES. Puede crear entradas con reglas de recurrencia, configurar recordatorios que muestren un banner en el panadapter y sintonizar una red con un solo clic. Los horarios se pueden importar o exportar como JSON para realizar copias de seguridad o compartirlos.

## Cómo funciona

1. Abra el diálogo mediante `Tools > Net Scheduler...`.
2. La **Net table** enumera cada red programada con su nombre, frecuencia, regla de recurrencia, próxima ocurrencia y hora del recordatorio. Haga doble clic en una fila, o selecciónela y haga clic en **Tune Now**, para QSY en el slice activo.
3. **Add Net** abre el editor de redes donde proporciona un nombre, frecuencia, modo, **Regla de recurrencia** y tiempo de **Recordatorio**.
4. **Capture Current** captura la frecuencia VFO, el modo y los ajustes de filtro actuales para rellenar previamente una entrada nueva o existente.
5. **Edit / Delete** modifica o elimina la red seleccionada.
6. **Import / Export** guarda o carga todo el horario como un archivo `.json`.
7. Cuando una red está próxima, aparece un banner de recordatorio en el panadapter los minutos especificados antes.

Un indicador de **Próxima red** muestra el nombre y la cuenta regresiva hasta la siguiente red programada.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Net table | — | — | Tabla ordenable de redes programadas. Haga doble clic o use **Tune Now** para QSY. Refleja el diseño de la tabla del diálogo Memory. |
| Add Net | — | — | Abre el editor de redes para crear una nueva entrada con nombre, frecuencia, modo, regla de recurrencia y ajustes de recordatorio. |
| Edit / Delete | — | — | Edite la entrada de red seleccionada o elimínela del horario. |
| Tune Now | — | — | Sintoniza el slice activo a la frecuencia de la red seleccionada con el modo y los ajustes de filtro almacenados. Usa la misma ruta de recuperación que las recuperaciones de memoria. |
| Capture Current | — | — | Captura la frecuencia VFO, el modo y el filtro actuales como un preset de sintonización para una red nueva o existente. |
| Import / Export | — | — | Importe o exporte el horario de redes como un archivo JSON para realizar copias de seguridad o compartirlo. |
| Recurrence rule | Weekly | Once / Daily / Weekly / Biweekly / Monthly | Con qué frecuencia se repite la red. Configura el motor de recurrencia del planificador. |
| Reminder | 5 min | 1–60 min | Minutos antes del inicio de la red para mostrar el banner de recordatorio en el panadapter. |

## Relacionados

- [Crear un horario de red recurrente](create-a-recurring-net-schedule.md)
- [Editar o eliminar una red programada](edit-or-delete-a-scheduled-net.md)
- [Sintonizar una red con un solo clic](tune-to-a-net-with-one-click.md)
- [Capturar la frecuencia actual como preset de red](capture-the-current-frequency-as-a-net-preset.md)
- [Importar o exportar horarios de redes](import-or-export-net-schedules.md)
- [Configurar un recordatorio para una red próxima](set-a-reminder-for-an-upcoming-net.md)
