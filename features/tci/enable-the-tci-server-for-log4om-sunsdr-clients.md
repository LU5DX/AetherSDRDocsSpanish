# Habilitar el servidor TCI para clientes Log4OM / SunSDR

AetherSDR incluye un servidor TCI WebSocket integrado que permite a software de terceros — como Log4OM y las herramientas SunSDR — leer y controlar la radio mediante el protocolo TCI. Esta página explica cómo abrir el applet TCI e iniciar el servidor.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha. El applet TCI Server aparece en el panel de applets.
2. Verifique el campo **Port**. El valor predeterminado es `50001`. Cámbielo si otra aplicación ya está usando ese puerto (rango válido: 1024–65535; los valores fuera de rango vuelven automáticamente a `50001`).
3. Haga clic en **Enable**. El botón se resalta en verde cuando el servidor está en ejecución.
4. Confirme que el indicador de estado del servidor junto a **Enable** cambia de `(stopped)` a `:<puerto> (0 clients)`. Cuando un cliente se conecta, el contador se incrementa — por ejemplo, `50001 (1 client)`.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Port** | Puerto TCP en el que escucha el servidor TCI WebSocket. Cambiar el valor mientras el servidor está en ejecución lo reinicia automáticamente. | `50001` | 1024–65535 | `TciPort` |
| **Enable** | Inicia o detiene el servidor TCI. | Desactivado | — | — |
| Medidor y deslizador de ganancia **RX1–RX4** | Medidor y deslizador combinados. Arrastre para establecer la ganancia TCI RX de cada canal. | 0.5 | 0.0–1.0 | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| Medidor y deslizador de ganancia **TX** | Medidor y deslizador combinados. Arrastre para establecer la ganancia TCI TX. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Etiquetas de asignación de slice RX/TX | Indicadores de solo lectura que muestran qué slice controla cada fila RX o TX (por ejemplo, `Slice A`). Muestra `—` cuando no hay ningún slice asignado. | `—` | — | — |
| Estado del servidor | Muestra el estado actual del servidor y el número de clientes conectados. Se torna rojo y muestra `(port in use)` si ocurre un error de enlace. | `(stopped)` | — | — |

## Consejos

- Para que el servidor TCI se inicie automáticamente cada vez que AetherSDR se lance, habilite `Settings > Autostart TCI with AetherSDR` en lugar de hacer clic en **Enable** en cada sesión.
- Las etiquetas de asignación de slice junto a cada fila RX siguen la misma asignación de canales DAX. Si una fila muestra `—`, asigne un canal DAX al slice correspondiente.

## Solución de problemas

- **El botón Enable vuelve a desactivarse y el estado muestra `(port in use)`** — Otra aplicación ya está enlazada al puerto configurado. Ingrese un valor diferente en **Port** y haga clic en **Enable** nuevamente.
- **El applet TCI no aparece en el panel de applets** — Es posible que su versión de AetherSDR no incluya compatibilidad con WebSocket. El applet TCI solo está presente en versiones compiladas con soporte WebSocket habilitado.

## Temas relacionados

- [Descripción general del servidor TCI](overview.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Inicio automático de TCI al lanzar](autostart-tci-on-launch.md)
- [Ajustar la ganancia TCI RX por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TCI TX](adjust-tci-tx-gain.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
