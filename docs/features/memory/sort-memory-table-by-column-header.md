# Ordenar la tabla de memorias por encabezado de columna

Haga clic en un encabezado de columna en el diálogo Memory Channels para ordenar todas las filas de memoria visibles según esa columna. Use esta función para encontrar rápidamente entradas por frecuencia, nombre, grupo u otros campos.

## Antes de comenzar

- Se requiere una conexión de radio para abrir el diálogo Memory Channels.
- Abra el diálogo mediante `Settings > Memory...`.

## Pasos

1. Vaya a `Settings > Memory...`.
2. En la tabla de memorias, haga clic en el encabezado de la columna por la que desea ordenar (por ejemplo, "Frequency" o "Name").
3. La tabla se ordena de forma ascendente en el primer clic. Aparece una flecha indicadora de orden en el encabezado.
4. Haga clic en el mismo encabezado nuevamente para invertir el orden a descendente.
5. Haga clic en un encabezado de columna diferente para ordenar por esa columna; el orden vuelve a ascendente.

## Qué hace cada control

| Encabezado de columna | Ordena por |
|---|---|
| Group | Nombre del grupo de memoria |
| Owner | Nombre del propietario |
| Frequency | Frecuencia almacenada (numérica) |
| Name | Nombre de la memoria |
| Mode | Modo de operación (p. ej., USB, CW) |
| Step | Paso de sintonía |
| FM TX Offset Dir | Dirección del desplazamiento del repetidor |
| Repeater Offset | Valor del desplazamiento del repetidor |
| Tone Mode | Modo de tono CTCSS/DCS |
| Tone Value | Frecuencia o código de tono |
| Squelch | Estado de habilitación del squelch |
| Squelch Level | Nivel umbral del squelch |
| RX Filter Low | Límite inferior del filtro de recepción |
| RX Filter High | Límite superior del filtro de recepción |
| RTTY Mark | Frecuencia mark de RTTY |
| RTTY Shift | Valor de desplazamiento de RTTY |
| DIGL Offset | Desplazamiento de banda lateral inferior digital |
| DIGU Offset | Desplazamiento de banda lateral superior digital |

El ordenamiento se aplica a las filas actualmente visibles. Si hay activo un filtro por nombre o un filtro por perfil, solo se ordenan las filas filtradas.

## Consejos

- Las columnas numéricas, como Frequency, usan comparación numérica, por lo que 14.225 se ordena correctamente por encima de 7.200.
- El ordenamiento no cambia el orden almacenado de las memorias en el radio; solo afecta la visualización en este diálogo.
- Para volver a una vista sin ordenar, cierre y vuelva a abrir el diálogo mediante `Settings > Memory...`.

## Relacionado

- [Vista general de Memory Channels](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
