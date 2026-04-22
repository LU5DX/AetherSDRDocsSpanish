# Agregar una memoria en la frecuencia actual

Guarde la frecuencia, el modo y los ajustes de filtro del VFO activo como un canal de memoria con nombre para poder volver a él más adelante sin necesidad de resintonizar manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Memory Channels requiere una conexión de radio activa.
- Sintonice el slice activo en la frecuencia que desea almacenar antes de abrir el diálogo.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Haga clic en `Add`.

El radio crea una nueva fila de memoria en la frecuencia VFO actual. La nueva entrada aparece en la tabla de memorias con las columnas completadas a partir del slice activo, incluyendo Frequency, Mode y los ajustes de filtro.

3. Para nombrar la memoria de inmediato, seleccione la nueva fila y haga clic en `Edit`, luego escriba un nombre en la columna Name.
4. Presione Enter o haga clic fuera de la celda para confirmar la edición.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| `Add` | Crea una nueva memoria en la frecuencia VFO actual. |
| `Edit` | Activa el modo de edición en línea en la fila de memoria seleccionada. Úselo después de agregar una memoria para establecer el Name, Group u otros campos. |
| Tabla de memorias | Muestra todas las memorias almacenadas. Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. |

## Consejos

- Hacer doble clic en una fila de memoria sintoniza el slice activo en esa memoria. Si agrega una memoria y desea verificarla, haga doble clic en la fila en lugar de hacer clic en `Tune`.
- En Linux y Windows, Ctrl-clic agrega o elimina filas individuales de la selección sin perder las demás filas seleccionadas.
- Puede usar `Ctrl+N` como atajo de teclado para agregar una memoria sin hacer clic en el botón `Add`.

## Relacionado

- [Editar el nombre, modo u offset de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar el radio en una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Descripción general de Memory Channels](overview.md)
