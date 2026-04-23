# Agregar una memoria en la frecuencia actual

Guarde la frecuencia del VFO activo, el modo y los ajustes de filtro como un canal de memoria con nombre para poder regresar a él rápidamente más adelante.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Memory Channels requiere una conexión de radio activa.
- Sintonice el slice activo a la frecuencia que desea almacenar.

## Pasos

1. Abra `Settings > Memory...`.
2. Haga clic en `Add`.

El radio crea una nueva fila de memoria con la frecuencia actual del VFO, el modo y los ajustes de filtro. La fila aparece en la tabla de memorias.

3. Para nombrar o editar la nueva entrada de inmediato, seleccione la fila y haga clic en `Edit`, luego modifique los campos en línea.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `Add` | Botón | Crea una nueva memoria en el VFO actual. |
| `Edit` | Botón | Activa el modo de edición en línea sobre la fila de memoria seleccionada. |
| Tabla de memorias | Lista | Muestra todas las memorias almacenadas. Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. |

## Consejos

- Hacer doble clic en una fila de la tabla de memorias sintoniza el slice activo a esa memoria directamente.
- En Linux y Windows, `Ctrl+N` abre la acción Add desde el diálogo Memory Channels.

## Solución de problemas

- **`Add` no tiene efecto** — El diálogo requiere una conexión de radio activa. Si el radio no está conectado, conéctelo primero mediante `Settings > Connect to Radio...` y luego vuelva a abrir `Settings > Memory...`.

## Relacionados

- [Editar el nombre, modo u offset de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar el radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
- [Descripción general de Memory Channels](overview.md)
