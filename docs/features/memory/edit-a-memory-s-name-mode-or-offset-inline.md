# Editar el nombre, modo u offset de una memoria en línea

Use esta página para cambiar el nombre, el modo, el offset del repetidor u otro campo editable de una memoria almacenada sin salir del diálogo Memory Channels.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Memory Channels requiere una conexión activa con la radio.
- La memoria que desea editar debe existir previamente. Para crear una nueva memoria, consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md).

## Pasos

1. Abra `Settings > Memory...`.
2. Localice la memoria que desea editar. Use el campo **Search:** o el cuadro combinado **Profile:** para reducir la lista si es necesario.
3. Haga clic en la fila para seleccionarla.
4. Haga clic en **Edit**. La fila seleccionada entra en modo de edición en línea.
5. Haga clic en la celda que desea modificar — por ejemplo, la columna **Name**, **Mode** o **Repeater Offset** — y escriba el nuevo valor.
6. Presione Enter o haga clic en otra celda para confirmar cada cambio.
7. Repita el proceso para las demás columnas de la misma fila.
8. Haga clic fuera de la fila o seleccione una fila diferente para finalizar la edición.

## Qué hace cada control

| Columna | Qué almacena |
|---|---|
| Group | Etiqueta de grupo o perfil de la memoria. |
| Owner | Etiqueta de propietario de la memoria. |
| Frequency | Frecuencia almacenada en MHz. |
| Name | Etiqueta legible por el usuario. |
| Mode | Modo de operación (p. ej., USB, LSB, CW, FM). |
| Step | Tamaño del paso de sintonía. |
| FM TX Offset Dir | Dirección del offset del repetidor. |
| Repeater Offset | Valor del offset del repetidor. |
| Tone Mode | Modo de tono CTCSS/DCS. |
| Tone Value | Frecuencia o código del tono. |
| Squelch | Squelch activado/desactivado (casilla de verificación). |
| Squelch Level | Nivel umbral del squelch. |
| RX Filter Low | Borde inferior del filtro de recepción. |
| RX Filter High | Borde superior del filtro de recepción. |
| RTTY Mark | Offset de frecuencia de marca RTTY. |
| RTTY Shift | Valor de desplazamiento RTTY. |
| DIGL Offset | Offset del modo DIGL. |
| DIGU Offset | Offset del modo DIGU. |

El botón **Edit** activa el modo de edición en línea sobre la memoria seleccionada. Todas las columnas listadas anteriormente son editables en línea.

## Consejos

- También puede hacer doble clic en una fila para sintonizar la radio en esa memoria, en lugar de editarla. Para editar, use el botón **Edit** en vez de hacer doble clic.
- Para encontrar una memoria específica rápidamente antes de editarla, escriba parte de su nombre en el campo **Search:**. La tabla se filtra mientras escribe.

## Solución de problemas

- **El botón Edit no hace nada** — No hay ninguna fila seleccionada. Haga clic en una fila de la tabla de memorias primero y luego haga clic en **Edit**.
- **Los cambios no parecen guardarse** — Confirme cada edición de celda presionando Enter o moviendo el foco a otra celda antes de hacer clic fuera de la fila.

## Relacionados

- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Sintonizar la radio en una memoria almacenada](tune-the-radio-to-a-stored-memory.md)
- [Eliminar una o más memorias](delete-one-or-more-memories.md)
