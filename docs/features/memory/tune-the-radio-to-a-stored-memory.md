# Sintonizar el radio a una memoria almacenada

Abra el diálogo Memory Channels para encontrar una frecuencia almacenada y enviarla directamente al slice receptor activo.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Memory Channels requiere una conexión de radio activa.
- Al menos una memoria debe estar almacenada previamente. Consulte [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md) si no tiene ninguna.

## Pasos

1. Haga clic en `Settings > Memory...` para abrir el diálogo Memory Channels.
2. Opcional: escriba un nombre en el campo **Search:** para reducir la lista, o seleccione un grupo en el cuadro combinado **Profile:** para filtrar por perfil.
3. Haga clic en la fila de la tabla de memorias que contiene la frecuencia a la que desea sintonizar. La fila se resalta y el contador de selección en la parte inferior derecha se actualiza para mostrar `1 selected`.
4. Haga clic en **Tune**.

El slice activo se sintoniza inmediatamente a la frecuencia, el modo y la configuración de filtro almacenados en esa memoria.

## Consejos

- Al hacer doble clic en cualquier fila de la tabla de memorias, el slice activo se sintoniza a esa memoria sin necesidad de hacer clic en **Tune**.
- Si necesita sintonizar una memoria que se encuentra dentro de una lista larga, use el campo **Search:** para filtrar por nombre primero. La tabla se actualiza mientras escribe. Presione Enter después de escribir para sintonizar directamente la fila resaltada en ese momento.
- En Linux y Windows, Ctrl+clic selecciona o deselecciona filas individuales sin borrar el resto de la selección. Solo la primera fila seleccionada se utiliza al hacer clic en **Tune** o al hacer doble clic.

## Solución de problemas

- **Tune no hace nada** — Confirme que el radio está conectado. El diálogo requiere una conexión de radio activa. Verifique que haya exactamente una fila seleccionada en la tabla.
- **La memoria que busca no es visible** — Es posible que haya un filtro activo. Borre el campo **Search:** usando su botón de limpieza y restablezca **Profile:** a su valor predeterminado (sin filtro) para mostrar todas las memorias.

## Relacionados

- [Descripción general de Memory Channels](overview.md)
- [Agregar una memoria en la frecuencia actual](add-a-memory-at-current-frequency.md)
- [Buscar memorias por nombre](search-memories-by-name.md)
- [Filtrar memorias por perfil](filter-memories-by-profile.md)
- [Editar el nombre, modo u offset de una memoria en línea](edit-a-memory-s-name-mode-or-offset-inline.md)
