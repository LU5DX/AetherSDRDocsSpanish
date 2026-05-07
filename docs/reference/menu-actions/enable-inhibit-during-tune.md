# Habilitar inhibición durante TUNE

Use `Settings > Inhibit during TUNE` para seleccionar qué salidas TX suprime el FLEX-8600 mientras el sintonizador está funcionando. Esto evita que RF llegue a amplificadores o puertos de antena que no deberían ser activados durante un ciclo de sintonización.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- Confirme qué puertos de salida TX están en uso en su estación antes de cambiar esta configuración.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Pase el cursor sobre `Inhibit during TUNE` para abrir el submenú.
3. Haga clic en cualquier combinación de las siguientes casillas de verificación para habilitar la inhibición en esas salidas durante la sintonización:
   - `None`
   - `ACC TX`
   - `TX1`
   - `TX2`
   - `TX3`

   Una marca de verificación al lado de un elemento significa que esa salida se suprimirá durante un ciclo de sintonización. Seleccionar `None` indica que no se inhibe ninguna salida.

## Qué hace cada control

| Casilla | Efecto al estar marcada |
|----------|------------------------|
| `None` | Ninguna salida TX se suprime durante la sintonización. |
| `ACC TX` | Suprime la salida ACC TX durante la sintonización. |
| `TX1` | Suprime la salida TX1 durante la sintonización. |
| `TX2` | Suprime la salida TX2 durante la sintonización. |
| `TX3` | Suprime la salida TX3 durante la sintonización. |

## Consejos

- Puede marcar múltiples salidas simultáneamente. Por ejemplo, marcar `TX1` y `TX2` inhibe ambos puertos mientras deja `TX3` activo.
- La configuración de inhibición por banda está disponible en `Settings > TX Band Settings...`, lo que proporciona un control más preciso sobre el comportamiento de inhibición por banda.

## Relacionado

- [Configurando los controles de AetherSDR](configuring-aethersdr-controls.md)
