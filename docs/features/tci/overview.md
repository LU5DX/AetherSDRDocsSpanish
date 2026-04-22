# Descripción general del servidor TCI

El applet TCI Server ejecuta un servidor WebSocket que habla el protocolo TCI de Expert Electronics, lo que permite que aplicaciones de terceros —como Log4OM, herramientas SunSDR y otras aplicaciones de registro o modos digitales compatibles con TCI— lean y controlen la radio sin una conexión directa a SmartSDR. Abra este applet para iniciar el servidor, configurar el puerto y ajustar los niveles de ganancia de audio por canal.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet TCI no está disponible sin una conexión de radio activa.
- La función TCI Server requiere una versión de AetherSDR que incluya soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón TCI en la bandeja no aparece, su versión no incluye esta función.

## Cómo funciona

El applet TCI está oculto de forma predeterminada. Ábralo o ciérrelo con el botón **TCI** de la bandeja en la barra lateral derecha. Una vez abierto, haga clic en **Enable** para enlazar el servidor al puerto configurado. Los clientes conectados se cuentan y se muestran en el indicador de estado del servidor.

El audio RX de cada canal TCI sigue las mismas asignaciones de canal DAX ya configuradas en sus slices (receptores virtuales). El slice que controla cada canal se muestra en las etiquetas de asignación RX/TX junto a cada medidor. Cuando ningún slice está asignado a un canal, la etiqueta muestra —.

El canal TX transporta el audio del slice que actualmente es el slice de transmisión.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Ganancia+medidor RX1–RX4 | Establece la ganancia de audio TCI RX para los canales 1–4. Arrastre para ajustar; el medidor muestra el nivel de señal en tiempo real. | 0.5 | 0.0–1.0 | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| Ganancia+medidor TX | Establece la ganancia de audio TCI TX. Arrastre para ajustar; el medidor muestra el nivel de señal en tiempo real. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Puerto | El puerto TCP en el que escucha el servidor WebSocket de TCI. Cambiar el puerto reinicia el servidor si ya está en ejecución. Los valores fuera del rango 1024–65535 vuelven automáticamente a 50001. | 50001 | 1024–65535 | `TciPort` |
| Enable | Inicia o detiene el servidor TCI. Si el puerto no puede enlazarse, el botón vuelve automáticamente a desactivado y el indicador de estado muestra `(port in use)` en rojo. | Off | — | — |
| Etiquetas de asignación RX/TX de slice | Indicadores de solo lectura que muestran qué slice controla cada fila RX o TX. Muestra `Slice <letra>` cuando hay un slice asignado, o — cuando no hay ninguno. | — | — o Slice A–H | — |
| Estado del servidor | Muestra el estado actual del servidor: `(stopped)`, `:<puerto> (<N> clients)` o `(port in use)`. Se vuelve rojo si falla el enlace. | (stopped) | — | — |

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que se inicia AetherSDR, use `Settings > Autostart TCI with AetherSDR`.
- Si el estado muestra `(port in use)`, otra aplicación ya está enlazada a ese puerto. Cambie el número de puerto y haga clic en **Enable** nuevamente.
- Los medidores de nivel RX utilizan suavizado exponencial: el nivel sube rápidamente con una señal y decae lentamente, de modo que los picos breves permanecen visibles.

## Solución de problemas

- **Enable vuelve automáticamente a desactivado de inmediato** — El servidor no pudo enlazarse al puerto especificado. Verifique que ninguna otra aplicación esté usando ese puerto, ingrese un valor diferente en Port y haga clic en **Enable**.
- **Las etiquetas de asignación de slice muestran — para todos los canales** — Ningún slice tiene canales DAX asignados. Configure las asignaciones de canal DAX en sus slices; los canales TCI RX siguen el mismo mapeo.
- **El botón TCI de la bandeja no es visible** — Su versión de AetherSDR no incluye soporte WebSocket. La función TCI Server no está disponible en esta versión.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia TCI RX por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TCI TX](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al lanzar la aplicación](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
