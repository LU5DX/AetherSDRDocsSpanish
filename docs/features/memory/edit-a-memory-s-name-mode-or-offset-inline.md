# Editar el nombre, el modo o el desplazamiento de una memoria en línea

El diálogo Memory Channels permite editar cualquier campo de una memoria almacenada — incluidos su nombre, modo, desplazamiento de repetidor y más — directamente en la tabla, sin abrir un formulario separado.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Memory Channels requiere una conexión activa con el radio.
- La memoria que desea editar debe existir previamente en la tabla. Para crear una, consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md).

## Pasos

1. Abra `Settings > Memory...`.
2. En la tabla de memorias, haga clic en la fila que desea editar para seleccionarla.
3. Haga clic en **Edit**. La fila seleccionada entra en modo de edición en línea y sus celdas se vuelven editables.
4. Haga clic en la celda que desea modificar — por ejemplo, la columna **Name**, **Mode** o **Repeater Offset** — y escriba el nuevo valor.
5. Presione Enter o haga clic en otra celda para confirmar cada cambio.
6. Repita el proceso para cualquier otra celda de la misma fila.
7. Haga clic fuera de la fila o seleccione una fila diferente para finalizar la edición.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Edit** | Activa el modo de edición en línea en la fila de memoria actualmente seleccionada. |
| Campo de texto **Search:** | Filtra la tabla por nombre de memoria. Úselo para localizar la fila que desea editar antes de hacerlo. Tiene un botón para borrar el contenido; presione Enter para aplicar el filtro. |
| Cuadro combinado **Profile:** | Filtra la tabla para mostrar únicamente las memorias que pertenecen al perfil global seleccionado. Reduzca la lista desde aquí si la tabla es extensa. |
| Tabla de memorias | Muestra todas las filas de memoria. Las columnas editables incluyen: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. |

## Consejos

- También puede usar el teclado para navegar entre celdas mientras se encuentra en modo de edición en línea.
- Para localizar una memoria rápidamente antes de editarla, escriba parte de su nombre en el campo **Search:**. La tabla se filtra a medida que escribe.

## Solución de problemas

- **El botón Edit no hace nada al hacer clic** — No hay ninguna fila seleccionada. Haga clic en una fila de la tabla para seleccionarla y luego haga clic en **Edit**.
- **Los cambios no parecen guardarse** — Confirme cada cambio en una celda presionando Enter antes de pasar a una fila diferente. Si hace clic en otro lugar sin confirmar, es posible que se descarte la edición en curso.

## Relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
- [Sintonizar el radio en una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
