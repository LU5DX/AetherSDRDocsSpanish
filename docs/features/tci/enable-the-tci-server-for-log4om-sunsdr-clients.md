# Activar el servidor TCI para clientes Log4OM / SunSDR

El applet TCI Server ejecuta un servidor WebSocket que permite a software de terceros, como Log4OM y herramientas SunSDR, leer y controlar la radio mediante el protocolo TCI. Use esta página para abrir el applet e iniciar el servidor.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- El panel de applets debe estar visible. Si está oculto, vaya a `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha. El applet TCI Server aparece en el panel de applets.
2. Verifique el campo **Port**. El valor predeterminado es `50001`. Cámbielo si otra aplicación ya usa ese puerto (rango válido: 1024–65535; los valores fuera de rango se restablecen a `50001`).
3. Haga clic en **Enable**. El botón se resalta y el estado del servidor cambia de `(stopped)` a `:<port> (0 clients)`.
4. Apunte su cliente TCI (Log4OM, herramienta SunSDR, etc.) a la dirección del host de AetherSDR y al puerto que aparece en el área de estado.

Cuando un cliente se conecta, el estado se actualiza a `:<port> (1 client)` o muestra el número de clientes conectados.

## Qué hace cada control

| Control | Función | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Port** | Establece el puerto TCP en el que escucha el servidor WebSocket TCI. Cambiar el puerto mientras el servidor está en ejecución lo reinicia automáticamente. | `50001` | 1024–65535 | `TciPort` |
| **Enable** | Inicia o detiene el servidor TCI. | Desactivado | — | — |
| Medidor+control **RX1–RX4** | Medidor y control deslizante combinados. Arrastre para ajustar la ganancia TCI RX de ese canal. La etiqueta junto a cada fila indica qué slice está asignado (p. ej., `Slice A`), o `—` si no hay ninguno asignado. | 0.5 | 0.0–1.0 | `TciRxGain1` – `TciRxGain4` |
| Medidor+control **TX** | Medidor y control deslizante combinados. Arrastre para ajustar la ganancia TCI TX. La etiqueta muestra el slice TX activo o `—`. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Estado del servidor | Indicador de solo lectura que muestra el estado del servidor y el número de clientes conectados. Se vuelve rojo y muestra `(port in use)` si ocurre un error de enlace. | `(stopped)` | — | — |

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que se inicie AetherSDR, active `Settings > Autostart TCI with AetherSDR`.
- Las asignaciones de slice RX que se muestran junto a cada fila RX siguen el mapeo de canales DAX. Asigne un canal DAX a un slice para poblar esas etiquetas.

## Solución de problemas

- **Enable vuelve a desactivarse y el estado muestra `(port in use)`** — Otra aplicación ya está enlazada a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable** nuevamente.
- **El estado permanece en `(stopped)` después de hacer clic en Enable** — Confirme que la radio está conectada. El applet TCI requiere una conexión de radio activa y no se iniciará sin una.
- **El applet TCI o el botón de bandeja TCI no son visibles** — Es posible que su compilación no incluya soporte para WebSocket. La función TCI requiere una compilación de AetherSDR con WebSocket habilitado.

## Temas relacionados

- [Descripción general del servidor TCI](overview.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia TCI RX por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TCI TX](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al lanzar la aplicación](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
