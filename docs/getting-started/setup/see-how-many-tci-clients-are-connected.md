# Vea cuántos clientes TCI están conectados

El applet del Servidor TCI muestra un conteo de clientes en vivo en su indicador de estado. Úselo para confirmar que Log4OM, herramientas SunSDR o cualquier otro cliente TCI se haya conectado exitosamente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El applet TCI requiere una conexión de radio activa.
- El servidor TCI debe estar en ejecución (Enable activado). Si está detenido, el estado muestra `(stopped)` y no hay conteo de clientes disponible.

## Pasos

1. Haga clic en el botón **TCI** de la bandeja en la barra lateral derecha para abrir el applet del Servidor TCI.
2. Lea el indicador de estado junto al campo Port.

Cuando el servidor está en ejecución y al menos un cliente está conectado, el estado muestra:

```
:<puerto> (N clients)
```

Por ejemplo, con dos clientes conectados en el puerto predeterminado:

```
:50001 (2 clients)
```

Cuando el servidor está en ejecución pero no hay clientes conectados, el estado muestra el puerto y `(0 clients)`. Cuando el servidor está detenido, el estado muestra `(stopped)`.

## Función de cada control

| Control            | Descripción                                                                                 | Valor predeterminado                                                                                                                                                                                                                                               |
|--------------------|---------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Port               | Puerto en el que escucha el servidor WebSocket TCI. Los valores fuera de rango se ajustan a `50001`. | `50001`                                                                                                                                                                                                                                                             |
| Enable             | Inicia o detiene el servidor TCI.                                                             | Off                                                                                                                                                                                                                                                                 |
| Server status      | Muestra `(stopped)`, `:<puerto> (N clients)` o `(port in use)`. Se vuelve rojo si falla la vinculación. | `(stopped)`                                                                                                                                                                                                                                                         |
| RX1–RX4 gain+meter | Control deslizante de ganancia e indicador de nivel para cada canal RX de TCI.                | 0.5                                                                                                                                                                                                                                                                 |
| TX gain+meter      | Los arrastres establecen la ganancia TX de TCI y emiten tciTxGainChanged.                    | TciServer::setTxGain persiste TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). |

## Consejos

- El conteo de clientes se actualiza automáticamente cuando un cliente se conecta o desconecta; no es necesario recargar.
- Cuando hay un cliente conectado, el estado muestra `(1 client)` (singular); dos o más muestran `(N clients)` (plural).
- El texto de estado se vuelve azul cuando uno o más clientes están conectados, lo que facilita su identificación de un vistazo.

## Solución de problemas

- **El estado muestra `(port in use)`** — Otro proceso ya está vinculado al puerto configurado. Cambie el valor en el campo Port a un puerto no utilizado en el rango 1024–65535 y presione Enter. El servidor se reinicia automáticamente si Enable está activado.
- **El estado permanece `(stopped)` después de hacer clic en Enable** — La vinculación falló y Enable volvió a apagarse. Verifique el valor de Port y confirme que ninguna otra aplicación esté usando ese puerto.
- **El conteo de clientes se mantiene en 0** — Confirme que la aplicación de terceros esté configurada para conectarse al host y puerto correctos. El puerto en uso se muestra en el indicador de estado.

## Relacionados

- [Enable the TCI server for Log4OM / SunSDR clients](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Change the TCI port](../../features/tci/change-the-tci-port.md)
- [Autostart TCI on launch](../../features/tci/autostart-tci-on-launch.md)
- [TCI Server overview](../../features/tci/overview.md)
