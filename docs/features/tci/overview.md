# Descripción general del servidor TCI

El applet TCI Server ejecuta un servidor WebSocket que habla el protocolo Expert TCI, permitiendo que aplicaciones de terceros como Log4OM y las herramientas SunSDR lean y controlen la radio. Utilice esta página para entender lo que ofrece el applet; siga los enlaces para tareas específicas.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet TCI requiere una conexión de radio activa.
- El applet TCI solo está disponible en compilaciones que incluyen soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón TCI en la bandeja no está presente, su compilación no incluye esta función.

## Cómo funciona

El applet TCI Server escucha en un puerto TCP configurable y acepta conexiones WebSocket de clientes compatibles con TCI. Cuando un cliente se conecta, puede leer el audio del receptor, controlar los slices (canales de recepción) de la radio, y enviar y recibir audio en el canal TX.

Los canales RX 1–4 se corresponden con las mismas asignaciones de canal DAX utilizadas por el puente de audio DAX — la letra del slice que aparece junto a cada fila RX refleja el slice que tiene asignado ese canal DAX. La fila TX muestra el slice TX activo en ese momento. Los controles deslizantes de ganancia de cada canal permiten escalar el nivel de audio de forma independiente antes de que llegue al cliente conectado.

El indicador de estado del servidor en el applet muestra el estado actual:

| Texto de estado | Significado |
|---|---|
| `(stopped)` | El servidor no está en ejecución. |
| `:<port> (N clients)` | El servidor está activo en el puerto indicado con N clientes conectados. |
| `(port in use)` | Error de enlace; otro proceso ocupa el puerto. |

El estado se vuelve rojo cuando ocurre un error de enlace. Cuando el puerto ya está en uso, Enable vuelve automáticamente a la posición de desactivado.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Ganancia+medidor RX1–RX4 | Medidor y control deslizante combinados. Arrastre para establecer la ganancia TCI RX de cada canal. El medidor refleja el nivel de recepción en tiempo real con suavizado exponencial. | 0.5 | 0.0–1.0 | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| Ganancia+medidor TX | Medidor y control deslizante combinados. Arrastre para establecer la ganancia TCI TX. El medidor refleja el nivel de transmisión en tiempo real. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Etiquetas de asignación de slice RX/TX | Indicadores junto a cada fila que muestran qué slice maneja ese canal (p. ej., `Slice A`). Muestra `—` cuando no hay ningún slice asignado. | `—` | `—` o `Slice <letter>` | — |
| Puerto | Puerto TCP al que se enlaza el servidor. Cambiar este campo mientras el servidor está en ejecución lo reinicia en el nuevo puerto. Los valores fuera de rango se ajustan a `50001`. | `50001` | 1024–65535 | `TciPort` |
| Enable | Botón de alternancia. Inicia el servidor cuando está activado; lo detiene cuando está desactivado. Vuelve a desactivado si el enlace al puerto falla. | Desactivado | — | — |
| Estado del servidor | Etiqueta de solo lectura que muestra el estado del servidor y el número de clientes conectados. Se vuelve rojo cuando ocurre un error de enlace. | `(stopped)` | — | — |

## Consejos

- Para abrir el applet TCI, haga clic en el botón TCI de la bandeja en la barra lateral derecha. El applet está oculto de forma predeterminada.
- Para iniciar el servidor TCI automáticamente cada vez que AetherSDR se inicia, active `Settings > Autostart TCI with AetherSDR`. Esto es independiente del botón Enable del applet.
- Las etiquetas de asignación de slice siguen la asignación de canales DAX. Si a un slice no se le ha asignado un canal DAX, su fila muestra `—`.

## Relacionados

- [Activar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia TCI RX por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TCI TX](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al lanzar la aplicación](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
