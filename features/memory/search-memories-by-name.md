# Búsqueda de memorias por nombre

Use el campo Search en el diálogo Memory Channels para filtrar la tabla de memorias y mostrar solo las entradas cuyo nombre coincida con lo que escribe. Esto es útil cuando tiene un gran número de frecuencias almacenadas y necesita encontrar una rápidamente.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El diálogo Memory Channels requiere una conexión de radio activa.
- Abra el diálogo Memory Channels mediante `Settings > Memory...`.

## Pasos

1. Abra `Settings > Memory...`.
2. Haga clic en el campo **Search:** en la parte superior del diálogo.
3. Escriba parte o la totalidad del nombre de la memoria que busca. La tabla se filtra mientras escribe.
4. Para borrar la búsqueda y mostrar todas las memorias, haga clic en el botón de limpieza dentro del campo **Search:**, o elimine el texto manualmente.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Search:** | Filtra la tabla de memorias para mostrar las filas cuyo nombre coincide con el texto que escribe. | Tiene un botón de limpieza. Presione Enter para activar la fila resaltada en ese momento. |
| Tabla de memorias | Muestra los resultados filtrados. Las columnas incluyen Group, Owner, Frequency, Name, Mode y otras. | Haga clic en una fila para seleccionarla. Haga doble clic en una fila para sintonizar el radio en esa memoria. |

## Consejos

- La tabla se filtra con cada pulsación de tecla — no es necesario presionar Enter para ver los resultados. Presione Enter para sintonizar el radio en la fila resaltada actualmente.
- Para buscar y luego actuar sobre varios resultados, use Shift-clic para seleccionar un rango o Ctrl-clic (Command-clic en macOS) para agregar filas individuales a la selección.
- Combine **Search:** con el filtro **Profile:** para reducir los resultados por nombre y grupo de perfil al mismo tiempo.

## Temas relacionados

- [Descripción general de Memory Channels](overview.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Sintonizar el radio en una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
