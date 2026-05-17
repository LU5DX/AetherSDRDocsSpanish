# Vea cuántos clientes TCI están conectados

El applet del Servidor TCI muestra un conteo en vivo de clientes en su indicador de estado. Úselo para confirmar que Log4OM, herramientas SunSDR o cualquier otro cliente TCI se ha conectado exitosamente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. El applet TCI requiere una conexión activa con la radio.
- El servidor TCI debe estar en ejecución (Enable activado). Si está detenido, el estado muestra `(stopped)` y no hay conteo de clientes disponible.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha para abrir el applet del Servidor TCI.
2. Lea el indicador de estado junto al campo Port.

Cuando el servidor está en ejecución y al menos un cliente está conectado, el estado muestra:

```
:<puerto> (N clients)
```

Por ejemplo, con dos clientes conectados en el puerto predeterminado:

```
:50001 (2 clients)
```

Cuando el servidor está en ejecución pero ningún cliente está conectado, el estado muestra el puerto y `(0 clients)`. Cuando el servidor está detenido, el estado muestra `(stopped)`.

## Qué hace cada control

| Control                          | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Valor predeterminado                                                                                                                                        |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Port                             | Puerto en el que escucha el servidor WebSocket TCI. Los valores fuera de rango se ajustan a `50001`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | `50001`                                                                                                                                                     |
| Enable                           | Inicia o detiene el servidor TCI.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Desactivado                                                                                                                                                 |
| Server status                    | Muestra `(stopped)`, `:<puerto> (N clients)` o `(port in use)`. Se vuelve rojo en caso de fallo de enlace.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | `(stopped)`                                                                                                                                                 |
| RX1–RX4 gain+meter               | Medidor/deslizador combinado; al arrastrar se ajusta la ganancia RX de TCI para el canal y emite `tciRxGainChanged`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | 0.5                                                                                                                                                         |
| TX gain+meter                    | Al arrastrar se ajusta la ganancia TX de TCI y emite `tciTxGainChanged`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | 0.5                                                                                                                                                         |
| RX/TX slice-assignment labels    | Muestra qué slice controla actualmente cada fila RX/TX. Muestra `—` cuando no hay ningún slice asignado o `Slice <letra>` cuando hay un slice mapeado. La letra del slice se renderiza en texto enriquecido para admitir formato HTML (v26.5.2.1, #2606).                                                                                                                                                                                                                                                                                                                                       | `—`                                                                                                                                                         |

## Consejos

- El conteo de clientes se actualiza automáticamente cuando un cliente se conecta o desconecta, no es necesario actualizar.
- Cuando hay un cliente conectado, el estado muestra `(1 client)` (singular); dos o más muestran `(N clients)` (plural).
- El texto de estado se vuelve azul cuando hay uno o más clientes conectados, lo que facilita identificarlo de un vistazo.

## Solución de problemas

- **El estado muestra `(port in use)`** — Otro proceso ya está enlazado al puerto configurado. Cambie el valor en el campo Port a un puerto no utilizado en el rango 1024–65535 y presione Enter. El servidor se reinicia automáticamente si Enable está activado.
- **El estado permanece en `(stopped)` después de hacer clic en Enable** — El enlace falló y Enable volvió a desactivarse. Verifique el valor de Port y confirme que ninguna otra aplicación esté usando ese puerto.
- **El conteo de clientes se mantiene en 0** — Confirme que la aplicación de terceros esté configurada para conectarse al host y puerto correctos. El puerto en uso se muestra en el indicador de estado.

## Relacionado

- [Enable the TCI server for Log4OM / SunSDR clients](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Change the TCI port](../../features/tci/change-the-tci-port.md)
- [Autostart TCI on launch](../../features/tci/autostart-tci-on-launch.md)
- [TCI Server overview](../../features/tci/overview.md)
