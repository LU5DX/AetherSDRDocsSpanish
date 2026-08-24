# Omita el amplificador VK3AMP

Extraiga el amplificador VK3AMP de la ruta de señal de transmisión para poder operar sin amplificador (barefoot) o solucionar un problema.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- El amplificador VK3AMP debe ser accesible por TCP con telemetría UDP habilitada.

## Pasos

1. Abra el panel de Applet y haga clic en el mosaico **VKAMP**.
2. Localice el botón **BYPASS**. La etiqueta muestra el estado actual: "BYPASS" en ámbar significa que el amplificador está omitido; "BYPASS" en verde significa que el amplificador está en línea.
3. Haga clic en **BYPASS** para alternar entre operación omitida y en línea.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **BYPASS** | Alterna el amplificador entre omitido y en línea. La etiqueta del botón muestra el estado actual, no la acción que está a punto de realizar. Borde ámbar = omitido; borde verde = en línea. |
| **COOLING** | Alterna la anulación del enfriamiento. El estado activo se muestra con un color de texto normal. |

## Consejos

- La etiqueta del botón **BYPASS** le indica el estado actual, no lo que hará al hacer clic. Si el botón muestra "BYPASS" en ámbar, el amplificador ya está omitido.
- Cuando se pierde la conexión con la radio, la aplicación borra el estado de omisión y restablece el botón: el amplificador vuelve a su estado predeterminado, no necesariamente a omitido.

## Solución de problemas

- **El amplificador no se omite cuando hago clic en BYPASS** — Verifique que la conexión del amplificador esté activa (revise la píldora de estado en la parte superior del applet). Si la conexión está caída, el botón está deshabilitado y no responderá.
- **El botón muestra en línea pero el amplificador está realmente omitido** — El botón refleja el último estado conocido del amplificador. Si el amplificador se cambió externamente, espere la próxima actualización de telemetría: la pantalla refleja el estado en vivo, no su último clic.

## Relacionado

- [Descripción general del amplificador VK3AMP](overview.md)
- [Supervise la potencia directa y reflejada en el amplificador VK3AMP](monitor-forward-and-reflected-power-on-the-vk3amp-amplifier.md)
- [Seleccione el puerto de antena VK3AMP](select-the-vk3amp-antenna-port.md)
