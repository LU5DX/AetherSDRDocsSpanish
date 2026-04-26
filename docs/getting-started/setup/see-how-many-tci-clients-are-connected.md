# Ver cuántos clientes TCI están conectados

El applet TCI Server muestra un recuento de clientes en tiempo real en su indicador de estado. Úselo para confirmar que software de terceros, como Log4OM o las herramientas SunSDR, se ha conectado correctamente.

## Antes de comenzar

- El servidor TCI debe estar en ejecución. El botón Enable debe estar activado (en verde).
- El applet TCI debe estar visible. Si no lo está, haga clic en el botón **TCI** de la bandeja en la barra lateral derecha para mostrarlo.

## Pasos

1. Haga clic en el botón **TCI** de la bandeja en la barra lateral derecha para abrir el applet TCI Server.
2. Lea el indicador de estado junto al campo Port en la parte inferior del applet. Cuando el servidor está en ejecución, muestra la forma `:<port> (N clients)` — por ejemplo, `:50001 (2 clients)`. El recuento se actualiza automáticamente cada vez que un cliente se conecta o desconecta.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Port | Puerto TCP en el que escucha el servidor WebSocket de TCI. Los valores fuera de rango se ajustan a 50001. | `50001` | 1024–65535 | `TciPort` |
| Enable | Inicia o detiene el servidor TCI. Al activarse, el botón se torna verde. Si el puerto ya está en uso, el interruptor vuelve a la posición de desactivado y el estado muestra `(port in use)` en rojo. | Off | — | — |
| Server status | Indicador de solo lectura que muestra el estado del servidor y el recuento de clientes conectados. Muestra `(stopped)`, `:<port> (N clients)` o `(port in use)`. El texto se torna azul cuando hay uno o más clientes conectados. | `(stopped)` | — | — |
| RX1–RX4 gain+meter | Medidor y control deslizante combinados que ajustan la ganancia RX de TCI para cada canal. | 0.5 | 0.0–1.0 | `TciRxGain1`–`TciRxGain4` |
| TX gain+meter | Medidor y control deslizante combinados que ajustan la ganancia TX de TCI. | 0.5 | 0.0–1.0 | `TciTxGain` |
| RX/TX slice-assignment labels | Solo lectura. Muestra qué slice maneja cada fila RX o TX (por ejemplo, `Slice A`), o `—` si no está asignado. | `—` | — | — |

## Solución de problemas

- **El estado muestra `(stopped)` en lugar del recuento de clientes** — Enable no ha sido activado, o el servidor se detuvo tras un fallo de vinculación. Haga clic en Enable para iniciar el servidor. Si el estado cambia inmediatamente a `(port in use)`, otra aplicación está ocupando el puerto configurado. Cambie el valor en el campo Port a un puerto libre en el rango 1024–65535 y haga clic en Enable nuevamente.
- **El estado muestra `:<port> (0 clients)` pero su software debería estar conectado** — Confirme que la aplicación externa se está conectando al mismo puerto que aparece en el indicador de estado. Verifique que ningún cortafuegos esté bloqueando el puerto.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Inicio automático de TCI al lanzar la aplicación](../../features/tci/autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](../../features/tci/overview.md)
