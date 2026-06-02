# Resumen de Estaciones Conectadas

Cuando multiFLEX está deshabilitado en su FLEX-8600, solo una estación cliente puede estar conectada a la vez. El diálogo de Estaciones Conectadas lista cada cliente actualmente conectado a la radio, para que pueda identificar y desconectar otra sesión antes de conectar AetherSDR.

## Cómo funciona

El diálogo se abre automáticamente cuando AetherSDR intenta conectarse a una radio que tiene multiFLEX deshabilitado y otro cliente ya conectado. También puede abrirlo manualmente desde **Help > Connected Stations...**.

El diálogo está dividido en dos secciones:

**Sección Radio** — Muestra el modelo, apodo e indicativo de la radio conectada como información de solo lectura. Esto ayuda a confirmar que está viendo la radio correcta.

**Sección Estaciones Conectadas** — Lista cada cliente conectado con un botón de opción. Para cada entrada, ve el nombre del programa cliente y, si está disponible, el nombre de la estación. Si no se conoce ninguno, la etiqueta de respaldo muestra "client 0x<HEX>" usando el identificador del cliente.

Seleccione una estación haciendo clic en su botón de opción, luego haga clic en **Disconnect Station** para eliminar ese cliente de la radio. El botón solo está habilitado cuando una estación está seleccionada. Haga clic en **Cancel** para cerrar el diálogo sin desconectar.

## Función de cada control

| Control | Comportamiento | Notas |
|---------|----------|-------|
| Sección Radio | Bloque de solo lectura que muestra modelo, apodo e indicativo de la radio | El encabezado de sección dice "Radio" |
| Botones de opción de estación | Selecciona qué estación desconectar | Cada entrada muestra el nombre del programa y opcionalmente el nombre de la estación. Respaldo: "client 0x<HEX>" |
| **Disconnect Station** | Desconecta la estación seleccionada de la radio | Solo habilitado cuando un botón de opción está marcado. Con estilo rojo/tema oscuro |
| **Cancel** | Cierra el diálogo sin desconectar | |
| Etiqueta informativa | Explica que multiFLEX está deshabilitado y se debe desconectar una estación primero | Texto completo: "multiFLEX is disabled on this radio. Select a station to disconnect before connecting AetherSDR." |

## Consejos

- El diálogo es modal de aplicación — no puede interactuar con la ventana principal de AetherSDR hasta que desconecte una estación o haga clic en Cancel.
- El diálogo aplica el estilo de contenedor del tema `dialog/connectedStations` para una apariencia consistente con el resto de la aplicación.

## Relacionado

- [Desconectar otro cliente para liberar un espacio](../../getting-started/setup/disconnect-another-client-to-free-a-slot.md)
- [Identificar cada cliente por programa y nombre de estación](identify-each-client-by-program-and-station-name.md)
- [Ver todas las estaciones conectadas cuando multiFLEX está desactivado](../../getting-started/setup/see-all-stations-connected-when-multiflex-is-off.md)
