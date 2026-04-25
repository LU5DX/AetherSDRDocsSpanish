# Ver cuántos clientes TCI están conectados

El applet TCI Server muestra un recuento de clientes en tiempo real en su indicador de estado. Úselo para confirmar que el software de registro o de modos digitales se ha conectado correctamente al servidor TCI de AetherSDR.

## Antes de comenzar

- El servidor TCI debe estar en ejecución. Haga clic en Enable en el applet TCI si aún no está activo. Consulte [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md).
- AetherSDR debe estar conectado al radio. El applet TCI requiere una conexión de radio activa.

## Pasos

1. Haga clic en el botón de bandeja **TCI** de la barra lateral derecha para abrir el applet TCI Server.
2. Lea el indicador de estado del servidor en la fila inferior del applet, a la derecha del campo **Port**.

El indicador de estado muestra una de las siguientes opciones:

| Texto | Significado |
|------|---------|
| `(stopped)` | El servidor TCI no está en ejecución. |
| `:<port> (N clients)` | El servidor está en ejecución en el puerto indicado con N clientes conectados. |
| `(port in use)` | El servidor no pudo vincularse — otro proceso está usando el puerto. |

Cuando hay al menos un cliente conectado, el texto del estado se muestra en azul. Cuando el servidor está en ejecución pero no hay clientes conectados, el texto es gris.

## Consejos

- El recuento de clientes se actualiza automáticamente cada vez que un cliente se conecta o desconecta — no es necesario actualizar manualmente.
- Si espera que aparezca un cliente pero el recuento permanece en 0, confirme que el cliente apunta al puerto correcto. El puerto actual se muestra en el campo **Port** directamente a la izquierda del indicador de estado. El puerto predeterminado es `50001`.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable se desactiva** — otra aplicación ya está escuchando en el puerto configurado. Cambie el puerto a un valor diferente en el rango 1024–65535. Los valores fuera de este rango se revierten a `50001`. Consulte [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md).
- **El estado muestra `:<port> (0 clients)` pero el software externo está en ejecución** — verifique que el software externo esté configurado para conectarse al mismo puerto que aparece en el campo **Port** y a la dirección de host correcta.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Inicio automático de TCI al arrancar](../../features/tci/autostart-tci-on-launch.md)
- [Descripción general de TCI Server](../../features/tci/overview.md)
