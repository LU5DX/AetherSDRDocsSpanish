# Buscar memorias por nombre

Use el campo de búsqueda en el diálogo Memory Channels para filtrar la tabla de memorias y mostrar solo las entradas cuyos nombres coincidan con lo que escribe. Esto resulta útil cuando tiene una gran cantidad de canales almacenados y desea encontrar uno rápidamente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Memory Channels requiere una conexión de radio activa.
- Abra el diálogo mediante `Settings > Memory...`.

## Pasos

1. Abra `Settings > Memory...`.
2. Haga clic en el campo **Search:** en la parte superior del diálogo.
3. Escriba una parte o el nombre completo de la memoria que está buscando. La tabla se filtra mientras escribe.
4. Para confirmar la selección y sintonizar el primer resultado coincidente, presione **Enter**.
5. Para borrar la búsqueda y mostrar todas las memorias nuevamente, haga clic en el botón de borrar dentro del campo **Search:**.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Search:** | Filtra la tabla de memorias para mostrar las filas cuyo nombre coincide con el texto escrito. | Tiene un botón de borrar. Al presionar Enter se activa la fila actualmente resaltada. |
| Tabla de memorias | Muestra el conjunto filtrado de memorias. | Las columnas incluyen Group, Owner, Frequency, Name, Mode y otras. |

## Consejos

- La tabla se actualiza con cada pulsación de tecla; no es necesario presionar Enter para ver los resultados filtrados.
- Al presionar Enter después de escribir, se sintoniza el slice activo en la fila de memoria actualmente resaltada, lo que equivale a hacer clic en **Tune**.
- Para reducir aún más los resultados después de buscar por nombre, use el cuadro combinado **Profile:** para filtrar adicionalmente por perfil.

## Relacionados

- [Descripción general de Memory Channels](overview.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Sintonizar la radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Ordenar la tabla de memorias por encabezado de columna](sort-memory-table-by-column-header.md)
