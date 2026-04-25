# Agregar una memoria en la frecuencia actual

Guarde la frecuencia, el modo y los ajustes de filtro del VFO activo como un canal de memoria con nombre para poder regresar a esa frecuencia rápidamente más adelante.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo Memory Channels requiere una conexión de radio activa.
- Sintonice el slice activo en la frecuencia que desea almacenar.

## Pasos

1. Abra `Settings > Memory...`.
2. Haga clic en `Add`.

La nueva memoria aparece en la tabla de memorias con la frecuencia actual del VFO precargada en la columna Frequency.

3. Para asignarle un nombre a la memoria de inmediato, seleccione la nueva fila, haga clic en `Edit`, escriba un nombre en la columna Name y presione Enter para confirmar.

## Qué hace cada control

| Control | Descripción |
|---|---|
| `Add` | Crea una nueva fila de memoria en la frecuencia actual del VFO. |
| `Edit` | Activa el modo de edición en línea sobre la fila seleccionada para que pueda actualizar cualquier campo. |
| Memory table | Muestra todas las memorias almacenadas. Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. |

## Consejos

- Hacer doble clic en una fila sintoniza el slice activo en esa memoria sin cerrar el diálogo.
- En Linux y Windows, Ctrl-clic agrega o quita filas individuales de la selección. En macOS, use Command-clic.

## Relacionado

- [Editar el nombre, el modo o el desplazamiento de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar la radio en una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
- [Descripción general de Memory Channels](overview.md)
