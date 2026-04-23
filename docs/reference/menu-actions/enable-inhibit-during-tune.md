# Activar Inhibit durante TUNE

Use `Settings > Inhibit during TUNE` para seleccionar qué líneas de salida TX suprime el radio Flex mientras el sintonizador está en funcionamiento. Esto evita que la RF llegue a amplificadores o conmutadores de antena que no deben recibir potencia de sintonización.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- Identifique qué conectores de salida TX de su radio están conectados al equipo que desea proteger durante la sintonización.

## Pasos

1. Haga clic en `Settings` en la barra de menús.
2. Pase el cursor sobre `Inhibit during TUNE` para abrir el submenú.
3. Haga clic en una o más casillas de verificación de la lista para activar el inhibit en esas salidas:
   - `None` — ninguna salida es suprimida durante la sintonización.
   - `ACC TX` — suprime la línea ACC TX.
   - `TX1` — suprime la salida TX1.
   - `TX2` — suprime la salida TX2.
   - `TX3` — suprime la salida TX3.
4. Repita el proceso para cada salida que desee inhibir. Las selecciones son casillas de verificación independientes; puede activar cualquier combinación.

## Qué hace cada control

| Casilla de verificación | Efecto durante TUNE |
|---|---|
| `None` | Ninguna salida es inhibida. La RF de sintonización pasa por todas las líneas TX configuradas. |
| `ACC TX` | La línea de control ACC TX se mantiene inactiva mientras el sintonizador funciona. |
| `TX1` | La salida TX1 es suprimida mientras el sintonizador funciona. |
| `TX2` | La salida TX2 es suprimida mientras el sintonizador funciona. |
| `TX3` | La salida TX3 es suprimida mientras el sintonizador funciona. |

## Consejos

- Si utiliza un amplificador externo en TX1, active `TX1` para evitar que la potencia de sintonización lo alcance mientras el sintonizador interno recorre las frecuencias.
- `None` y las casillas de verificación de salida individuales pueden interactuar: si `None` es la única selección, todas las salidas permanecen activas. Activar cualquier salida específica anula eso para esa línea.
- La configuración de inhibit por banda está disponible en `Settings > TX Band Settings...`, que ofrece un control más preciso a nivel de banda.

## Relacionado

- [Configuración de los controles de AetherSDR](configuring-aethersdr-controls.md)
- [Cables USB](usb-cables.md)
