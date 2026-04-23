# Descripción general del servidor TCI

El applet del servidor TCI ejecuta un servidor WebSocket dentro de AetherSDR que implementa el protocolo TCI de Expert Electronics. Aplicaciones de registro, modos digitales y SDR de terceros — como Log4OM y las herramientas de SunSDR — pueden conectarse a este servidor para leer y controlar la radio sin necesidad de software de puente adicional.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- El applet TCI está oculto por defecto. Haga clic en el botón TCI de la bandeja en la barra lateral derecha para mostrarlo.

## Cómo funciona

Al hacer clic en Enable, AetherSDR enlaza un servidor WebSocket al puerto configurado (por defecto `50001`). Cualquier cliente compatible con TCI en la misma red puede entonces conectarse a `<host>:<port>`. El servidor admite hasta cuatro flujos de audio RX simultáneos, un flujo de audio TX y control bidireccional de frecuencia y modo.

Cada canal RX se corresponde con una asignación de canal DAX. Los indicadores de asignación de slice (slice — canal de recepción independiente) junto a cada fila RX y TX muestran qué slice controla actualmente ese canal; por ejemplo, `Slice A`. Si no hay ningún slice asignado, el indicador muestra `—`.

El indicador de estado del servidor se actualiza en tiempo real conforme los clientes se conectan y desconectan. Cuando el servidor está en ejecución, muestra `:<port> (N clients)`. Cuando está detenido, muestra `(stopped)`. Si el puerto ya está en uso al hacer clic en Enable, el estado muestra `(port in use)` en rojo y Enable vuelve automáticamente a la posición desactivada.

Puede configurar el servidor para que se inicie automáticamente cada vez que AetherSDR arranque mediante `Settings > Autostart TCI with AetherSDR`.

## Qué hace cada control

| Control | Descripción | Valor por defecto | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Ganancia+medidor RX1–RX4 | Medidor de nivel y control deslizante de ganancia combinados para cada canal TCI RX. Arrastre para ajustar la ganancia. | 0.5 | 0.0–1.0 | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| Ganancia+medidor TX | Medidor de nivel y control deslizante de ganancia combinados para el canal TCI TX. Arrastre para ajustar la ganancia. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Port | Puerto WebSocket en el que escucha el servidor. Si se cambia mientras el servidor está en ejecución, el servidor se reinicia de inmediato. Los valores fuera del rango 1024–65535 se ajustan automáticamente a `50001`. | `50001` | 1024–65535 | `TciPort` |
| Enable | Inicia o detiene el servidor TCI. Si el puerto no puede enlazarse, el botón vuelve automáticamente a la posición desactivada. | Off | On / Off | — |
| Etiquetas de asignación de slice RX/TX | Indicadores de solo lectura que muestran qué slice está asignado a cada fila RX o TX. Muestra `Slice <letter>` o `—`. | `—` | `—` o `Slice <letter>` | — |
| Estado del servidor | Muestra el estado actual del servidor y el número de clientes conectados. Se muestra en rojo si falla el enlace del puerto. | `(stopped)` | `(stopped)`, `:<port> (N clients)`, `(port in use)` | — |

## Temas relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia TCI RX por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TCI TX](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al arrancar](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
