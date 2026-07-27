# Sintonice una red con un solo clic

Utilice el Net Scheduler para sintonizar instantáneamente su slice activo a la frecuencia, modo y configuración de filtro de una red programada.

## Antes de comenzar

- El Net Scheduler debe contener al menos una entrada de red (consulte [Create a recurring net schedule](create-a-recurring-net-schedule.md)).
- Se requiere una conexión de radio para transmitir comandos de sintonización.

## Pasos

1. Abra el Net Scheduler: `Tools > Net Scheduler...`.
2. Seleccione la red que desea sintonizar en la tabla de redes.
3. Haga clic en **Tune Now**.

El slice activo cambia inmediatamente a la frecuencia, modo y filtro almacenados de la red.

## Función de cada control

| Control | Comportamiento |
|---------|----------------|
| **Tune Now** | Sintoniza el slice activo a la frecuencia de la red seleccionada con el modo y configuración de filtro almacenados. Utiliza la misma política de recuperación de memoria que las recuperaciones de memoria. |
| **Tabla de redes** | Haga doble clic en cualquier entrada de red para realizar la misma acción de sintonización con un solo clic que **Tune Now**. |

## Relacionados

- [Net Scheduler overview](overview.md)
- [Create a recurring net schedule](create-a-recurring-net-schedule.md)
- [Capture the current frequency as a net preset](capture-the-current-frequency-as-a-net-preset.md)
