# Habilitar el inicio automático de TCI con AetherSDR

Esta página explica cómo configurar AetherSDR para que inicie el servidor TCI automáticamente cada vez que se ejecute la aplicación, de modo que no necesite activar TCI manualmente después de cada reinicio.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte para WebSocket (`HAVE_WEBSOCKETS`). Si el elemento del menú está ausente, su compilación no incluye TCI.
- Debe estar familiarizado con la forma en que el software cliente TCI se conecta al servidor TCI de AetherSDR.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Haga clic en `Autostart TCI with AetherSDR`.

El elemento del menú es un conmutador que se puede marcar. Una marca de verificación junto a la etiqueta indica que el inicio automático está habilitado. Al hacer clic nuevamente se elimina la marca y se deshabilita el inicio automático.

## Descripción de cada control

| Control | Descripción | Predeterminado | Clave persistida |
|---|---|---|---|
| `Autostart TCI with AetherSDR` | Cuando está marcado, AetherSDR inicia el servidor TCI inmediatamente al ejecutarse sin requerir activación manual. | Desactivado | `AutoStartTCI` |

## Consejos

- Si solo ejecuta clientes TCI ocasionalmente, deje el inicio automático desactivado e inicie el servidor TCI manualmente cuando sea necesario para evitar el uso innecesario de recursos.
- La configuración se guarda inmediatamente cuando alterna el elemento del menú. No es necesario reiniciar AetherSDR para que los inicios futuros respeten el nuevo valor.

## Relacionados

- [Habilitar el inicio automático de CAT con AetherSDR](enable-autostart-for-cat-with-aethersdr.md)
- [Habilitar el inicio automático de DAX con AetherSDR](enable-autostart-for-dax-with-aethersdr.md)
- [Habilitar el inicio automático de rigctld con AetherSDR](enable-autostart-for-rigctld-with-aethersdr.md)
- [Introducción](getting-started.md)
