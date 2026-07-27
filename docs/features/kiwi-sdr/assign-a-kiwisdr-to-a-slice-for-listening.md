# Asignar un KiwiSDR a un slice para escuchar

Después de navegar por el directorio público de KiwiSDR y conectarse a un receptor, asígnelo a un slice activo para poder sintonizar y escuchar a través del KiwiSDR remoto seleccionado.

## Antes de comenzar

- Debe tener un receptor KiwiSDR conectado (el indicador de estado muestra "Connected").
- Debe haber un slice activo en el panadapter.

## Pasos

1. Abra el **Applet panel** y haga clic en el mosaico **KiwiSDR** para abrir el applet de KiwiSDR.
2. En la **Receiver list**, seleccione el receptor KiwiSDR que desea utilizar.
3. Haga clic en **Assign to slice**.

El slice ahora sintoniza el receptor KiwiSDR seleccionado. El **Status indicator** muestra los detalles de la conexión.

## Función de cada control

| Control | Comportamiento |
|---------|----------------|
| Receiver list | Lista buscable y desplazable de receptores KiwiSDR públicos con nombre, ubicación, banda y estado. |
| Assign to slice | Asigna el receptor KiwiSDR seleccionado al slice activo para sintonización y escucha. |
| Status indicator | Muestra el estado de la conexión (`Disconnected` / `Connecting` / `Connected` / `Error`) con texto detallado. |

## Relacionado

- [Resumen de KiwiSDR](overview.md)
- [Navegar por el directorio público de KiwiSDR](browse-the-public-kiwisdr-directory.md)
- [Conectarse a un receptor KiwiSDR](../../getting-started/setup/connect-to-a-kiwisdr-receiver.md)
