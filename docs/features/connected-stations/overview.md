# Vista general de Estaciones Conectadas

Cuando multiFLEX está deshabilitado en su FLEX-8600, solo una estación cliente puede estar conectada a la vez. El cuadro de diálogo de Estaciones Conectadas enumera cada cliente actualmente conectado al radio, para que pueda identificar y desconectar otra sesión antes de conectar AetherSDR.

## Cómo funciona

El cuadro de diálogo se abre automáticamente cuando AetherSDR intenta conectarse a un radio que tiene multiFLEX deshabilitado y otro cliente ya está conectado. También puede abrirlo manualmente desde **Help > Connected Stations...**.

El cuadro de diálogo está dividido en dos secciones:

**Radio section** — Muestra el modelo, apodo e indicativo del radio conectado como información de solo lectura. Esto ayuda a confirmar que está viendo el radio correcto.

**Connected Stations section** — Enumera cada cliente conectado con un botón de opción. Para cada entrada, ve el nombre del programa cliente y, si está disponible, el nombre de la estación. Si no se conoce ninguno, la etiqueta de respaldo muestra "client 0x<HEX>" usando el identificador del cliente.

Seleccione una estación haciendo clic en su botón de opción, luego haga clic en **Disconnect Station** para eliminar ese cliente del radio. El botón se habilita solo cuando una estación está seleccionada. Haga clic en **Cancel** para cerrar el cuadro de diálogo sin desconectar.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---------|---------------|-------|
| Radio section | Bloque de solo lectura que muestra modelo, apodo e indicativo del radio | El encabezado de la sección dice "Radio" |
| Station radio buttons | Selecciona qué estación desconectar | Cada entrada muestra el nombre del programa y opcionalmente el nombre de la estación. Respaldo: "client 0x<HEX>" |
| **Disconnect Station** | Desconecta la estación seleccionada del radio | Habilitado solo cuando un botón de opción está marcado. Estilo rojo/tema oscuro |
| **Cancel** | Cierra el cuadro de diálogo sin desconectar | |
| Info label | Explica que multiFLEX está deshabilitado y se debe desconectar una estación primero | Texto completo: "multiFLEX is disabled on this radio. Select a station to disconnect before connecting AetherSDR." |

## Consejos

- El cuadro de diálogo es modal para la aplicación: no puede interactuar con la ventana principal de AetherSDR hasta que desconecte una estación o haga clic en Cancel.

## Relacionados

- [Desconectar otro cliente para liberar un espacio](../../getting-started/setup/disconnect-another-client-to-free-a-slot.md)
- [Identificar cada cliente por programa y nombre de estación](identify-each-client-by-program-and-station-name.md)
- [Ver todas las estaciones conectadas cuando multiFLEX está apagado](../../getting-started/setup/see-all-stations-connected-when-multiflex-is-off.md)
