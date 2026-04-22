# Habilitar el inicio automático de TCI con AetherSDR

Esta página explica cómo configurar AetherSDR para que inicie su servidor TCI automáticamente cada vez que se lanza la aplicación. Use esta función si ejecuta software de registro de QSO o de concursos que se conecta a AetherSDR mediante TCI.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte para WebSockets. Si `Settings > Autostart TCI with AetherSDR` no aparece en el menú, su versión no incluye esta función.
- Conéctese a su FLEX-8600 antes de habilitar el inicio automático si desea verificar que TCI funciona correctamente tras el cambio.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Haga clic en `Autostart TCI with AetherSDR`.

El elemento es una entrada de menú con casilla de verificación. Una marca indica que la opción está activada. Al hacer clic se activa o desactiva la marca y el cambio se guarda inmediatamente en `AutoStartTCI`.

3. Reinicie AetherSDR para confirmar que el servidor TCI se inicia al lanzar la aplicación.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Clave persistente |
|---|---|---|---|
| `Autostart TCI with AetherSDR` | Cuando está marcado, AetherSDR inicia el servidor TCI cada vez que se lanza, sin requerir intervención manual. | Desactivado | `AutoStartTCI` |

## Relacionados

- [Habilitar el inicio automático de CAT con AetherSDR](enable-autostart-for-cat-with-aethersdr.md)
- [Habilitar el inicio automático de DAX con AetherSDR](enable-autostart-for-dax-with-aethersdr.md)
- [Habilitar el inicio automático de rigctld con AetherSDR](enable-autostart-for-rigctld-with-aethersdr.md)
- [Primeros pasos](getting-started.md)
