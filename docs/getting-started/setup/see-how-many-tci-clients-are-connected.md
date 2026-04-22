# Ver cuántos clientes TCI están conectados

El applet TCI Server muestra un conteo de clientes en tiempo real en su indicador de estado. Use esta página para abrir el applet y leer ese conteo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- El servidor TCI debe estar habilitado. Si no está en ejecución, el estado muestra `(stopped)` y no hay conteo de clientes disponible.

## Pasos

1. Haga clic en el botón **TCI** de la barra lateral derecha para abrir el applet TCI Server.
2. Observe el indicador de estado en la fila inferior del applet, a la derecha del campo **Port**.
3. Lea el conteo de clientes. Cuando el servidor está en ejecución, el estado muestra `:<port> (N clients)` — por ejemplo, `:50001 (2 clients)`. Cuando no hay clientes conectados, muestra `:50001 (0 clients)`. Cuando el servidor está detenido, muestra `(stopped)`.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango / Estados | Clave de configuración |
|---|---|---|---|---|
| **Port** | El puerto en el que escucha el servidor WebSocket de TCI. Al cambiarlo se reinicia el servidor si está habilitado. Los valores fuera de rango se ajustan a `50001`. | `50001` | 1024–65535 | `TciPort` |
| **Enable** | Inicia o detiene el servidor TCI. Si el puerto ya está en uso, el interruptor regresa a desactivado y el estado muestra `(port in use)`. | Off | On / Off | — |
| Indicador de estado del servidor | Muestra el estado actual del servidor y el conteo de clientes conectados. Se vuelve azul cuando hay uno o más clientes conectados; se vuelve rojo si falla el enlace. | `(stopped)` | `(stopped)`, `:<port> (N clients)`, `(port in use)` | — |
| Ganancia+medidor **RX1–RX4** | Medidor y deslizador combinados que ajustan la ganancia de TCI RX para cada canal. | 0.5 | 0.0–1.0 | `TciRxGain1`–`TciRxGain4` |
| Ganancia+medidor **TX** | Medidor y deslizador combinados que ajustan la ganancia de TCI TX. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Etiquetas de asignación de slice RX/TX | Indican qué slice controla cada fila RX o TX. Muestran `—` cuando no hay ningún slice asignado, o `Slice <letter>` cuando hay uno. | `—` | `—` o `Slice <letter>` | — |

## Consejos

- El conteo de clientes se actualiza en tiempo real. No es necesario volver a abrir el applet; el indicador de estado se actualiza cada vez que un cliente se conecta o desconecta.
- Si el estado muestra `(port in use)`, otra aplicación ya está usando ese puerto. Cambie el valor en el campo **Port** a un número diferente en el rango 1024–65535 y presione Enter.

## Solución de problemas

- **El estado muestra `(stopped)` aunque Enable aparece activo** — El enlace falló de forma silenciosa. Cierre y vuelva a abrir el applet. Haga clic en **Enable** nuevamente. Si el estado muestra inmediatamente `(port in use)`, elija un puerto diferente.
- **El conteo de clientes se mantiene en 0** — Confirme que la aplicación de terceros esté configurada para conectarse al mismo puerto que se muestra en el campo **Port**, y que ningún cortafuegos esté bloqueando ese puerto.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Inicio automático de TCI al arrancar](../../features/tci/autostart-tci-on-launch.md)
- [Descripción general de TCI Server](../../features/tci/overview.md)
