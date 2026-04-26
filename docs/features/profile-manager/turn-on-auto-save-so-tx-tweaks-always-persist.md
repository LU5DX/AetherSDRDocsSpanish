# Activar el guardado automático para que los ajustes de TX siempre persistan

Active el guardado automático para que cualquier cambio que realice en los ajustes de transmisión y micrófono se escriba automáticamente en el perfil activo, sin necesidad de guardar manualmente después de cada ajuste.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Profile Manager requiere una conexión de radio activa.
- Debe existir al menos un perfil de transmisión en la radio para que el guardado automático tenga un perfil donde escribir.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña **Auto-Save**.
3. Marque **Auto-save profile changes**.
4. Haga clic en **Close**.

La configuración surte efecto de inmediato. AetherSDR envía el cambio a la radio y guarda su elección en `AutoSaveTransmitProfile`.

## Qué hace cada control

| Control | Descripción | Ajuste persistido |
|---|---|---|
| **Auto-save profile changes** | Cuando está marcado, los cambios en los ajustes de TX y micrófono se escriben automáticamente en el perfil activo. Cuando no está marcado, los cambios se descartan a menos que guarde manualmente. | `AutoSaveTransmitProfile` |

## Consejos

- Para desactivar el guardado automático, vuelva a `Profiles > Profile Manager...`, haga clic en la pestaña **Auto-Save** y desmarque **Auto-save profile changes**.
- Si desea una base limpia antes de activar el guardado automático, cargue primero el perfil deseado desde la pestaña **Transmit** y luego active el guardado automático.

## Relacionado

- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Guardar el estado actual de la radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Descripción general del Profile Manager](overview.md)
