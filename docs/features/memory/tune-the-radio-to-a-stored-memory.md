# Sintonizar la radio en una memoria almacenada

Abra el cuadro de diálogo Memory Channels para localizar una frecuencia almacenada y enviarla directamente al slice receptor activo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El cuadro de diálogo Memory Channels requiere una conexión de radio activa.
- Debe haber al menos una memoria almacenada. Consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md) si la lista está vacía.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el cuadro de diálogo Memory Channels.
2. Opcional: escriba un nombre en el campo **Search:** para reducir la lista, o elija un grupo en el menú desplegable **Profile:** para filtrar por perfil.
3. Haga clic en la fila de la tabla de memorias que contiene la frecuencia deseada.
4. Haga clic en **Tune**.

El slice activo se sintoniza de inmediato en la frecuencia, el modo y la configuración de filtro almacenados en esa memoria.

**Atajo:** Haga doble clic en cualquier fila de la tabla de memorias para sintonizar sin necesidad de hacer clic en **Tune**.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Search:** | Filtra la tabla para mostrar las filas cuyo nombre coincide con el texto ingresado. Presione Enter o borre el campo con el botón de borrado integrado. |
| **Profile:** | Limita la tabla a las memorias que pertenecen al perfil global seleccionado. |
| Tabla de memorias | Muestra todas las memorias almacenadas. Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. |
| **Tune** | Sintoniza el slice activo en la memoria seleccionada. Requiere que haya exactamente una fila seleccionada. |
| Contador de selección | Muestra cuántas filas están seleccionadas en ese momento (por ejemplo, `1 selected`). |

## Consejos

- En Linux y Windows, mantenga presionada la tecla Ctrl y haga clic para agregar o quitar filas individuales de la selección. En macOS, use Command-clic. Cuando hace clic en **Tune**, solo se sintoniza la primera memoria seleccionada.
- Shift-clic selecciona un rango contiguo de filas.
- Para encontrar una memoria rápidamente, haga clic en el encabezado de una columna para ordenar por esa columna y luego desplácese hasta la frecuencia o el nombre deseado.

## Solución de problemas

- **Tune no está disponible** — No hay ninguna fila seleccionada. Haga clic primero en una fila de la tabla de memorias.
- **La radio no cambia de frecuencia** — Confirme que AetherSDR está conectado a la radio. Una conexión perdida deshabilita todos los comandos de radio.

## Relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
- [Descripción general de Memory Channels](overview.md)
