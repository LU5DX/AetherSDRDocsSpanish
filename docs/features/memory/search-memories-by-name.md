# Buscar memorias por nombre

Use el campo Search del diálogo Memory Channels para filtrar la tabla de memorias y mostrar solo las entradas cuyo nombre coincida con lo que escriba. Esto resulta útil cuando tiene una gran cantidad de frecuencias almacenadas y desea localizar una en particular rápidamente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Memory Channels requiere una conexión de radio activa.
- Abra el diálogo Memory Channels mediante `Settings > Memory...`.

## Pasos

1. Abra `Settings > Memory...`.
2. Haga clic en el campo **Search:** ubicado en la parte superior del diálogo.
3. Escriba parte o todo el nombre de la memoria que desea encontrar. La tabla se filtra a medida que escribe.
4. Para borrar la búsqueda y mostrar todas las memorias, haga clic en el botón de borrado dentro del campo **Search:**.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Search:** | Filtra la tabla de memorias para mostrar las filas cuyo nombre coincida con el texto ingresado. | Tiene un botón de borrado. Presione Enter para activar la fila resaltada actualmente. |

## Consejos

- No es necesario presionar Enter para filtrar: la tabla se actualiza con cada carácter que escriba.
- Presionar Enter después de escribir confirma y activa (sintoniza) la fila seleccionada actualmente en los resultados filtrados.
- El campo **Search:** puede enfocarse rápidamente mediante el atajo de teclado de búsqueda (`Ctrl+F` en Linux y Windows, `Cmd+F` en macOS) sin necesidad de usar el mouse.
- Use el cuadro combinado **Profile:** junto al campo de búsqueda para restringir los resultados a un perfil específico antes de buscar.

## Relacionados

- [Descripción general de Memory Channels](overview.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Sintonizar el radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
