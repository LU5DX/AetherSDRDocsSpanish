# Sintonizar la radio con una memoria almacenada

Abra un canal de memoria guardado y vuelva a sintonizar el slice (segmento de recepción) activo a la frecuencia, modo y ajustes de filtro almacenados.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El diálogo Memory Channels requiere una conexión de radio activa.
- Debe haber al menos una memoria almacenada. Consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md) si la lista está vacía.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Opcional: Escriba un nombre en el campo **Search:** para reducir la lista, o seleccione un grupo en el menú desplegable **Profile:** para filtrar por perfil.
3. Haga clic en la fila de la memoria a la que desea sintonizar. La fila se resalta y el contador de selección se actualiza.
4. Haga clic en **Tune**.

El slice activo se sintoniza a la frecuencia, el modo y los ajustes de filtro almacenados de la memoria seleccionada.

**Atajo:** Haga doble clic en cualquier fila de la tabla de memorias para sintonizar de inmediato sin necesidad de hacer clic en **Tune**.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **Search:** | Filtra la tabla para mostrar las filas cuyo nombre coincide con el texto escrito. Presione Enter para confirmar, o use el botón de borrar para restablecer. |
| **Profile:** | Filtra la tabla para mostrar las memorias que pertenecen al perfil global seleccionado. |
| Tabla de memorias | Muestra todas las memorias almacenadas. Las columnas incluyen Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset y DIGU Offset. Haga clic en un encabezado de columna para ordenar. |
| **Tune** | Sintoniza el slice activo con la memoria seleccionada. Se habilita cuando hay exactamente una fila seleccionada. |

## Consejos

- Para seleccionar un rango contiguo de memorias, haga clic en la primera fila y luego Shift-clic en la última. Para agregar o quitar filas individuales de una selección, use Ctrl-clic (Command-clic en macOS). Solo la memoria individual sobre la que actúa con **Tune** o con doble clic se aplica al slice.
- Si conoce el nombre de la memoria, escríbalo en **Search:** y presione Enter para sintonizar directamente desde el teclado sin necesidad de usar el ratón.

## Solución de problemas

- **Tune no está disponible** — No hay ninguna fila seleccionada. Haga clic en una fila de la tabla primero.
- **La tabla está vacía** — Es posible que haya un filtro de perfil activo. Restablezca **Profile:** a su estado sin filtro, o borre el campo **Search:** para mostrar todas las memorias.

## Relacionados

- [Descripción general de Memory Channels](overview.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
