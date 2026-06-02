# Ver todas las estaciones conectadas cuando multiFLEX está desactivado

Use el cuadro de diálogo **Connected Stations** para ver todos los clientes actualmente conectados a su radio FLEX-8600 cuando multiFLEX está deshabilitado. Esto le ayuda a identificar qué estación desconectar antes de que AetherSDR pueda tomar un espacio de conexión.

## Antes de comenzar

- Su radio debe estar encendida y accesible en la red.
- multiFLEX debe estar deshabilitado en la radio (el cuadro de diálogo solo aparece bajo esta condición).
- AetherSDR debe estar en proceso de conectarse a la radio (el cuadro de diálogo aparece automáticamente, o puede abrirlo manualmente).

## Pasos

1. Abra AetherSDR e intente conectarse a su radio.
   - Si multiFLEX está deshabilitado y otro cliente ya está conectado, **Connected Stations** aparece automáticamente.
2. Si necesita abrirlo más tarde: **Help > Connected Stations...**
3. Lea la sección **Radio** en la parte superior para confirmar el modelo, apodo e indicativo de la radio.
4. Revise la lista **Connected Stations** debajo. Cada entrada muestra el nombre del programa cliente y opcionalmente el nombre de la estación.
   - Si no se conoce el programa ni el nombre de la estación, la entrada muestra `client 0x<HEX>`.
5. Seleccione el botón de opción junto a la estación que desea desconectar.
6. Haga clic en **Disconnect Station**.
7. El cuadro de diálogo se cierra y AetherSDR continúa con su conexión.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Sección **Radio** | Bloque de información de solo lectura que muestra el modelo, apodo e indicativo de la radio conectada. |
| Botones de opción de estación | Seleccione qué estación desconectar. Cada entrada muestra el nombre del programa cliente y opcionalmente el nombre de la estación. Valor predeterminado: `client 0x<HEX>`. |
| **Disconnect Station** | Desconecta la estación seleccionada. Solo está habilitado cuando se ha marcado un botón de opción. |
| **Cancel** | Cierra el cuadro de diálogo sin desconectar. |
| Etiqueta informativa | Muestra "multiFLEX is disabled on this radio. Select a station to disconnect before connecting AetherSDR." |

## Consejos

- El cuadro de diálogo se centra en la pantalla donde se encuentra AetherSDR, o en su monitor principal si no está disponible.
- No puede conectar AetherSDR mientras otro cliente ocupa el único espacio disponible: debe desconectar uno primero.
- El cuadro de diálogo utiliza un estilo de contenedor temático que coincide con el tema del sistema o el seleccionado por el usuario.

## Relacionado

- [Desconectar otro cliente para liberar un espacio](disconnect-another-client-to-free-a-slot.md)
- [Identificar cada cliente por programa y nombre de estación](../../features/connected-stations/identify-each-client-by-program-and-station-name.md)
- [Resumen de Connected Stations](../../features/connected-stations/overview.md)
- [Ver todas las estaciones conectadas a esta FLEX](see-all-stations-connected-to-this-flex.md)
