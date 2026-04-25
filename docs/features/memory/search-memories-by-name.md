# Buscar memorias por nombre

Use el campo de búsqueda en el cuadro de diálogo Memory Channels para filtrar la tabla de memorias según las entradas cuyo nombre coincida con lo que escriba. Esto es útil cuando tiene un gran número de frecuencias almacenadas y desea encontrar una específica rápidamente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El cuadro de diálogo Memory Channels requiere una conexión activa al radio.
- Abra el cuadro de diálogo Memory Channels mediante `Settings > Memory...`.

## Pasos

1. Abra `Settings > Memory...`.
2. Haga clic en el campo **Search:** en la parte superior del cuadro de diálogo.
3. Escriba parte o todo el nombre de la memoria que está buscando. La tabla se filtra a medida que escribe.
4. Para confirmar y activar el primer resultado, presione Enter. Para borrar la búsqueda y mostrar todas las memorias nuevamente, haga clic en el botón de borrar dentro del campo **Search:**.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Search:** | Filtra la tabla de memorias para mostrar las filas cuyo nombre coincide con el texto ingresado. | Tiene un botón de borrar. Presione Enter para activar la fila actual. |
| Tabla de memorias | Muestra el conjunto filtrado de memorias. Las columnas incluyen Group, Owner, Frequency, Name, Mode y otras. | Haga clic en una fila para seleccionarla. Haga doble clic en una fila para sintonizar el slice activo en esa memoria. |

## Consejos

- El filtro se aplica a medida que escribe — no es necesario presionar Enter para ver cómo se reducen los resultados.
- Para mover el foco al campo **Search:** desde cualquier parte del cuadro de diálogo, use el atajo de teclado de búsqueda (`Ctrl+F` en Linux y Windows, `Cmd+F` en macOS). El texto existente se selecciona automáticamente para que pueda comenzar a escribir de inmediato.
- Después de filtrar, use Shift-click para seleccionar un rango de resultados, o `Ctrl+click` (`Cmd+click` en macOS) para agregar o quitar filas individuales.

## Relacionado

- [Descripción general de Memory Channels](overview.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Sintonizar el radio en una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
