# Resumen del servidor TCI

El applet del servidor TCI ejecuta un servidor WebSocket que habla el protocolo TCI de Expert Electronics, permitiendo que aplicaciones de terceros para registro, modos digitales y SDR — como Log4OM y herramientas SunSDR — lean y controlen el radio a través de una conexión de red local. Abra el applet para iniciar el servidor, configurar el puerto y ajustar la ganancia de audio para cada canal de RX y TX.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TCI requiere una conexión activa al radio.
- Esta funcionalidad solo está presente en compilaciones realizadas con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón de la bandeja TCI no aparece, su compilación no incluye TCI.

## Cómo funciona

El applet TCI está oculto de forma predeterminada. Actívelo con el botón de la bandeja **TCI** en la barra lateral derecha.

Al hacer clic en **Enable**, AetherSDR vincula un servidor WebSocket en el puerto configurado (predeterminado `50001`). Cualquier cliente compatible con TCI que se conecte a `ws://<su-host>:<puerto>` podrá consultar y comandar el radio usando el protocolo TCI. El applet muestra el estado actual del servidor y la cantidad de clientes conectados en el área de estado junto al botón **Enable**.

El audio de RX para los canales 1–4 sigue las mismas asignaciones de canales DAX que el applet DAX. La letra de slice que aparece junto a cada fila de RX y TX — por ejemplo, `Slice A` — refleja el slice actualmente asignado a ese canal DAX. Si no hay ningún slice asignado, el indicador muestra `—`.

Los niveles de ganancia configurados en el applet se aplican al flujo de audio TCI y son independientes de los controles de ganancia de RF del radio.

## Qué hace cada control

| Control                           | Qué hace                                                                                                                                                                                                                              | Valor predeterminado                                                                                                                                                                                                                                                |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Medidor+ganancia RX1–RX4          | Medidor de nivel y control deslizante de ganancia combinados para cada canal TCI de RX. Arrastre para configurar la ganancia de salida del flujo de audio de ese canal.                                                                | 0.5                                                                                                                                                                                                                                                                 |
| Medidor+ganancia TX               | Arrastrar configura la ganancia TCI de TX y emite tciTxGainChanged.                                                                                                                                                                    | TciServer::setTxGain persiste TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TCI de TX siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). |
| Etiquetas de asignación de slice RX/TX | Indicadores de solo lectura que muestran qué slice maneja cada fila (`Slice A`, `Slice B`, etc., o `—` si no está asignado). Usa formato de texto enriquecido para que las letras de slice se rendericen correctamente (#2606). | `—`                                                                                                                                                                                                                                                                 |
| Puerto                           | Puerto WebSocket en el que escucha el servidor. Cambiar el valor mientras el servidor está en ejecución lo reinicia en el nuevo puerto. Los valores fuera del rango válido vuelven a `50001`.                                           | `50001`                                                                                                                                                                                                                                                             |
| Enable                           | Inicia o detiene el servidor TCI. Si el puerto ya está en uso, el botón vuelve a la posición de apagado y el estado muestra `(port in use)` en rojo.                                                                                  | Off                                                                                                                                                                                                                                                                 |
| Estado del servidor              | Muestra `(stopped)`, `:<puerto> (<N> clientes)` o `(port in use)`. Se vuelve rojo en caso de error de enlace.                                                                                                                         | `(stopped)`                                                                                                                                                                                                                                                         |

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que AetherSDR se inicie, active `Settings > Autostart TCI with AetherSDR`. Esto establece la preferencia `AutoStartTCI`.
- El recuento de clientes que se muestra en el estado del servidor se actualiza en vivo a medida que los clientes se conectan y desconectan. Consulte [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md) para obtener más detalles.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable se desactiva** — Otro proceso ya está vinculado a ese puerto. Cambie el puerto en el campo Port a un puerto libre en el rango 1024–65535 y haga clic en Enable nuevamente. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **Falta el botón de la bandeja TCI** — Esta compilación de AetherSDR se compiló sin soporte WebSocket. TCI no está disponible.
- **Las etiquetas de slice muestran `—` para todos los canales** — Ningún slice tiene asignado un canal DAX. Asigne un canal DAX a un slice a través de la configuración del radio para completar las etiquetas de RX y TX.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia TCI de RX por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TCI de TX](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al iniciar](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
