# Habilitar el inicio automático de TCI con AetherSDR

Esta página explica cómo configurar AetherSDR para que inicie el servidor TCI automáticamente cada vez que se lanza la aplicación, de modo que no sea necesario habilitar TCI manualmente tras cada reinicio.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el elemento de menú no aparece, su compilación no incluye TCI.
- Debe estar familiarizado con la forma en que el software cliente TCI se conecta al servidor TCI de AetherSDR.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Haga clic en `Autostart TCI with AetherSDR`.

El elemento de menú es un interruptor de selección. Una marca de verificación junto a la etiqueta indica que el inicio automático está habilitado. Al hacer clic de nuevo se elimina la marca y se deshabilita el inicio automático.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Clave guardada |
|---|---|---|---|
| `Autostart TCI with AetherSDR` | Cuando está marcado, AetherSDR inicia el servidor TCI inmediatamente al lanzarse, sin requerir activación manual. | Desactivado | `AutoStartTCI` |

## Consejos

- Si solo utiliza clientes TCI en algunas ocasiones, deje el inicio automático desactivado e inicie el servidor TCI manualmente cuando sea necesario, para evitar el uso innecesario de recursos.
- La configuración se guarda de inmediato al activar o desactivar el elemento de menú. No se requiere reiniciar AetherSDR para que los lanzamientos futuros respeten el nuevo valor.

## Relacionados

- [Habilitar el inicio automático de CAT con AetherSDR](enable-autostart-for-cat-with-aethersdr.md)
- [Habilitar el inicio automático de DAX con AetherSDR](enable-autostart-for-dax-with-aethersdr.md)
- [Habilitar el inicio automático de rigctld con AetherSDR](enable-autostart-for-rigctld-with-aethersdr.md)
- [Primeros pasos](getting-started.md)
