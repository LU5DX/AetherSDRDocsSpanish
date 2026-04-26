# Habilitar el servidor TCI para clientes Log4OM / SunSDR

El applet TCI Server ejecuta un servidor WebSocket que permite a software de terceros — como Log4OM y las herramientas SunSDR — leer y controlar la radio mediante el protocolo Expert TCI. Esta página explica cómo iniciar el servidor por primera vez.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón **TCI** de la barra lateral derecha para abrir el applet TCI Server.
2. Confirme que el campo **Port** muestra el puerto que espera su cliente. El valor predeterminado es `50001`. Los valores válidos son 1024–65535; los valores fuera de ese rango vuelven automáticamente a `50001`.
3. Haga clic en **Enable**.
4. Compruebe el indicador de estado del servidor junto al botón **Enable**. Cuando el servidor se inicia correctamente, muestra `:<port> (0 clients)`. Al conectarse un cliente, el contador se incrementa.

## Función de cada control

| Control | Descripción | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Port** | Puerto TCP en el que escucha el servidor WebSocket TCI. Cambiar el puerto mientras el servidor está en ejecución lo reinicia automáticamente. | `50001` | 1024–65535 | `TciPort` |
| **Enable** | Inicia o detiene el servidor TCI. | Desactivado | Activado / Desactivado | — |
| **RX1–RX4 gain+meter** | Medidor de nivel y control deslizante de ganancia combinados para cada canal de recepción TCI. Arrastre para ajustar la ganancia de salida de ese canal. | 0.5 | 0.0–1.0 | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| **TX gain+meter** | Medidor de nivel y control deslizante de ganancia combinados para el canal de transmisión TCI. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Etiquetas de asignación de slice RX/TX | Indicadores de solo lectura que muestran qué slice controla cada fila RX o TX (por ejemplo, `Slice A`). Muestra `—` cuando no hay ningún slice asignado. | `—` | `—` o `Slice <letter>` | — |
| Estado del servidor | Muestra `(stopped)`, `:<port> (N clients)` o `(port in use)`. Se vuelve rojo si falla el enlace al puerto. | `(stopped)` | — | — |

## Consejos

- Los canales RX1–RX4 comparten las mismas asignaciones de canal DAX. La letra de slice que aparece junto a cada fila refleja el slice actualmente asignado a ese canal DAX.
- Para que el servidor se inicie automáticamente cada vez que AetherSDR arranque, use `Settings > Autostart TCI with AetherSDR` en lugar de hacer clic en **Enable** en cada sesión.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable vuelve a desactivarse** — Otra aplicación ya está utilizando ese puerto. Ingrese un número de puerto diferente en el campo **Port** y, a continuación, haga clic en **Enable** nuevamente.

## Relacionados

- [Descripción general del TCI Server](overview.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Inicio automático de TCI al arrancar](autostart-tci-on-launch.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
