# Habilitar Inhibit durante TUNE

Use `Settings > Inhibit during TUNE` para seleccionar qué salidas de TX suprime el FLEX-8600 mientras el sintonizador está en funcionamiento. Esto evita que la RF llegue a amplificadores o puertos de antena que no deben activarse durante un ciclo de sintonización.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- Confirme qué puertos de salida de TX están en uso en su estación antes de modificar estos ajustes.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Coloque el cursor sobre `Inhibit during TUNE` para abrir el submenú.
3. Haga clic en cualquier combinación de las siguientes casillas de verificación para habilitar el inhibit en esas salidas durante la sintonización:
   - `None`
   - `ACC TX`
   - `TX1`
   - `TX2`
   - `TX3`

   Una marca de verificación junto a un elemento indica que esa salida será suprimida durante un ciclo de sintonización. Seleccionar `None` indica que ninguna salida está inhibida.

## Qué hace cada control

| Casilla | Efecto al activarse |
|----------|---------------------|
| `None` | Ninguna salida de TX es suprimida durante la sintonización. |
| `ACC TX` | Suprime la salida ACC TX durante la sintonización. |
| `TX1` | Suprime la salida TX1 durante la sintonización. |
| `TX2` | Suprime la salida TX2 durante la sintonización. |
| `TX3` | Suprime la salida TX3 durante la sintonización. |

## Consejos

- Es posible marcar varias salidas simultáneamente. Por ejemplo, marcar `TX1` y `TX2` inhibe ambos puertos mientras `TX3` permanece activo.
- Los ajustes de inhibit por banda están disponibles en `Settings > TX Band Settings...`, lo que proporciona un control más preciso del comportamiento del inhibit según la banda.

## Relacionado

- [Configuración de los controles de AetherSDR](configuring-aethersdr-controls.md)
