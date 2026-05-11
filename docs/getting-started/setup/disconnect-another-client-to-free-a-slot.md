# Desconectar otro cliente para liberar un espacio

Cuando multiFLEX está deshabilitado en su FLEX-8600, solo un cliente puede estar conectado a la vez. Si otro cliente ya está conectado, esta página le muestra cómo desconectarlo para que AetherSDR pueda conectarse.

## Antes de comenzar

- AetherSDR debe estar intentando conectarse a una radio donde multiFLEX está deshabilitado y otro cliente ya está conectado. El cuadro de diálogo Connected Stations aparece automáticamente en esta situación.
- No necesita usar el menú para abrir el cuadro de diálogo; se abre por sí solo cuando la radio rechaza la conexión.

## Pasos

1. Si el cuadro de diálogo Connected Stations no aparece automáticamente, ábralo manualmente: **Help > Connected Stations...**
2. En la sección **Connected Stations**, haga clic en el botón de opción junto al cliente que desea desconectar. Cada entrada muestra el nombre del programa cliente y opcionalmente el nombre de la estación. Los clientes desconocidos se etiquetan como "client 0x&lt;HEX&gt;".
3. Haga clic en **Disconnect Station** (el botón rojo). El botón solo se habilita después de seleccionar una estación.
4. AetherSDR intentará ahora conectarse al espacio liberado.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Radio section** | Sección de solo lectura en la parte superior que muestra el modelo de radio, apodo e indicativo de la radio conectada. |
| **Station radio buttons** | Uno por cada cliente conectado. Al seleccionar uno, se habilita **Disconnect Station**. |
| **Disconnect Station** | Desconecta el cliente seleccionado de la radio. La etiqueta es roja. |
| **Cancel** | Cierra el cuadro de diálogo sin desconectar. |
| **Info label** | Explica que multiFLEX está deshabilitado y que debe seleccionar una estación para desconectar. |

## Solución de problemas

- **El botón Disconnect Station está atenuado** — Seleccione una estación haciendo clic en su botón de opción. El botón permanece deshabilitado hasta que se realiza una selección.
- **El cuadro de diálogo no aparece, pero sabe que otro cliente está conectado** — Ábralo manualmente a través de **Help > Connected Stations...**

## Relacionado

- [Ver todas las estaciones conectadas cuando multiFLEX está desactivado](see-all-stations-connected-when-multiflex-is-off.md)
- [Identificar cada cliente por programa y nombre de estación](../../features/connected-stations/identify-each-client-by-program-and-station-name.md)
