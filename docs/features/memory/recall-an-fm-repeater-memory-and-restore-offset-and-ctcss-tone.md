# Recordar una Memoria de Repetidor FM y Restaurar Desplazamiento y Tono CTCSS

Abra una memoria guardada de repetidor FM y sintonice el slice activo a ella, restaurando la frecuencia de recepción almacenada, la dirección del desplazamiento de transmisión, el desplazamiento del repetidor y el valor del tono CTCSS en una sola operación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Memory Channels requiere una conexión de radio activa.
- La memoria del repetidor ya debe existir en la tabla de memorias con sus columnas FM TX Offset Dir, Repeater Offset, Tone Mode y Tone Value completadas. Si no es así, consulte [Add a memory at current frequency](add-a-memory-at-current-frequency.md) y [Edit a memory's name, mode or offset inline](edit-a-memory-s-name-mode-or-offset-inline.md).
- Al menos un slice debe estar activo en la radio.

## Pasos

1. Abra `Settings > Memory...`.
2. Localice la memoria del repetidor. Si la lista es larga, escriba parte del nombre de la memoria en el campo **Search:** y presione Enter para filtrar la tabla.
3. Haga clic en la fila de la memoria del repetidor para seleccionarla.
4. Haga clic en **Tune**.

El slice activo se sintoniza a la frecuencia almacenada. La radio restaura el modo, FM TX Offset Dir, Repeater Offset, Tone Mode y Tone Value desde la fila de la memoria.

Alternativamente, haga doble clic en la fila para sintonizar sin usar el botón **Tune**.

## Propósito de cada control

| Control | Propósito | Notas |
|---|---|---|
| **Search:** | Filtra la tabla por nombre de memoria. | Tiene un botón de borrar; presione Enter para saltar a la primera coincidencia. |
| **Profile:** | Reduce la tabla a las memorias que pertenecen al perfil global seleccionado. | Útil cuando las memorias de repetidor están agrupadas bajo un perfil regional. |
| **Tabla de memorias — FM TX Offset Dir** | Almacena la dirección del desplazamiento de transmisión (p. ej., menos, más, simplex). | Columna 7 en la tabla. Se restaura al sintonizar. |
| **Tabla de memorias — Repeater Offset** | Almacena la frecuencia de desplazamiento en MHz. | Columna 8 en la tabla. Se restaura al sintonizar. |
| **Tabla de memorias — Tone Mode** | Almacena el modo CTCSS/DCS (p. ej., codificación de tono CTCSS). | Columna 9 en la tabla. Se restaura al sintonizar. |
| **Tabla de memorias — Tone Value** | Almacena la frecuencia del tono CTCSS o el código DCS. | Columna 10 en la tabla. Se restaura al sintonizar. |
| **Tune** | Sintoniza el slice activo a la memoria seleccionada, restaurando todos los campos almacenados. | Debe seleccionarse una fila. Hacer doble clic en una fila tiene el mismo efecto. |

## Consejos

- Si sus memorias de repetidor están mezcladas con otras entradas, use **Profile:** para filtrar por un grupo dedicado a repetidores, así la fila objetivo será más fácil de encontrar.
- Puede ordenar la tabla por cualquier columna ordenable — por ejemplo, Frequency — haciendo clic en el encabezado de la columna. Esto puede ayudarle a encontrar un repetidor por su frecuencia de salida. Consulte [Sort memory table by column header](sort-memory-table-by-column-header.md).

## Solución de problemas

- **Tune está atenuado** — No hay ninguna fila seleccionada. Haga clic en una fila de la tabla de memorias primero, luego haga clic en **Tune**.
- **El desplazamiento o tono del repetidor no se aplica después de sintonizar** — Las columnas FM TX Offset Dir, Repeater Offset, Tone Mode o Tone Value pueden estar vacías para esa memoria. Seleccione la fila, haga clic en **Edit**, complete las columnas faltantes y sintonice de nuevo. Consulte [Edit a memory's name, mode or offset inline](edit-a-memory-s-name-mode-or-offset-inline.md).
- **La memoria esperada no aparece en la tabla** — Verifique el filtro **Profile:**. Si está seleccionado un perfil diferente al que contiene la memoria del repetidor, la fila estará oculta. Establezca **Profile:** en el perfil correcto o borre el filtro.

## Relacionados

- [Add a memory at current frequency](add-a-memory-at-current-frequency.md)
- [Edit a memory's name, mode or offset inline](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Tune the radio to a stored memory](tune-the-radio-to-a-stored-memory.md)
- [Search memories by name](search-memories-by-name.md)
- [Filter memories by profile](filter-memories-by-profile.md)
- [Sort memory table by column header](sort-memory-table-by-column-header.md)
