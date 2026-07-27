# Resumen de KiwiSDR

El applet KiwiSDR le permite explorar y conectarse a receptores KiwiSDR públicos en todo el mundo, y luego escucharlos a través de un slice de AetherSDR. Esto es útil para monitoreo remoto, verificación de propagación o escuchar bandas que su radio local no puede alcanzar.

## Cómo funciona

El applet muestra un directorio con capacidad de búsqueda de receptores KiwiSDR en línea. Usted selecciona un receptor de la lista, hace clic en Assign to slice, y AetherSDR se conecta a ese receptor y encamina su audio a través del slice activo. Un indicador de estado en vivo muestra el estado de la conexión y los metadatos del receptor conectado.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---------|------|----------------------|----------------|------------------------|
| Receiver list | Lista | Vacía | Lista con capacidad de búsqueda y desplazamiento de receptores KiwiSDR públicos con nombre, ubicación, banda y estado. | None (no se persiste) |
| Assign to slice | Botón pulsador | — | Asigna el receptor KiwiSDR seleccionado al slice activo para sintonización y escucha. | None (no se persiste) |
| Status indicator | Indicador | Disconnected | Muestra el estado de la conexión: Disconnected, Connecting, Connected o Error. | None (no se persiste) |

## Consejos

- El applet KiwiSDR no requiere una conexión a su radio FLEX-8600. Puede usarlo de forma independiente para escucha remota.
- El indicador de estado de conexión se actualiza en tiempo real; si ve "Error", verifique que el receptor KiwiSDR esté en línea y sea accesible desde su red.

## Relacionado

- [Examinar el directorio público de KiwiSDR](browse-the-public-kiwisdr-directory.md)
- [Conectarse a un receptor KiwiSDR](../../getting-started/setup/connect-to-a-kiwisdr-receiver.md)
- [Asignar un KiwiSDR a un slice para escuchar](assign-a-kiwisdr-to-a-slice-for-listening.md)
