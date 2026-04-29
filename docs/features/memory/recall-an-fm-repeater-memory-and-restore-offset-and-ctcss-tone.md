# Recuperar una memoria de repetidor FM y restaurar el desplazamiento y el tono CTCSS

Abra una memoria de repetidor FM guardada y sintonice el slice (canal de recepción) activo en ella, restaurando la frecuencia de recepción almacenada, la dirección del desplazamiento de transmisión, el desplazamiento del repetidor y el valor del tono CTCSS en una sola operación.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El módulo Memory Channels requiere una conexión de radio activa.
- La memoria del repetidor debe existir en la tabla de memorias con sus columnas FM TX Offset Dir, Repeater Offset, Tone Mode y Tone Value completadas. Si no es así, consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md) y [Editar el nombre, modo o desplazamiento de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md).
- Al menos un slice debe estar activo en el radio.

## Pasos

1. Abra `Settings > Memory...`.
2. Localice la memoria del repetidor. Si la lista es larga, escriba parte del nombre de la memoria en el campo **Search:** y presione Enter para filtrar la tabla.
3. Haga clic en la fila de la memoria del repetidor para seleccionarla.
4. Haga clic en **Tune**.

El slice activo se sintoniza en la frecuencia almacenada. El radio restaura el modo, FM TX Offset Dir, Repeater Offset, Tone Mode y Tone Value desde la fila de memoria.

Alternativamente, haga doble clic en la fila para sintonizar sin usar el botón **Tune**.

## Qué hace cada control

| Control | Propósito | Notas |
|---|---|---|
| **Search:** | Filtra la tabla por nombre de memoria. | Tiene un botón para limpiar; presione Enter para ir a la primera coincidencia. |
| **Profile:** | Reduce la tabla a las memorias que pertenecen al perfil global seleccionado. | Útil cuando las memorias de repetidores están agrupadas bajo un perfil regional. |
| **Memory table — FM TX Offset Dir** | Almacena la dirección del desplazamiento de transmisión (por ejemplo, minus, plus, simplex). | Columna 7 de la tabla. Se restaura al sintonizar. |
| **Memory table — Repeater Offset** | Almacena la frecuencia de desplazamiento en MHz. | Columna 8 de la tabla. Se restaura al sintonizar. |
| **Memory table — Tone Mode** | Almacena el modo CTCSS/DCS (por ejemplo, codificación de tono CTCSS). | Columna 9 de la tabla. Se restaura al sintonizar. |
| **Memory table — Tone Value** | Almacena la frecuencia del tono CTCSS o el código DCS. | Columna 10 de la tabla. Se restaura al sintonizar. |
| **Tune** | Sintoniza el slice activo en la memoria seleccionada, restaurando todos los campos almacenados. | Debe haber una fila seleccionada. Hacer doble clic en una fila tiene el mismo efecto. |

## Consejos

- Si sus memorias de repetidores están mezcladas con otras entradas, use **Profile:** para filtrar por un grupo dedicado a repetidores y así localizar la fila deseada más fácilmente.
- Puede ordenar la tabla por cualquier columna ordenable —por ejemplo, Frequency— haciendo clic en el encabezado de la columna. Esto puede ayudarle a encontrar un repetidor por su frecuencia de salida. Consulte [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md).

## Solución de problemas

- **Tune aparece en gris** — No hay ninguna fila seleccionada. Haga clic en una fila de la tabla de memorias primero y luego haga clic en **Tune**.
- **El desplazamiento del repetidor o el tono no se aplican después de sintonizar** — Las columnas FM TX Offset Dir, Repeater Offset, Tone Mode o Tone Value pueden estar vacías para esa memoria. Seleccione la fila, haga clic en **Edit**, complete las columnas faltantes y sintonice nuevamente. Consulte [Editar el nombre, modo o desplazamiento de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md).
- **La memoria esperada no aparece en la tabla** — Verifique el filtro **Profile:**. Si está seleccionado un perfil distinto al que contiene la memoria del repetidor, la fila quedará oculta. Establezca **Profile:** en el perfil correcto o limpie el filtro.

## Relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Editar el nombre, modo o desplazamiento de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
- [Sintonizar el radio en una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
