# Editar el nombre, modo u offset de una memoria en línea

Use esta página para cambiar el nombre, el modo, el offset del repetidor u otro campo de una memoria almacenada sin salir del diálogo Memory Channels.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Memory Channels requiere una conexión activa con el radio.
- Debe existir al menos una memoria en la tabla. Para crear una, consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md).

## Pasos

1. Abra `Settings > Memory...`.
2. En la tabla de memorias, haga clic en la fila que desea editar para seleccionarla.
3. Haga clic en **Edit**.  
   La fila seleccionada entra en modo de edición en línea. La celda resaltada se vuelve editable.
4. Escriba el nuevo valor en la celda.
5. Presione **Tab** para pasar a la siguiente celda, o haga clic en otra celda de la misma fila para editarla.
6. Cuando haya terminado de editar todos los campos que desea cambiar, presione **Enter** o haga clic fuera de la fila para confirmar los cambios.

## Qué hace cada control

| Control | Columna(s) afectada(s) | Notas |
|---|---|---|
| Tabla de memorias | Las 18 columnas | Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. El modo de edición en línea se activa mediante el botón **Edit** o el teclado. |
| **Edit** | — | Activa el modo de edición en línea en la fila actualmente seleccionada. |

## Consejos

- También puede activar el modo de edición en línea usando el teclado después de seleccionar una fila, sin necesidad de hacer clic en **Edit**.
- Hacer doble clic en una fila sintoniza el slice activo a esa memoria en lugar de abrirla para edición. Use el botón **Edit** cuando desee cambiar valores, no sintonizar.
- Use el campo **Search:** para filtrar la tabla por nombre de memoria antes de seleccionar una fila; esto es útil cuando la lista es larga. Consulte [Buscar memorias por nombre](search-memories-by-name.md).
- Para limitar la tabla a un grupo específico antes de editar, use el combo **Profile:**. Consulte [Filtrar memorias por perfil](filter-memories-by-profile.md).

## Solución de problemas

- **El botón Edit no tiene efecto** — No hay ninguna fila seleccionada. Haga clic en una fila de la tabla primero y luego haga clic en **Edit**.
- **Los cambios no se guardan después de escribir** — Presione **Enter** o haga clic fuera de la celda editada para confirmar. Cerrar el diálogo sin confirmar puede descartar las ediciones en curso.
- **La columna Frequency muestra valores inesperados después de editar** — El campo Frequency espera un valor en MHz. Verifique que el formato coincida con las entradas existentes en la tabla.

## Relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Sintonizar el radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Recuperar una memoria de repetidor FM y restaurar el offset y el tono CTCSS](recall-an-fm-repeater-memory-and-restore-offset-and-ctcss-tone.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
