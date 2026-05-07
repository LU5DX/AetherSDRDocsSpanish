# Habilitar el inicio automático de rigctld con AetherSDR

Cuando esta configuración está activada, AetherSDR inicia automáticamente un servidor CAT rigctld cada vez que se inicia la aplicación. Esto permite que el software externo de registro, concurso y modo digital se conecte a su radio a través de la interfaz estándar rigctld sin necesidad de pasos manuales de inicio.

## Antes de comenzar

- AetherSDR debe estar instalado y poder alcanzar su radio FLEX-8600.
- rigctld debe estar instalado y accesible en la ruta PATH de su sistema.

## Pasos

1. Haga clic en **Settings** en la barra de menú.
2. Haga clic en **Autostart rigctld with AetherSDR**.

El elemento del menú se activa o desactiva cada vez que hace clic en él. Una marca de verificación junto a la etiqueta indica que está habilitado. La configuración persiste entre sesiones mediante la clave AppSettings `AutoStartRigctld`.

## Qué hace cada control

| Control | Descripción | Clave persistida |
|---|---|---|
| Autostart rigctld with AetherSDR | Elemento de menú seleccionable. Cuando está marcado, AetherSDR inicia rigctld al arrancar. Cuando no está marcado, rigctld no se inicia automáticamente. | `AutoStartRigctld` |

## Consejos

- Para deshabilitar el inicio automático, haga clic nuevamente en **Settings > Autostart rigctld with AetherSDR** para eliminar la marca de verificación.
- Si solo necesita control CAT mediante puerto serie virtual en lugar de rigctld, consulte [Habilitar el inicio automático de CAT con AetherSDR](enable-autostart-for-cat-with-aethersdr.md).

## Solución de problemas

- **rigctld no se inicia al lanzar** — Confirme que rigctld está instalado y disponible en la ruta PATH de su sistema. Si no se encuentra el binario, AetherSDR no puede iniciarlo independientemente de esta configuración.
- **El software externo no puede conectarse a rigctld** — Verifique que el puerto en el que escucha rigctld no esté bloqueado por un cortafuegos y coincida con el puerto configurado en su software externo. Consulte la documentación de rigctld para la configuración del puerto.

## Relacionados

- [Habilitar el inicio automático de CAT con AetherSDR](enable-autostart-for-cat-with-aethersdr.md)
- [Habilitar el inicio automático de TCI con AetherSDR](enable-autostart-for-tci-with-aethersdr.md)
- [Habilitar el inicio automático de DAX con AetherSDR](enable-autostart-for-dax-with-aethersdr.md)
- [Primeros pasos](getting-started.md)
