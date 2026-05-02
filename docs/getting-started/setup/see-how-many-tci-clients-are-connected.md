# Ver cuántos clientes TCI están conectados

El applet TCI Server muestra un contador de clientes en tiempo real en su indicador de estado. Úselo para confirmar que Log4OM, las herramientas SunSDR u otro cliente TCI se han conectado correctamente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El applet TCI requiere una conexión de radio activa.
- El servidor TCI debe estar en ejecución (Enable activado). Si está detenido, el estado muestra `(stopped)` y el contador de clientes no está disponible.

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

| Control            | Descripción                                                                                          | Valor predeterminado                                                                                                                                                                                                                                                                    |
|--------------------|------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Port               | Puerto en el que escucha el servidor WebSocket TCI. Los valores fuera de rango se ajustan a `50001`. | `50001`                                                                                                                                                                                                                                                                                 |
| Enable             | Inicia o detiene el servidor TCI.                                                                    | Off                                                                                                                                                                                                                                                                                     |
| Server status      | Muestra `(stopped)`, `:<port> (N clients)` o `(port in use)`. Se torna rojo si falla el enlace.      | `(stopped)`                                                                                                                                                                                                                                                                             |
| RX1–RX4 gain+meter | Control deslizante de ganancia y medidor de nivel para cada canal RX TCI.                            | 0.5                                                                                                                                                                                                                                                                                     |
| TX gain+meter      | El control deslizante ajusta la ganancia TX TCI y emite tciTxGainChanged.                            | TciServer::setTxGain conserva TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX hospedado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). |

## Consejos

- El contador de clientes se actualiza automáticamente cada vez que un cliente se conecta o desconecta — no es necesario actualizar la pantalla.
- Cuando hay un cliente conectado, el estado muestra `(1 client)` (singular); con dos o más muestra `(N clients)` (plural).
- El texto del estado se torna azul cuando hay uno o más clientes conectados, lo que facilita identificarlo de un vistazo.

## Solución de problemas

- **El estado muestra `(port in use)`** — Otro proceso ya está vinculado al puerto configurado. Cambie el valor en el campo Port a un puerto libre en el rango 1024–65535 y presione Enter. El servidor se reinicia automáticamente si Enable está activado.
- **El estado permanece en `(stopped)` después de hacer clic en Enable** — El enlace falló y Enable volvió a desactivarse. Verifique el valor de Port y confirme que ninguna otra aplicación esté usando ese puerto.
- **El contador de clientes permanece en 0** — Confirme que la aplicación de terceros está configurada para conectarse al host y puerto correctos. El puerto en uso se muestra en el indicador de estado.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Inicio automático de TCI al lanzar la aplicación](../../features/tci/autostart-tci-on-launch.md)
- [Descripción general de TCI Server](../../features/tci/overview.md)
