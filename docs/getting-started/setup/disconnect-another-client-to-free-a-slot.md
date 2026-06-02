# Desconectar otro cliente para liberar un espacio

Cuando multiFLEX está desactivado en su FLEX-8600, solo un cliente puede estar conectado a la vez. Si ya hay otro cliente conectado, esta página le muestra cómo desconectarlo para que AetherSDR pueda conectarse.

## Antes de comenzar

- AetherSDR debe estar intentando conectarse a una radio donde multiFLEX está desactivado y otro cliente ya está conectado. El cuadro de diálogo Connected Stations aparece automáticamente en esta situación.
- No es necesario usar el menú para abrir el cuadro de diálogo; se abre solo cuando la radio rechaza la conexión.

## Pasos

1. Si el cuadro de diálogo Connected Stations no aparece automáticamente, ábralo manualmente: **Help > Connected Stations...**
2. En la sección **Connected Stations**, haga clic en el botón de opción junto al cliente que desea desconectar. Cada entrada muestra el nombre del programa cliente y, opcionalmente, el nombre de la estación. Los clientes desconocidos se etiquetan como "client 0x&lt;HEX&gt;".
3. Haga clic en **Disconnect Station** (el botón rojo). El botón solo se habilita después de seleccionar una estación.
4. AetherSDR ahora intentará conectarse al espacio liberado.

## Descripción de cada control

| Control | Descripción |
|---|---|
| **Sección Radio** | Sección de solo lectura en la parte superior que muestra el modelo, el apodo y el indicativo de la radio conectada. El encabezado de la sección dice "Radio". |
| **Botones de opción de estación** | Uno por cada cliente conectado. Al seleccionar uno se habilita **Disconnect Station**. Cada entrada muestra el nombre del programa cliente y, opcionalmente, el nombre de la estación. La etiqueta por defecto es "client 0x&lt;HEX&gt;" si no se conoce el programa ni la estación. |
| **Disconnect Station** | Desconecta el cliente seleccionado de la radio. La etiqueta es "Disconnect Station" y aparece en rojo. Solo se habilita cuando un botón de opción de estación está marcado. |
| **Cancel** | Cierra el cuadro de diálogo sin desconectar. |
| **Etiqueta informativa** | Explica que multiFLEX está desactivado en esta radio y que debe seleccionar una estación para desconectar antes de conectar AetherSDR. Texto completo: "multiFLEX is disabled on this radio. Select a station to disconnect before connecting AetherSDR." |

## Solución de problemas

- **El botón Disconnect Station aparece atenuado** — Seleccione una estación haciendo clic en su botón de opción. El botón permanece deshabilitado hasta que se realiza una selección.
- **El cuadro de diálogo no aparece, pero sabe que hay otro cliente conectado** — Ábralo manualmente mediante **Help > Connected Stations...**
- **El cuadro de diálogo aparece con un tema oscuro al iniciarse por primera vez** — Esto es un comportamiento esperado. El cuadro de diálogo ahora aplica el estilo del tema inmediatamente al abrirse, garantizando una apariencia visual consistente en todos los sistemas operativos compatibles.

## Relacionado

- [Ver todas las estaciones conectadas cuando multiFLEX está desactivado](see-all-stations-connected-when-multiflex-is-off.md)
- [Identificar cada cliente por programa y nombre de estación](../../features/connected-stations/identify-each-client-by-program-and-station-name.md)
