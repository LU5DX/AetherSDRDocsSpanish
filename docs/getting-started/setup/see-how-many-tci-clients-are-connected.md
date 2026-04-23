# Ver cuántos clientes TCI están conectados

El applet TCI Server muestra un conteo de clientes en tiempo real en su indicador de estado cuando el servidor está en ejecución. Úselo para confirmar que un software externo como Log4OM o las herramientas de SunSDR se ha conectado correctamente.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. El applet TCI requiere una conexión de radio activa.
- El servidor TCI debe estar habilitado. Si no lo está, el indicador de estado muestra `(stopped)` y no hay conteo de clientes disponible.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha para abrir el applet TCI Server.
2. Lea el indicador de estado a la izquierda del botón **Enable**.

Cuando el servidor está en ejecución, el indicador muestra `:<puerto> (N clients)` — por ejemplo, `:50001 (2 clients)`. El conteo se actualiza automáticamente cada vez que un cliente se conecta o desconecta. Cuando no hay clientes conectados, el conteo muestra `0 clients`.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Port | Puerto TCP en el que escucha el servidor WebSocket TCI. Si se cambia mientras el servidor está en ejecución, el servidor se reinicia. Los valores fuera de rango vuelven a `50001`. | `50001` | 1024–65535 | `TciPort` |
| Enable | Inicia o detiene el servidor TCI. Si el puerto no puede enlazarse, el botón regresa a la posición apagada y el estado muestra `(port in use)`. | Off | — | — |
| Server status | Muestra `(stopped)`, `:<puerto> (N clients)` o `(port in use)`. Se vuelve rojo si ocurre un error de enlace. Se vuelve azul cuando uno o más clientes están conectados. | `(stopped)` | — | — |
| RX1–RX4 gain+meter | Medidor y control deslizante combinados que ajustan la ganancia TCI de RX para cada canal. | 0.5 | 0.0–1.0 | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| TX gain+meter | Medidor y control deslizante combinados que ajustan la ganancia TCI de TX. | 0.5 | 0.0–1.0 | `TciTxGain` |
| RX/TX slice-assignment labels | Muestran qué slice controla cada fila de RX o TX. Muestran `—` cuando no hay ningún slice asignado. | `—` | `—` o `Slice <letra>` | — |

## Solución de problemas

- **El estado muestra `(stopped)` aunque Enable aparece activo** — El enlace del puerto falló silenciosamente. Haga clic en **Enable** para desactivarlo, verifique que el puerto no esté en uso por otra aplicación y luego haga clic en **Enable** nuevamente.
- **El estado muestra `(port in use)`** — Otro proceso ya está escuchando en el puerto configurado. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable**.
- **El conteo de clientes permanece en 0 después de conectar el software externo** — Confirme que el software externo apunta al mismo puerto que se muestra en el campo **Port** y que ningún firewall está bloqueando la conexión.

## Temas relacionados

- [Descripción general del TCI Server](../../features/tci/overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Inicio automático de TCI al arrancar](../../features/tci/autostart-tci-on-launch.md)
