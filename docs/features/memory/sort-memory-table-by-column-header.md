# Ordenar la tabla de memorias por encabezado de columna

Haga clic en un encabezado de columna en el diálogo Memory Channels para ordenar todas las filas de memoria visibles según esa columna. Use el ordenamiento para localizar rápidamente entradas por frecuencia, nombre, grupo u otros campos.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Memory Channels requiere una conexión de radio activa.
- Abra el diálogo mediante `Settings > Memory...`.

## Pasos

1. Abra `Settings > Memory...` para mostrar el diálogo Memory Channels.
2. Haga clic en cualquier encabezado de columna ordenable en la tabla de memorias — por ejemplo, **Frequency** o **Name**.
3. La tabla se ordena de forma ascendente en el primer clic. Aparece una flecha indicadora de ordenamiento en el encabezado.
4. Haga clic en el mismo encabezado de columna nuevamente para invertir el orden a descendente.
5. Haga clic en un encabezado de columna diferente para ordenar por esa columna, restableciendo el orden ascendente.

## Qué hace cada control

| Encabezado de columna | Ordena por |
|---|---|
| Group | Nombre del grupo de memorias |
| Owner | Campo de propietario |
| Frequency | Frecuencia almacenada (numérica) |
| Name | Nombre de la memoria |
| Mode | Modo de operación (p. ej., USB, CW) |
| Step | Valor del paso de sintonía |
| FM TX Offset Dir | Dirección de desplazamiento del repetidor FM |
| Repeater Offset | Frecuencia de desplazamiento del repetidor |
| Tone Mode | Modo de tono CTCSS/DCS |
| Tone Value | Frecuencia o código del tono |
| Squelch | Estado de habilitación del squelch |
| Squelch Level | Nivel de umbral del squelch |
| RX Filter Low | Borde inferior del filtro de recepción |
| RX Filter High | Borde superior del filtro de recepción |
| RTTY Mark | Frecuencia mark de RTTY |
| RTTY Shift | Valor de desplazamiento de RTTY |
| DIGL Offset | Desplazamiento de banda lateral inferior digital |
| DIGU Offset | Desplazamiento de banda lateral superior digital |

La flecha indicadora de ordenamiento en el encabezado de columna muestra la columna activa y la dirección de ordenamiento. Los valores de frecuencia se ordenan de forma numérica y no alfabética.

## Consejos

- El ordenamiento se aplica sobre cualquier búsqueda activa o filtro de perfil. Primero reduzca la lista con **Search:** o **Profile:**, luego ordene para organizar los resultados filtrados.
- El ordenamiento no cambia el orden almacenado de las memorias en el radio. Es una operación solo de visualización.

## Relacionados

- [Descripción general de Memory Channels](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Sintonizar el radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
