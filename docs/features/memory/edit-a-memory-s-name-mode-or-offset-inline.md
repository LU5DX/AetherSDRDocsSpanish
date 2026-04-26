# Editar el nombre, modo u offset de una memoria de forma inline

El diálogo Memory Channels permite cambiar cualquier campo de una memoria almacenada — incluyendo su nombre, modo, offset de repetidor y más — sin salir de la tabla. Use esta función cuando necesite corregir o actualizar una memoria después de haberla agregado.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Memory Channels requiere una conexión activa con el radio.
- La memoria que desea editar ya debe existir en la tabla. Para crear una nueva memoria, consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md).

## Pasos

1. Abra `Settings > Memory...`.
2. En la tabla de memorias, haga clic en la fila que desea editar para seleccionarla.
3. Haga clic en `Edit`. La fila entra en modo de edición inline y sus celdas se vuelven editables.
4. Haga clic en la celda que desea modificar — por ejemplo, la columna **Name**, **Mode** o **Repeater Offset** — y escriba el nuevo valor.
5. Presione Enter o haga clic en otra celda para confirmar cada cambio.
6. Para finalizar la edición, haga clic en cualquier otra fila o presione Escape.

## Qué hace cada control

| Control | Descripción |
|---|---|
| Tabla de memorias | Muestra todas las filas de memorias. Columnas: Group, Owner, Frequency, Name, Mode, Step, FM TX Offset Dir, Repeater Offset, Tone Mode, Tone Value, Squelch, Squelch Level, RX Filter Low, RX Filter High, RTTY Mark, RTTY Shift, DIGL Offset, DIGU Offset. La edición inline se habilita después de hacer clic en `Edit`. |
| `Edit` | Activa el modo de edición inline para la fila seleccionada. |
| `Search:` | Filtra la tabla por nombre de memoria. Úselo para localizar una memoria antes de editarla. Cuenta con un botón para limpiar el campo; presione Enter para aplicar. |
| `Profile:` | Filtra la tabla por el perfil global activo. |

## Consejos

- También puede activar el modo de edición inline mediante el teclado después de seleccionar una fila, de acuerdo con el modo de edición por teclado de la tabla.
- Hacer doble clic en una fila sintoniza el radio en esa memoria en lugar de abrirla para edición. Para editar, use el botón `Edit`.
- Use `Search:` para reducir la tabla antes de seleccionar una fila a editar, especialmente si tiene muchas memorias almacenadas.

## Solución de problemas

- **`Edit` no tiene efecto** — Asegúrese de que exactamente una fila esté seleccionada antes de hacer clic en `Edit`. Si no hay ninguna fila seleccionada, el botón no activará el modo de edición.
- **Los cambios no parecen guardarse** — El diálogo requiere una conexión activa con el radio. Si la conexión se interrumpió, reconéctese e ingrese el valor nuevamente.

## Relacionado

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
