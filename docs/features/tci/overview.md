# Descripción general del servidor TCI

El applet del servidor TCI ejecuta un servidor WebSocket que implementa el protocolo TCI de Expert Electronics, lo que permite que aplicaciones de registro, modos digitales y SDR de terceros —como Log4OM y las herramientas de SunSDR— lean y controlen la radio a través de una conexión de red local. Abra el applet para iniciar el servidor, configurar el puerto y ajustar la ganancia de audio para cada canal RX y TX.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- Esta función solo está disponible en compilaciones realizadas con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón TCI en la bandeja no aparece, su compilación no incluye TCI.

## Cómo funciona

El applet TCI está oculto de forma predeterminada. Ábralo o ciérrelo con el botón **TCI** de la bandeja en la barra lateral derecha.

Al hacer clic en **Enable**, AetherSDR enlaza un servidor WebSocket en el puerto configurado (predeterminado `50001`). Cualquier cliente compatible con TCI que se conecte a `ws://<your-host>:<port>` puede consultar y controlar la radio usando el protocolo TCI. El applet muestra el estado actual del servidor y el número de clientes conectados en el área de estado junto al botón **Enable**.

El audio RX de los canales 1–4 sigue las mismas asignaciones de canal DAX que el applet DAX. La letra de slice (slice: segmento de recepción) que aparece junto a cada fila RX y TX —por ejemplo, `Slice A`— refleja el slice asignado en ese momento a ese canal DAX. Si no hay ningún slice asignado, el indicador muestra `—`.

Los niveles de ganancia configurados en el applet se aplican al flujo de audio TCI y son independientes de los controles de ganancia RF de la radio.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango válido | Clave persistente |
|---|---|---|---|---|
| Ganancia+medidor RX1–RX4 | Medidor de nivel y control deslizante de ganancia combinados para cada canal TCI RX. Arrastre para ajustar la ganancia de salida del flujo de audio de ese canal. | 0.5 | 0.0–1.0 | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| Ganancia+medidor TX | Medidor de nivel y control deslizante de ganancia combinados para el canal TCI TX. Arrastre para ajustar la ganancia de audio TX. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Etiquetas de asignación de slice RX/TX | Indicadores de solo lectura que muestran qué slice controla cada fila (`Slice A`, `Slice B`, etc., o `—` si no hay asignación). | `—` | `—` o `Slice <letter>` | — |
| Puerto | Puerto WebSocket en el que escucha el servidor. Si cambia el valor mientras el servidor está en ejecución, este se reiniciará en el nuevo puerto. Los valores fuera del rango válido vuelven automáticamente a `50001`. | `50001` | 1024–65535 | `TciPort` |
| Enable | Inicia o detiene el servidor TCI. Si el puerto ya está en uso, el botón regresa a la posición desactivada y el estado muestra `(port in use)` en rojo. | Desactivado | — | — |
| Estado del servidor | Muestra `(stopped)`, `:<port> (<N> clients)` o `(port in use)`. Se vuelve rojo si hay un error al enlazar. | `(stopped)` | — | — |

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que se lanza AetherSDR, habilite `Settings > Autostart TCI with AetherSDR`. Esto establece la preferencia `AutoStartTCI`.
- El recuento de clientes que se muestra en el estado del servidor se actualiza en tiempo real a medida que los clientes se conectan y desconectan. Consulte [Cómo ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md) para más detalles.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable se desactiva** — Otro proceso ya está enlazado a ese puerto. Cambie el puerto en el campo Port a un puerto libre en el rango 1024–65535 y haga clic en Enable nuevamente. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El botón TCI de la bandeja no aparece** — Esta compilación de AetherSDR fue realizada sin soporte WebSocket. TCI no está disponible.
- **Las etiquetas de slice muestran `—` en todos los canales** — Ningún slice tiene asignado un canal DAX. Asigne un canal DAX a un slice desde la configuración de la radio para que las etiquetas RX y TX se completen.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia TCI RX por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TCI TX](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al lanzar la aplicación](autostart-tci-on-launch.md)
- [Cómo ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
