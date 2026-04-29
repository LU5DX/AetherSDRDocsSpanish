# Sintonizar la radio en una memoria almacenada

Abra el diálogo Memory Channels para buscar una frecuencia almacenada y enviarla directamente al slice receptor activo.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El diálogo Memory Channels requiere una conexión de radio activa.
- Debe haber al menos una memoria ya almacenada. Consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md) si no tiene ninguna.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Localice la memoria que desea. Use el campo `Search:` para filtrar por nombre, o use el cuadro combinado `Profile:` para reducir la lista por perfil.
3. Haga clic en la fila de la tabla de memorias para seleccionarla.
4. Haga clic en `Tune`.

El slice activo se sintoniza en la frecuencia, el modo y los ajustes de filtro almacenados en esa memoria.

**Acceso directo:** Haga doble clic en cualquier fila de la tabla de memorias para sintonizar de inmediato sin necesidad de hacer clic en `Tune`.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| `Search:` | Filtra la tabla de memorias para mostrar las filas cuyo nombre coincide con el texto ingresado. Presione Enter o borre el campo para restablecer el filtro. |
| `Profile:` | Filtra la tabla para mostrar las memorias pertenecientes al perfil global seleccionado. |
| Tabla de memorias | Muestra todas las memorias almacenadas. Las columnas incluyen Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset y DIGU Offset. Haga clic en el encabezado de una columna para ordenar por esa columna. |
| `Tune` | Sintoniza el slice activo en la memoria seleccionada. Requiere exactamente una fila seleccionada. |

## Consejos

- Si no puede ver la memoria que desea, verifique si `Profile:` está configurado con un filtro que la excluye. Ajuste `Profile:` para mostrar todas las entradas.
- En Linux y Windows, mantenga presionado Ctrl y haga clic para seleccionar filas individuales sin deseleccionar las demás. En macOS, use Command-clic. Solo se utiliza la primera memoria seleccionada al hacer clic en `Tune`.

## Solución de problemas

- **`Tune` no tiene efecto o está deshabilitado** — Confirme que haya exactamente una fila seleccionada en la tabla de memorias y que AetherSDR esté conectado a la radio.
- **La memoria que desea no aparece en la tabla** — Es posible que el filtro `Search:` o `Profile:` la esté ocultando. Borre el campo `Search:` y ajuste `Profile:` para mostrar todas las entradas.

## Relacionado

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Recuperar una memoria de repetidor FM y restaurar el desplazamiento y el tono CTCSS](recall-an-fm-repeater-memory-and-restore-offset-and-ctcss-tone.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Descripción general de Memory Channels](overview.md)
