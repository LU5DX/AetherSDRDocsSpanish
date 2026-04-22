# Descripción general del servidor TCI

El applet TCI Server ejecuta un servidor WebSocket que implementa el protocolo Expert TCI, permitiendo que software de terceros como Log4OM y las herramientas SunSDR lean y controlen la radio. Use esta página para entender qué hace cada control; siga los enlaces a las páginas de tareas específicas para realizar operaciones concretas.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- El applet TCI está oculto de forma predeterminada. Haga clic en el botón TCI de la bandeja en la barra lateral derecha para mostrarlo.

## Cómo funciona

El TCI Server de AetherSDR escucha en un puerto TCP configurable las conexiones WebSocket de clientes compatibles con TCI. Cuando está habilitado, expone hasta cuatro canales RX y un canal TX, cada uno asignado a un slice (división de banda) de la radio mediante las asignaciones de canal DAX. Los clientes se conectan, reciben el estado de la radio y pueden emitir comandos de control a través del protocolo TCI.

Cada canal RX (RX1–RX4) transporta el audio del slice asignado al canal DAX correspondiente. El canal TX transporta el audio del slice que esté actualmente activo como slice TX. Los indicadores de asignación de slice en el applet se actualizan automáticamente a medida que los slices se agregan o reasignan.

El indicador de estado del servidor muestra el estado actual de un vistazo. Cuando el servidor está detenido, indica `(stopped)`. Cuando está en funcionamiento, indica `:<puerto> (N clients)` — por ejemplo `:50001 (2 clients)`. Si el puerto no puede enlazarse, el indicador se vuelve rojo y muestra `(port in use)`.

Habilitar el inicio automático mediante `Settings > Autostart TCI with AetherSDR` hace que el servidor arranque automáticamente cada vez que AetherSDR se inicia, usando el valor guardado en `TciPort`.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Ganancia+medidor RX1–RX4 | Medidor y deslizador combinados. El medidor refleja el nivel de audio RX entrante. Arrastre para establecer la ganancia TCI RX de ese canal. | 0.5 | 0.0–1.0 | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| Ganancia+medidor TX | Medidor y deslizador combinados. El medidor refleja el nivel de audio TX saliente. Arrastre para establecer la ganancia TCI TX. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Etiquetas de asignación de slice RX/TX | Indicadores de solo lectura que muestran qué slice maneja cada canal. Muestra `—` cuando no hay ningún slice asignado, o `Slice <letra>` cuando un slice está mapeado. | `—` | `—` o `Slice <letra>` | — |
| Puerto | Establece el puerto TCP en el que escucha el servidor. Si el servidor está en funcionamiento cuando se cambia este valor, se reinicia automáticamente en el nuevo puerto. Los valores fuera de rango se ajustan a `50001`. | `50001` | 1024–65535 | `TciPort` |
| Enable | Inicia o detiene el servidor TCI. Si el puerto no puede enlazarse, el botón vuelve a la posición de apagado y el estado muestra `(port in use)`. | Off | — | — |
| Estado del servidor | Indicador de solo lectura que muestra `(stopped)`, `:<puerto> (N clients)` o `(port in use)`. Se vuelve rojo si falla el enlace del puerto. | `(stopped)` | — | — |

## Solución de problemas

- **El estado muestra `(port in use)` y Enable vuelve a apagarse** — Otra aplicación ya está enlazada a ese puerto. Cambie el puerto en el campo Port a un valor diferente en el rango 1024–65535 y haga clic en Enable nuevamente.
- **Las etiquetas de asignación de slice muestran `—` en todos los canales** — Ningún slice ha sido asignado a un canal DAX. Asigne canales DAX a sus slices; las asignaciones TCI RX siguen el mismo mapeo.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia TCI RX por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TCI TX](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al arrancar](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
