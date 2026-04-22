# Editar el nombre, modo u offset de una memoria en línea

Use la edición en línea para cambiar los campos de una memoria almacenada — como su nombre, modo, offset de repetidor u otra columna — sin salir del diálogo Memory Channels.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La edición en línea requiere una conexión activa con el radio.
- El diálogo Memory Channels debe estar abierto. Si no lo está, vaya a `Settings > Memory...`.

## Pasos

1. Abra `Settings > Memory...`.
2. En la tabla de memorias, haga clic en la fila que desea cambiar para seleccionarla.
3. Haga clic en **Edit**.
4. La fila seleccionada entra en modo de edición en línea. Haga clic en la celda que desea cambiar.
5. Escriba el nuevo valor y presione Enter para confirmar, o presione Escape para cancelar.
6. Repita el proceso para cualquier otra celda de la fila que desee actualizar.
7. Haga clic en cualquier lugar fuera de la fila, o seleccione una fila diferente, para finalizar la edición.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Campo de texto **Search:** | Filtra la tabla para mostrar las filas cuyo nombre coincide con el texto escrito. Tiene un botón para borrar el contenido; presione Enter para activar el filtro. |
| Cuadro combinado **Profile:** | Filtra la tabla para mostrar las memorias pertenecientes al perfil global seleccionado. |
| Tabla de memorias | Muestra todas las filas de memoria. Columnas disponibles para edición en línea: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. |
| **Edit** | Activa el modo de edición en línea en la fila de memoria seleccionada. |

## Consejos

- Hacer doble clic en una fila sintoniza el slice activo a esa memoria en lugar de abrirla para edición. Para editar, use el botón **Edit** en su lugar.
- Para localizar una memoria específica antes de editarla, escriba su nombre en el campo **Search:**. La tabla se filtra a medida que escribe.
- Puede ordenar la tabla haciendo clic en el encabezado de una columna para facilitar la búsqueda de la memoria deseada antes de hacer clic en **Edit**. Consulte [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md).

## Solución de problemas

- **El botón Edit no tiene efecto** — Confirme que haya exactamente una fila seleccionada y que AetherSDR esté conectado al radio. La edición en línea no está disponible sin una conexión activa con el radio.
- **Los cambios no aparecen después de editar** — Presione Enter para confirmar el valor de una celda antes de hacer clic fuera de ella. Presionar Escape descarta el cambio.

## Temas relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
- [Sintonizar el radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
