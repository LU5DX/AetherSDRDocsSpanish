# Descripción general del servidor TCI

El applet del servidor TCI ejecuta un servidor WebSocket que utiliza el protocolo TCI de Expert Electronics, permitiendo que aplicaciones externas de registro, modo digital y SDR — como Log4OM y herramientas SunSDR — lean y controlen la radio a través de una conexión de red local. Abra el applet para iniciar el servidor, configurar el puerto y ajustar la ganancia de audio para cada canal de RX y TX.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión activa con la radio.
- Esta función solo está presente en compilaciones creadas con soporte para WebSocket (`HAVE_WEBSOCKETS`). Si el botón de la bandeja TCI no aparece, su compilación no incluye TCI.

## Cómo funciona

El applet TCI está oculto de forma predeterminada. Actívelo con el botón **TCI** en la bandeja de la barra lateral derecha.

Al hacer clic en **Enable**, AetherSDR vincula un servidor WebSocket en el puerto configurado (predeterminado `50001`). Cualquier cliente compatible con TCI que se conecte a `ws://<su-host>:<puerto>` podrá consultar y comandar la radio mediante el protocolo TCI. El applet muestra el estado actual del servidor y la cantidad de clientes conectados en el área de estado junto al botón **Enable**.

El audio de RX para los canales 1 a 4 sigue las mismas asignaciones de canales DAX que el applet DAX. La letra de slice que aparece junto a cada fila de RX y TX — por ejemplo, `Slice A` — refleja el slice asignado actualmente a ese canal DAX. Si no hay ningún slice asignado, el indicador muestra `—`.

Los niveles de ganancia establecidos en el applet se aplican al flujo de audio TCI y son independientes de los controles de ganancia de RF de la radio.

## Qué hace cada control

| Control                       | Qué hace                                                                                                                                                                                                                             | Valor predeterminado                                                                                                                                                                                                                                               |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ganancia+medidor RX1–RX4      | Medidor de nivel y control deslizante de ganancia combinados para cada canal TCI RX. Arrastre para ajustar la ganancia de salida del flujo de audio de ese canal.                                                                     | 0.5                                                                                                                                                                                                                                                                |
| Ganancia+medidor TX           | Arrastrar ajusta la ganancia TCI TX y emite tciTxGainChanged.                                                                                                                                                                        | TciServer::setTxGain conserva TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TCI TX siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). |
| Etiquetas de asignación RX/TX | Indicadores de solo lectura que muestran qué slice controla cada fila (`Slice A`, `Slice B`, etc., o `—` si no está asignado).                                                                                                       | `—`                                                                                                                                                                                                                                                                |
| Puerto                        | Puerto WebSocket en el que escucha el servidor. Cambiar el valor mientras el servidor está en ejecución lo reinicia en el nuevo puerto. Los valores fuera del rango válido se restablecen a `50001`.                                  | `50001`                                                                                                                                                                                                                                                            |
| Enable                        | Inicia o detiene el servidor TCI. Si el puerto ya está en uso, el botón vuelve a la posición de apagado y el estado muestra `(port in use)` en rojo.                                                                                 | Apagado                                                                                                                                                                                                                                                            |
| Estado del servidor           | Muestra `(stopped)`, `:<puerto> (<N> clientes)` o `(port in use)`. Se vuelve rojo en caso de error de vinculación.                                                                                                                    | `(stopped)`                                                                                                                                                                                                                                                        |

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que se lance AetherSDR, active `Settings > Autostart TCI with AetherSDR`. Esto establece la preferencia `AutoStartTCI`.
- El contador de clientes que se muestra en el estado del servidor se actualiza en vivo a medida que los clientes se conectan y desconectan. Consulte [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md) para más detalles.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable se desactiva** — Otro proceso ya está vinculado a ese puerto. Cambie el puerto en el campo Port a un puerto libre en el rango 1024–65535 y haga clic en Enable nuevamente. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El botón de la bandeja TCI no aparece** — Esta compilación de AetherSDR fue compilada sin soporte para WebSocket. TCI no está disponible.
- **Las etiquetas de slice muestran `—` para todos los canales** — No hay slices con un canal DAX asignado. Asigne un canal DAX a un slice a través de la configuración de la radio para completar las etiquetas RX y TX.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia TCI RX por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TCI TX](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al lanzar](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
