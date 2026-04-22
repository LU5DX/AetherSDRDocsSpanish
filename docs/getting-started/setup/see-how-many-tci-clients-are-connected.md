# Ver cuántos clientes TCI están conectados

El applet TCI Server muestra un conteo de clientes en tiempo real en su indicador de estado. Úselo para confirmar que el software externo (Log4OM, herramientas SunSDR, etc.) se ha conectado correctamente al servidor TCI de AetherSDR.

## Antes de comenzar

- El servidor TCI debe estar en ejecución. El indicador de estado muestra `(stopped)` si no lo está. Haga clic en Enable en el applet TCI para iniciarlo, o consulte [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md).
- AetherSDR debe estar conectado a un radio. El applet TCI requiere una conexión activa con el radio.

## Pasos

1. Haga clic en el botón **TCI** de la barra lateral derecha para abrir el applet TCI Server.
2. Observe el indicador de estado a la izquierda del botón Enable.

El indicador muestra el estado actual en una de tres formas:

| Texto de estado | Significado |
|---|---|
| `(stopped)` | El servidor no está en ejecución. |
| `:<port> (N clients)` | El servidor está ejecutándose en el puerto indicado; N es el número de clientes conectados. |
| `(port in use)` | El servidor no pudo enlazarse; el puerto está ocupado por otro proceso. |

Cuando hay uno o más clientes conectados, el texto del indicador se muestra en azul. Cuando el servidor está en ejecución pero no hay clientes conectados, el texto aparece en gris. El conteo se actualiza automáticamente cada vez que un cliente se conecta o desconecta.

## Consejos

- El conteo de clientes refleja las conexiones WebSocket abiertas actualmente hacia el servidor TCI. Si un cliente se desconecta de forma abrupta, el conteo disminuye en cuanto AetherSDR detecta la conexión cerrada.
- El puerto que aparece en el indicador de estado coincide con el valor del campo Port (valor predeterminado `50001`, almacenado como `TciPort`). Si cambió el puerto, confirme que el cliente externo apunta al mismo valor.

## Solución de problemas

- **El estado permanece en `(stopped)` incluso después de hacer clic en Enable** — Es posible que el puerto ya esté en uso por otra aplicación. El indicador de estado mostrará `(port in use)` en rojo. Cambie el valor de Port a un puerto libre en el rango 1024–65535 y haga clic en Enable nuevamente. Los valores fuera de rango se restablecen automáticamente a `50001`.
- **El conteo de clientes permanece en 0** — Verifique que la aplicación externa esté configurada para conectarse al host y al puerto correctos. Compruebe que ningún firewall esté bloqueando el puerto TCI.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Inicio automático de TCI al arrancar](../../features/tci/autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](../../features/tci/overview.md)
