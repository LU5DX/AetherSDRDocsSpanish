# Conectarse a un receptor KiwiSDR

Explore el directorio público de KiwiSDR y conéctese a un receptor remoto para escuchar a través de AetherSDR. Esto le permite sintonizar y escuchar receptores KiwiSDR en todo el mundo sin necesidad de una conexión física de radio.

## Antes de comenzar

- AetherSDR debe estar en ejecución (no se requiere una conexión de radio — el applet KiwiSDR funciona de forma independiente)
- El applet KiwiSDR depende del acceso a internet para descubrir receptores públicos

## Pasos

1. Abra el Panel de Applets y haga clic en el mosaico **KiwiSDR**.
2. El applet KiwiSDR muestra una lista de receptores públicos que se puede buscar. Desplácese o use el campo de búsqueda para encontrar un receptor.
3. Haga clic en un receptor de la lista para seleccionarlo.
4. Haga clic en **Assign to slice**. El KiwiSDR seleccionado se asigna al slice activo y el indicador de estado muestra el estado de la conexión.

## Función de cada control

| Control | Descripción |
|---------|-------------|
| Receiver list | Lista de receptores KiwiSDR públicos con capacidad de búsqueda y desplazamiento que muestra nombre, ubicación, banda y estado |
| Assign to slice | Asigna el receptor KiwiSDR seleccionado al slice activo para sintonización y escucha |
| Status indicator | Muestra el estado de la conexión: Disconnected (predeterminado), Connecting, Connected o Error |

## Relacionados

- [Browse the public KiwiSDR directory](../../features/kiwi-sdr/browse-the-public-kiwisdr-directory.md)
- [KiwiSDR overview](../../features/kiwi-sdr/overview.md)
- [Assign a KiwiSDR to a slice for listening](../../features/kiwi-sdr/assign-a-kiwisdr-to-a-slice-for-listening.md)
