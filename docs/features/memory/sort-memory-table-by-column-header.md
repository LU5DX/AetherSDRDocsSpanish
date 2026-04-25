# Ordenar la tabla de memorias por encabezado de columna

Haga clic en un encabezado de columna en el diálogo Memory Channels para ordenar la tabla de memorias por esa columna. Use esto para agrupar entradas relacionadas rápidamente — por ejemplo, ordenar por Frequency para explorar los canales almacenados en orden de banda, o por Group para agrupar memorias por categoría.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El diálogo Memory Channels requiere una conexión de radio activa.
- Abra el diálogo mediante `Settings > Memory...`.

## Pasos

1. Abra `Settings > Memory...`.
2. Haga clic en cualquier encabezado de columna ordenable en la tabla de memorias — por ejemplo, **Frequency**, **Name**, **Group** o **Mode**.
3. La tabla se ordena en forma ascendente. Aparece una flecha indicadora de orden en el encabezado.
4. Haga clic en el mismo encabezado nuevamente para invertir el orden a descendente.
5. Haga clic en un encabezado diferente para ordenar por esa columna, restableciendo el orden ascendente.

## Qué hace cada control

| Encabezado de columna | Ordena por |
|---|---|
| Group | Nombre del grupo de memoria |
| Owner | Campo de propietario |
| Frequency | Frecuencia almacenada (numérica) |
| Name | Nombre de la memoria |
| Mode | Modo de operación |
| Step | Paso de sintonía |
| FM TX Offset Dir | Dirección del desplazamiento del repetidor |
| Repeater Offset | Valor del desplazamiento del repetidor |
| Tone Mode | Configuración del modo de tono |
| Tone Value | Valor de frecuencia del tono |
| Squelch | Estado de activación del squelch |
| Squelch Level | Umbral del squelch |
| RX Filter Low | Borde inferior del filtro |
| RX Filter High | Borde superior del filtro |
| RTTY Mark | Frecuencia de marca RTTY |
| RTTY Shift | Valor de desplazamiento RTTY |
| DIGL Offset | Desplazamiento digital inferior |
| DIGU Offset | Desplazamiento digital superior |

Es posible que no todas las columnas admitan ordenamiento. Si al hacer clic en un encabezado no aparece ningún indicador de orden, esa columna no es ordenable.

## Consejos

- Los valores de Frequency se ordenan numéricamente, no como texto, por lo que 14.225 se ubica correctamente entre 14.200 y 14.300.
- El ordenamiento no reorganiza las memorias en el radio — solo cambia el orden de visualización en la tabla.
- El ordenamiento persiste mientras el diálogo está abierto. Cerrar y volver a abrir el diálogo restablece el orden.
- Use el campo **Search:** junto con el ordenamiento para acotar los resultados antes de ordenar. Consulte [Buscar memorias por nombre](search-memories-by-name.md).

## Relacionados

- [Descripción general de Memory Channels](overview.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Sintonizar el radio a una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
