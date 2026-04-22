# Sintonizar la radio en una memoria almacenada

Abra el diálogo Memory Channels para localizar una frecuencia almacenada y enviarla al slice receptor activo con un solo clic o doble clic.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Memory Channels requiere una conexión activa con la radio.
- Debe haber al menos una memoria almacenada. Consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md) si su lista está vacía.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Opcional: escriba un nombre en el campo **Search:** para filtrar la tabla, o elija un grupo en el menú desplegable **Profile:** para reducir la lista.
3. Haga clic en la fila de la memoria a la que desea sintonizar. La fila se resalta y el contador de selección en la parte inferior derecha se actualiza.
4. Haga clic en **Tune**. El slice activo se sintoniza en la frecuencia, el modo y los ajustes de filtro almacenados en esa memoria.

Como alternativa, haga doble clic en cualquier fila de la tabla de memorias para sintonizar de inmediato sin usar el botón **Tune**.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Search:** | Filtra la tabla para mostrar las filas cuyo nombre coincide con el texto escrito. Incluye un botón para borrar; presione Enter para confirmar. |
| **Profile:** | Filtra la tabla para mostrar las memorias pertenecientes al perfil global seleccionado. |
| Tabla de memorias | Muestra todas las memorias almacenadas. Las columnas incluyen Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset y DIGU Offset. Haga clic en el encabezado de una columna para ordenar por esa columna. |
| **Tune** | Sintoniza el slice activo en la memoria seleccionada. |
| Contador de selección | Muestra el número de filas seleccionadas actualmente (indicado como `N selected`). |

## Consejos

- Hacer doble clic en una fila sintoniza la radio sin necesidad de hacer clic en **Tune**, lo cual es más rápido al navegar entre memorias.
- Use **Search:** para saltar rápidamente a una memoria por nombre. La tabla se filtra mientras escribe; presione Enter para sintonizar la fila resaltada.
- Shift-clic selecciona un rango de filas. En Linux y Windows, Ctrl-clic agrega o quita filas individuales de la selección. En macOS, use Command-clic en su lugar.

## Solución de problemas

- **Tune no hace nada** — Verifique que la radio esté conectada. El botón **Tune** requiere una conexión activa con la radio. Compruebe el estado de la conexión y vuelva a conectarse mediante `Settings > Connect to Radio...` si es necesario.
- **La memoria que busca no es visible** — Es posible que un término de búsqueda o el filtro Profile la esté ocultando. Borre el campo **Search:** y restablezca **Profile:** a su valor predeterminado para mostrar todas las memorias.

## Relacionado

- [Descripción general de Memory Channels](overview.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
