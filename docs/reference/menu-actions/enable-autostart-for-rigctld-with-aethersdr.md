# Habilitar el inicio automático de rigctld con AetherSDR

Cuando esta configuración está habilitada, AetherSDR inicia automáticamente un servidor CAT rigctld cada vez que se abre la aplicación. Esto permite que software externo de registro, concursos y modos digitales se conecte a su radio a través de la interfaz estándar de rigctld sin necesidad de pasos de inicio manual.

## Antes de comenzar

- AetherSDR debe estar instalado y poder comunicarse con su radio FLEX-8600.
- rigctld debe estar instalado y ser accesible en el PATH de su sistema.

## Pasos

1. Haga clic en **Settings** en la barra de menú.
2. Haga clic en **Autostart rigctld with AetherSDR**.

El elemento de menú se activa o desactiva cada vez que hace clic en él. Una marca de verificación junto a la etiqueta indica que está habilitado. La configuración se conserva entre sesiones mediante la clave `AutoStartRigctld` de AppSettings.

## Qué hace cada control

| Control | Descripción | Clave persistente |
|---|---|---|
| Autostart rigctld with AetherSDR | Elemento de menú con casilla de verificación. Cuando está marcado, AetherSDR inicia rigctld al arrancar. Cuando no está marcado, rigctld no se inicia automáticamente. | `AutoStartRigctld` |

## Consejos

- Para deshabilitar el inicio automático, haga clic nuevamente en **Settings > Autostart rigctld with AetherSDR** para quitar la marca de verificación.
- Si solo necesita control CAT por puerto serie virtual en lugar de rigctld, consulte [Habilitar el inicio automático de CAT con AetherSDR](enable-autostart-for-cat-with-aethersdr.md).

## Solución de problemas

- **rigctld no se inicia al arrancar** — Confirme que rigctld está instalado y disponible en el PATH de su sistema. Si no se puede encontrar el ejecutable, AetherSDR no podrá iniciarlo independientemente de esta configuración.
- **El software externo no puede conectarse a rigctld** — Verifique que el puerto en el que escucha rigctld no esté bloqueado por un cortafuegos y coincida con el puerto configurado en su software externo. Consulte la documentación de rigctld para la configuración del puerto.

## Relacionados

- [Habilitar el inicio automático de CAT con AetherSDR](enable-autostart-for-cat-with-aethersdr.md)
- [Habilitar el inicio automático de TCI con AetherSDR](enable-autostart-for-tci-with-aethersdr.md)
- [Habilitar el inicio automático de DAX con AetherSDR](enable-autostart-for-dax-with-aethersdr.md)
- [Primeros pasos](getting-started.md)
