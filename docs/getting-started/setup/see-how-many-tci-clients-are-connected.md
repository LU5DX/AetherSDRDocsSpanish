# Ver cuántos clientes TCI están conectados

El applet TCI Server muestra un conteo de clientes en tiempo real en su indicador de estado. Use esto para confirmar que Log4OM, las herramientas SunSDR u cualquier otro cliente TCI se ha conectado correctamente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El applet TCI requiere una conexión de radio activa.
- El servidor TCI debe estar en ejecución (Enable activado). Si está detenido, el estado muestra `(stopped)` y no hay conteo de clientes disponible.

## Pasos

1. Haga clic en el botón **TCI** de la barra lateral derecha para abrir el applet TCI Server.
2. Lea el indicador de estado junto al campo Port.

Cuando el servidor está en ejecución y al menos un cliente está conectado, el estado muestra:

```
:<port> (N clients)
```

Por ejemplo, con dos clientes conectados en el puerto predeterminado:

```
:50001 (2 clients)
```

Cuando el servidor está en ejecución pero no hay clientes conectados, el estado muestra el puerto y `(0 clients)`. Cuando el servidor está detenido, el estado muestra `(stopped)`.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Port | Puerto en el que escucha el servidor WebSocket TCI. Los valores fuera de rango se ajustan a `50001`. | `50001` | 1024–65535 | `TciPort` |
| Enable | Inicia o detiene el servidor TCI. | Off | On / Off | — |
| Server status | Muestra `(stopped)`, `:<port> (N clients)` o `(port in use)`. Se pone rojo si falla el enlace. | `(stopped)` | — | — |
| RX1–RX4 gain+meter | Control deslizante de ganancia y medidor de nivel para cada canal TCI RX. | 0.5 | 0.0–1.0 | `TciRxGain1`–`TciRxGain4` |
| TX gain+meter | Control deslizante de ganancia y medidor de nivel para el canal TCI TX. | 0.5 | 0.0–1.0 | `TciTxGain` |

## Consejos

- El conteo de clientes se actualiza automáticamente cada vez que un cliente se conecta o desconecta — no es necesario actualizar manualmente.
- Cuando hay un cliente conectado, el estado muestra `(1 client)` (singular); con dos o más muestra `(N clients)` (plural).
- El texto de estado se pone azul cuando hay uno o más clientes conectados, lo que facilita identificarlo de un vistazo.

## Solución de problemas

- **El estado muestra `(port in use)`** — Otro proceso ya está vinculado al puerto configurado. Cambie el valor en el campo Port a un puerto disponible en el rango 1024–65535 y presione Enter. El servidor se reinicia automáticamente si Enable está activado.
- **El estado permanece en `(stopped)` después de hacer clic en Enable** — El enlace falló y Enable volvió a desactivarse. Verifique el valor de Port y confirme que ninguna otra aplicación esté usando ese puerto.
- **El conteo de clientes permanece en 0** — Confirme que la aplicación de terceros esté configurada para conectarse al host y puerto correctos. El puerto en uso se muestra en el indicador de estado.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Inicio automático de TCI al arrancar](../../features/tci/autostart-tci-on-launch.md)
- [Descripción general de TCI Server](../../features/tci/overview.md)
